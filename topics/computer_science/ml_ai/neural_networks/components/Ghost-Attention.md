---
tags:
  - ml_ai
  - ml_ai/neural_nets
created: 2025-04-18T21:26
modified: 2026-02-15T10:11
published:
sources:
  - "[Llama 2: Open Foundation and Fine-Tuned Chat Models](https://arxiv.org/abs/2307.09288)"
topics:
  - Self-Attention
authors:
ai-assisted:
hidden:
public: true
---
# Ghost-Attention
> In a dialogue setup, some instructions should apply for all the conversation turns, e.g., to respond succinctly, or to “act as” some public figure. When we provided such instructions to **LLAMA 2-CHAT**, the subsequent response should always respect the constraint. However, our initial RLHF models tend to forget the initial instruction after a few turns of dialogue, as illustrated in Figure 9 (left).
> 
> To address these limitations, we propose Ghost Attention (GAtt), a very simple method inspired by Context Distillation (Bai et al., 2022b) that hacks the fine-tuning data to help the attention focus in a multi-step process. GAtt enables dialogue control over multiple turns, as illustrated in Figure 9 (right).
> 
> **GAtt Method.** Assume we have access to a multi-turn dialogue dataset between two persons (e.g., a user and an assistant), with a list of messages \(\[u_1, a_1, \ldots, u_n, a_n\]\), where \(u_n\) and \(a_n\) correspond to the user and assistant messages for turn *n*, respectively. Then, we define an instruction, *inst*, that should be respected throughout the dialogue. For example, *inst* could be “act as.” We can then synthetically concatenate this instruction to all the user messages of the conversation.
> 
> Next, we can sample from this synthetic data using the latest RLHF model. We now have a context-dialogue and the sample with which to fine-tune a model, in a process analogous to Rejection Sampling. Instead of augmenting all context-dialogue turns with the instruction, we can drop it in all but the first turn, but this would lead to a mismatch at training time between the system message, i.e., all the intermediate assistant messages that come before the last turn, and our sample. To fix this issue, which could hurt the training, we simply set the loss to 0 for all the tokens from the previous turns, including assistant messages.
> 
> For the training instructions, we created a few synthetic constraints to sample from: Hobbies (“*You enjoy e.g. Tennis*”), Language (“*Speak in e.g. French*”), or Public Figure (“*Act as e.g. Napoleon*”). To obtain the lists of hobbies and public figures, we asked **LLAMA 2-CHAT** to generate it, avoiding a mismatch between the instruction and model knowledge (e.g., asking the model to act as someone it had not encountered during training). To make the instructions more complex and diverse, we construct the final instruction by randomly combining the above constraints. When constructing the final system message for the training data, we also modify the original instruction half of the time to be less verbose, e.g., *“Always act as Napoleon from now”* → *“Figure: Napoleon.”* These steps produce an SFT dataset, which we can fine-tune **LLAMA 2-CHAT** on.

## Summary
Source: ChatGPT 4o[^1]
Ghost Attention is not an architectural change but a data augmentation method used during supervised fine-tuning. The core idea involves embedding the system prompt into each user message during training, ensuring the model consistently considers the system instructions.​
**Training Process:**
1. **Augmentation:** For each user message in the training dataset, the system prompt is prepended, effectively combining them into a single input.​
2. **Response Generation:** The model generates responses based on these augmented inputs, learning to associate the system instructions with user queries.​
3. **Fine-Tuning:** After sufficient training, the model internalizes the system prompt's influence, allowing it to generate appropriate responses even when the prompt isn't explicitly present in the user message.​
    
This method ensures that the model maintains the context and directives provided by the system prompt across multiple interactions.

[^1]: Prompt: "And can you explain how does the Ghost Attention fits into this? Is the Ghost Attention just specific way of fine-tuning LLMs for processing system messages?"