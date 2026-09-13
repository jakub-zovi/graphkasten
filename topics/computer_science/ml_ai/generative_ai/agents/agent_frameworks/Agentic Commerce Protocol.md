---
tags:
  - gen_ai
  - gen_ai/agents
created: 2026-04-03T12:00
modified: 2026-08-01T11:12
published:
sources:
  - "[Buy it in ChatGPT: Instant Checkout and the Agentic Commerce Protocol](https://openai.com/index/buy-it-in-chatgpt/)"
  - "[Developing an Open Standard for Agentic Commerce](https://stripe.com/blog/developing-an-open-standard-for-agentic-commerce)"
topics:
  - Agent Payment
  - Payment Protocol
authors:
  - Jakub
ai-assisted: true
hidden:
public: true
human-review: true
---
# Agentic Commerce Protocol
- Open standard interaction model for connecting buyers, their AI agents, and businesses to complete purchases
- Maintained jointly by **OpenAI** and **Stripe** as founding maintainers; Apache 2.0 license
- Spec latest release: **2026-01-30**
- Github: [agentic-commerce-protocol/agentic-commerce-protocol](https://github.com/agentic-commerce-protocol/agentic-commerce-protocol)
	- **1.3k** stars
## How It Works
- Agent queries merchant's ACP-compliant endpoint to retrieve product/inventory data
- Agent presents options to user; user selects and confirms purchase intent
- Encrypted, scoped payment token is generated and passed to merchant
- Merchant fulfills order; confirmation returned to agent
