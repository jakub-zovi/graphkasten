---
tags:
  - gen_ai
  - gen_ai/agents
created: 2026-04-03T12:00
modified: 2026-08-01T11:16
published:
sources:
  - "[Announcing Agent Payments Protocol (AP2)](https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol)"
  - "[AP2 Protocol Documentation](https://ap2-protocol.org/)"
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
# AP2 (Agent Payments Protocol)
- Open protocol for securely initiating and transacting **agent-led payments** across platforms
- Developed by **Google Cloud**; announced **September 2025** in collaboration with 60+ organizations
- Payment-agnostic: supports credit/debit cards, stablecoins, and real-time bank transfers
- Can extend A2A and MCP
- Github: [google-agentic-commerce/AP2](https://github.com/google-agentic-commerce/AP2)
	- **2.9k** stars
## Problems It Solves
- Agent-initiated payments lack a common trust framework — merchants cannot verify that a purchase truly reflects user intent
- No standard mechanism for users to delegate spending authority to agents in a bounded, auditable way
- Fragmented payment integrations across AI platforms and merchants
## Design Principles
- **Authorization** — proves users explicitly granted agents specific purchase authority
- **Authenticity** — allows merchants to verify agent requests reflect the user's genuine intent
- **Accountability** — provides mechanisms to resolve fraudulent or incorrect transactions
## Key Features
- **Payment-agnostic** — single protocol spanning fiat (cards, bank transfers) and crypto (stablecoins)
- **A2A × x402 extension** — production-ready crypto payment extension developed with Coinbase, Ethereum Foundation, and MetaMask
- **Extensible** — designed to layer on top of A2A and MCP stacks
- **Enterprise-grade** — built with 60+ industry partners including Mastercard, PayPal, Adyen, Revolut, Salesforce, and Worldpay
