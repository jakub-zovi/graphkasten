---
tags:
  - gen_ai
  - gen_ai/agents
created: 2025-09-02T10:41
modified: 2025-09-08T09:21
published:
sources:
  - "[Why I'm Betting Against AI Agents in 2025 (Despite Building Them)](https://readwise.io/reader/shared/01k0m01krb7x5x8c5k09bznpsr/)"
topics:
authors:
ai-assisted:
hidden:
public: true
---
# Compounding of errors in AI Agents
This not aggregates information about error compounding in multi-step agent workflows. 
## Why I'm Betting Against AI Agents in 2025
After building AI systems, here's what I've learned:
1. Error rates compound exponentially in multi-step workflows. 95% reliability per step = 36% success over 20 steps. Production needs 99.9%+.
2. Context windows create quadratic token costs. Long conversations become prohibitively expensive at scale.
3. The real challenge isn't AI capabilities, it's designing tools and feedback systems that agents can actually use effectively.
### The Mathematical Reality No One Talks About

Here's the uncomfortable truth that every AI agent company is dancing around: error compounding makes autonomous multi-step workflows mathematically impossible at production scale.

![Error Compounding in AI Agent Workflows](https://utkarshkanwat.com/writing/betting-against-agents/error_compounding_graph.svg)

Error Compounding in AI Agent Workflows

Let's do the math. If each step in an agent workflow has 95% reliability, which is optimistic for current LLMs, then:

- 5 steps = 77% success rate
- 10 steps = 59% success rate
- 20 steps = 36% success rate

Production systems need 99.9%+ reliability. Even if you magically achieve 99% per-step reliability (which no one has), you still only get 82% success over 20 steps. This isn't a prompt engineering problem. This isn't a model capability problem. This is mathematical reality.

==My DevOps agent works precisely because it's not actually a 20-step autonomous workflow . It's 3-5 discrete, independently verifiable operations with explicit rollback points and human confirmation gates== (). The "agent" handles the complexity of generating infrastructure code, but the system is architected around the mathematical constraints of reliability.

==Every successful agent system I've built follows the same pattern: bounded contexts, verifiable operations, and human decision points (sometimes) at critical junctions. The moment you try to chain more than a handful of operations autonomously, the math kills you.==
## Error Compounding More Realistic View (i.e. It Gets Worse)
(Source: ChatGPT5[^1])
### Probabilistic view
Consider a pipeline with steps $1,\dots,k$. Let $E_i$ be the event “step $i$ is wrong,” and let $p_i=\Pr(\text{step }i\text{ is correct}\mid\text{all previous steps correct})$.
- **Independent, optimistic baseline.**  
	If every step’s correctness depends only on the ground-truth input (no coupling to earlier mistakes), overall success is $\Pr(\text{all correct})=\prod_{i=1}^{k}p_i$.  
	With five steps at 90% each, $0.9^5=0.59049$, so only $\sim59% $ of runs are fully correct. The union bound shows the same story from the error side: $\Pr(\text{any error})=\Pr\big(\bigcup_i E_i\big)\le\sum_i(1-p_i)$.
- **Realistic coupling (distribution shift).**  
	In practice, once a step errs, later steps see **corrupted context** and become _more likely_ to err. Write $\Pr(E_i\mid\text{previous correct})=e_i,\ \ \Pr(E_i\mid\text{some previous wrong})=e_i+\Delta_i$, where $\Delta_i\ge0$ captures **error amplification**. Then the effective error at step $i$ is $e_i'\approx e_i+\Delta_i\cdot\Pr(\text{any previous error})$, and overall success shrinks to $\prod_i(1-e_i')$, typically much lower than $\prod_i(1-e_i)$.  
	A more general bound makes the coupling explicit: $\Pr\big(\bigcup_i E_i\big)\le\sum_i e_i+\sum_{i>j}c_{ij}e_j$, where $c_{ij}$ measures how much an error at $j$ increases the chance of an error at $i$. The second term is exactly the **compounding**.
### How a human “resets” the error
Introduce a **human checkpoint** after some step $k$ that verifies/edits to ground truth (accuracy $\approx1$ for that field). Probabilistically this is conditioning on a **trusted observation** that **replaces** the model’s uncertain latent state with the correct value.

**Effects:**
1. **Cuts the coupling terms.** In the bound above, any $c_{ij}$ with $i>k>j$ disappears—the human blocks the propagation path from early errors to later steps. Formally, the post-checkpoint steps again operate at their _clean-input_ error rates $e_{k+1},e_{k+2},\dots$ instead of inflated $e_i'$.
2. **Resets distribution shift.** Downstream prompts are re-grounded on a gold context; the $\Delta_i$ terms drop to $\approx0$ after the checkpoint.
3. **Improves expected utility under selective routing.** If the system is calibrated, hand off to human when model confidence $<\tau$. Let $H$ be the (random) set of routed cases. Then expected error becomes $\mathbb{E}[\text{error}]\approx\Pr(\text{no human})\cdot\text{pipeline error on high-confidence cases}$, while human workload is $\Pr(H)$. With good calibration, you remove the tail of hard cases—the ones that cause most cascades—at modest cost.

[^1]: Prompts: "Explain to me the accumulation of the error in the multi-step LLM workflow from a probabilistic or statistical perspective. And mention how this error can be reset by including human in some setp to reset the error.", ""