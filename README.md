# Agent Commerce Manifest (ACM)

> An open ontology standard for businesses to be discoverable, understandable, and transactable by AI agents — without human intermediation.

**Proposed by [No GUI](https://no-gui.com) · v0.1 · September 2026**

---

## What is ACM?

ACM is a **vertical ontology for agent commerce**. It describes a business's reality — what it offers, under what conditions, what actions agents can take — in a structured format that AI agents can reason about, not just read.

It is served at `/.well-known/agent.json` on any domain.

Think of it as:
- **Schema.org** → for search engines to understand products
- **FIBO** → for regulators to reason about financial instruments
- **ACM** → for agents to discover, compare and transact with businesses

---

## The Problem

Human marketing was built for human perception.

> *"This sofa feels like resting on the clouds — velvety and warm."*

An AI agent executing the directive *"buy a comfortable sofa for someone with back pain who likes warmth"* cannot reason from that sentence. It needs structured, matchable attributes:

```json
{
  "material": "velvet",
  "thermal_retention": "high",
  "firmness": 3,
  "lumbar_support": true,
  "sensation_tags": ["cozy", "warm", "soft"]
}
```

ACM provides the standard for expressing that structure.

---

## The Architecture

ACM operates across two parallel webs on the same domain:

```
same DNS: yourbusiness.com
│
├── Human web (HTTP)
│   → Indexed by Google, scraped by crawlers
│   → HTML, CSS, images — for humans
│
└── Agent web (ACM + Blockchain)
    → Discovered via DNS TXT record
    → NOT indexed by normal scrapers
    → Immutable, signed, verifiable
    → Rules cannot change post-commitment
```

**Gateway — DNS TXT record:**
```
_agent.yourbusiness.com = ipfs://QmHash... | contract:0x...
```

---

## The Spec — v0.1

Served at `/.well-known/agent.json`:

```json
{
  "acm_version": "0.1",

  "business": {
    "name": "Your Company",
    "description": "Concise description for the agent to understand who you are",
    "categories": ["restaurant", "mexican food"],
    "language": "en-US",
    "currency": "USD"
  },

  "catalog": [{
    "id": "product-001",
    "name": "Product or service name",
    "price": 120.00,
    "unit": "per_person",
    "availability": "available",
    "purchase_endpoint": "https://yourcompany.com/api/agent/order"
  }],

  "transaction": {
    "methods": ["card", "transfer", "crypto"],
    "endpoint": "https://yourcompany.com/api/agent/order",
    "escrow": {
      "enabled": true,
      "release_condition": "delivery_confirmed",
      "smart_contract": "0x..."
    }
  },

  "loyalty": {
    "program": true,
    "collateral": {
      "description": "Lock funds to guarantee purchase commitment",
      "commitments": [{
        "id": "buy-3x",
        "description": "Buy 3 times in 30 days and get 15% discount",
        "required_purchases": 3,
        "window_days": 30,
        "reward": "15%_discount",
        "collateral_amount": 50,
        "collateral_currency": "USD",
        "smart_contract": "0x..."
      }]
    }
  },

  "subscriptions": {
    "available": true,
    "plans": [{
      "id": "monthly-pro",
      "price": 29.00,
      "interval": "monthly",
      "auto_renew": true,
      "cancel_condition": "any_time",
      "agent_managed": true
    }]
  },

  "volume_commitments": {
    "available": true,
    "tiers": [{
      "units_per_month": 100,
      "unit_price": 8.00,
      "standard_price": 12.00,
      "contract_duration_months": 6,
      "smart_contract": "0x..."
    }]
  },

  "micropayments": {
    "available": true,
    "models": [
      { "id": "per_minute", "rate": 0.25, "currency": "USD" },
      { "id": "per_action", "rate": 0.05, "currency": "USD" },
      { "id": "per_token",  "rate": 0.001, "currency": "USD" }
    ],
    "payment_channel": "lightning_network"
  },

  "access_control": {
    "nft_membership": {
      "enabled": true,
      "contract": "0x...",
      "chain": "polygon",
      "benefit": "preferred_price_20%"
    }
  },

  "conditional_payments": {
    "available": true,
    "conditions": [
      { "trigger": "sla_met",      "action": "release_payment_100%" },
      { "trigger": "sla_breached", "action": "automatic_refund" },
      { "trigger": "rating_gte_4", "action": "release_payment_100%" }
    ],
    "oracle": "https://yourcompany.com/api/agent/verify"
  },

  "collective_buying": {
    "dao_enabled": true,
    "min_agents": 10,
    "group_discount": "25%",
    "coordination_contract": "0x...",
    "window_hours": 48
  },

  "agent_instructions": "I accept bookings with 24h notice. I verify NFT before applying preferred pricing. Micropayments via Lightning. For agent groups (DAO), use /api/agent/collective."
}
```

---

## Roadmap

| Version | What it adds |
|---|---|
| **v0.1** (today) | Readable JSON — discovery, catalog, basic transactions |
| **v0.2** (next) | Semantic ontology — agents reason relationships, not just read data |
| **v1.0** (horizon) | Smart contract collateral — cryptographic commitments between agent and merchant |

---

## Compatibility

ACM is designed to be compatible with:

- **[MCP (Model Context Protocol)](https://modelcontextprotocol.io)** by Anthropic — ACM is the content; MCP is the pipe. An ACM-ready business can expose its ontology via an MCP server.
- **RDF / OWL** — ACM v0.2 will adopt semantic web principles for richer reasoning
- **Schema.org** — ACM extends product schema with agent-specific fields
- **HTTP / HTTPS** — no infrastructure changes required; same DNS, same domain

---

## Why ACM matters for merchants

Agents will learn to prefer businesses with **stable, verifiable rules**. A merchant that silently changes pricing or loyalty terms after an agent has committed will be penalized — not by humans, but by the agents themselves.

**Define your rules now. Merchants who commit early will have structural advantage for decades.**

---

## Contributing

This is an open standard. Contributions, proposals and critiques are welcome.

- Open an [issue](https://github.com/lfayalan/agent-commerce-manifest/issues) to propose changes
- Submit a PR to contribute to the spec
- Read the full manifesto at [no-gui.com/manifiesto](https://no-gui.com/manifiesto)

---

## License

MIT — free to use, implement and extend.

---

*ACM is proposed and maintained by [No GUI](https://no-gui.com) — the consultancy preparing brands for the agent economy.*
