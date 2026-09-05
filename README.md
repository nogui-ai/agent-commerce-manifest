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

---

## GS1 Digital Link Compatibility

ACM is designed to be the agent layer on top of **GS1 Digital Link** — the successor to the traditional barcode, becoming a global standard in 2027.

### What is GS1 Digital Link?

GS1 Digital Link replaces the traditional barcode number with a URL. That URL carries structured product data: origin, ingredients, certifications, supply chain history, batch tracking, and more. It is the standard used by Walmart, Amazon, and every major retailer globally.

### The gap GS1 leaves

GS1 Digital Link was designed for human-facing web pages — a URL that opens a product page with information for consumers. It was not designed for agent commerce: agents cannot transact, compare, or reason from a product page.

### ACM fills that gap

ACM is the agent-readable layer on top of GS1 Digital Link. The **GS1 → ACM Translator** converts GS1 product data into an executable ACM that agents can reason about and transact with.

```
Physical product barcode scan
  → GS1 Digital Link (product data URL)
  → GS1 → ACM Translator
  → ACM of the product (agent-executable):
    {
      "entity_type": "physical_product",
      "gs1_gtin": "00012345678905",
      "gs1_link": "https://id.gs1.org/01/00012345678905",
      "origin": { "country": "Mexico", "region": "Guanajuato", "producer": "Rancho El Fresón" },
      "certifications": ["USDA Organic", "Fair Trade"],
      "harvest_date": "2026-09-03",
      "cold_chain": { "verified": true, "checkpoints": 3 },
      "purchase_endpoint": "https://supplier.com/api/agent/order"
    }
  → Agent verifies, purchases, logs
```

### Mapping table: GS1 → ACM

| GS1 Field | ACM Field | Notes |
|---|---|---|
| GTIN | `catalog[].id` | Global Trade Item Number |
| GLN | `business.location_id` | Global Location Number |
| Batch/Lot | `catalog[].batch` | Traceability |
| Best Before | `catalog[].expiry` | ISO 8601 date |
| Country of Origin | `business.origin.country` | |
| Certifications | `catalog[].certifications` | Array of strings |
| Digital Link URL | `catalog[].gs1_link` | Source of truth link |

### ACM fields added for physical products

```json
{
  "entity_type": "physical_product",
  "gs1_gtin": "string — Global Trade Item Number",
  "gs1_link": "string — GS1 Digital Link URL",
  "origin": {
    "country": "string",
    "region": "string",
    "producer": "string",
    "coordinates": "optional lat/long"
  },
  "certifications": ["array of certification strings"],
  "batch": "string — lot or batch number",
  "harvest_date": "ISO 8601 date — for perishables",
  "expiry": "ISO 8601 date",
  "cold_chain": {
    "required": "boolean",
    "verified": "boolean",
    "checkpoints": "integer"
  }
}
```

### Roadmap

- **ACM v0.1** (now) — digital services and businesses
- **ACM v0.2** — physical products with GS1 Digital Link mapping
- **ACM v1.0** — full supply chain: raw materials → manufacturer → distributor → retailer → consumer

### Why this matters

Every physical product in the world is going to have a GS1 Digital Link by 2027. Each of those products will need an agent-readable representation. ACM is the standard that makes that possible — and the GS1 → ACM Translator is the bridge between the physical supply chain and the agent economy.

