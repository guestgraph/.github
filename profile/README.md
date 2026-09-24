# GuestGraph

**The open-source guest identity graph for hospitality.** → [**guestgraph.io**](https://guestgraph.io)

Guest data lives scattered across the PMS, POS, booking engine, loyalty program, wifi portal, and review platforms — each with its own keys and its own version of the truth. GuestGraph resolves those scattered records into one unified, explainable golden profile per guest: the guest graph.

## 🧭 Where to start

| Repository | What it is |
| --- | --- |
| [**engine**](https://github.com/guestgraph/engine) | The core: identity resolution engine, guest graph, REST API |
| [**connector-apaleo**](https://github.com/guestgraph/connector-apaleo) | The first connector: reservations and bookings from Apaleo into the guest graph, a client of the engine's API |
| [**service-conventions**](https://github.com/guestgraph/service-conventions) | The rules every service is held to by check: one parent build, one error shape, the architecture tests and the workflow, vendored by each service at a pinned release |
| [**guestgraph.github.io**](https://github.com/guestgraph/guestgraph.github.io) | The site at [guestgraph.io](https://guestgraph.io) — landing page, the [model](https://guestgraph.io/model/) and its team, principles and surfaces, the API, billing, privacy, the [talks](https://guestgraph.io/talks/), and a chat that answers from the model |
| [**mental-model**](https://github.com/guestgraph/mental-model) | GuestGraph itself, described in [CompanyGraph](https://companygraph.io)'s vocabulary: vision, values, products, concepts and how the work is done |
| [**mcp-guestgraph-io**](https://github.com/guestgraph/mcp-guestgraph-io) | [mcp.guestgraph.io](https://mcp.guestgraph.io), that model served to agents over MCP, and the chat beside it |

**New here?** The [twelve-minute introduction](https://guestgraph.io/talks/intro/) is the fastest way in: why a returning guest looks like five strangers, what it costs to merge them wrongly, and how every decision stays explainable and reversible. DE · EN.

## 🧩 What runs

Two services, two schemas, one direction. A connector calls the engine and never the other way round, so a deployment can run the engine alone, or run several connectors against one engine.

```mermaid
flowchart TB
    CLIENT(["API client"])
    OPERATOR(["operator"])

    subgraph apaleo["Apaleo"]
        AID["identity.apaleo.com"]
        AAPI["api.apaleo.com"]
        AHOOK["webhook.apaleo.com"]
    end

    CONN["<b>connector-apaleo</b><br/>port 8081"]
    ENG["<b>engine</b><br/>port 8080"]

    CDB[("PostgreSQL<br/>schema apaleo_connector")]
    EDB[("PostgreSQL<br/>schema engine")]

    OPERATOR -- "operations · bearer token" --> CONN
    CLIENT -- "REST · X-API-Key" --> ENG

    CONN -- "token · OAuth client credentials" --> AID
    CONN -- "reservations and bookings" --> AAPI
    CONN -- "subscribe, unsubscribe" --> AHOOK
    AHOOK -. "delivery · secret in the path" .-> CONN
    CONN -- "records and guests · X-API-Key" --> ENG

    CONN --- CDB
    ENG --- EDB
```

The engine holds the guest graph and serves the API every other component is a client of; it calls nothing outward. A connector reaches one external system and submits what it finds. Each service owns its schema and connects as a role that sees nothing else, so one database or two is a deployment choice. What each path is and what guards it, in the [engine](https://github.com/guestgraph/engine#readme) and the [connector](https://github.com/guestgraph/connector-apaleo#readme) READMEs.

Beside the product runs a second, smaller thing: GuestGraph's own model, the project described in [CompanyGraph](https://companygraph.io)'s vocabulary. It holds no guest and no hotel's data, and nothing in it reaches the engine.

```mermaid
flowchart TB
    subgraph gg["guestgraph"]
        GGMM["<b>mental-model</b><br/>GuestGraph, described<br/>in CompanyGraph's vocabulary"]
        SITE["<b>guestgraph.io</b><br/>landing, the model pages,<br/>the talk, the chat button"]
        MCPGG["<b>mcp.guestgraph.io</b><br/>the model over MCP,<br/>and chat.guestgraph.io"]
    end

    subgraph cg["companygraph"]
        MM["<b>meta-model</b><br/>the vocabulary"]
        SRV["<b>mcp-server</b> · <b>chat-server</b>"]
    end

    MM -- "core vendored at a release" --> GGMM
    GGMM -- "pinned by commit · builds the model pages" --> SITE
    GGMM -- "pinned by commit · parsed into a snapshot" --> MCPGG
    SRV -- "pinned by tag" --> MCPGG
    SITE -. "the chat button asks" .-> MCPGG
```

An agent reaches the model at `https://mcp.guestgraph.io/mcp`, listed in the MCP Registry as `io.guestgraph/mental-model`, and a visitor asks it in their own words from the button at the foot of every page of guestgraph.io. How it is deployed is in [mcp-guestgraph-io](https://github.com/guestgraph/mcp-guestgraph-io#readme).

## 🧱 Principles

- **Source records are immutable** — the golden profile is derived and can always be recomputed; corrections arrive as new records, never as edits
- **Every merge is explainable and reversible** — identity resolution you can audit and trust
- **Tenant-scoped from day one** — one instance serves many brands, properties, or customers
- **API-first** — everything the engine can do is reachable over the REST API
- **Apache 2.0** — the core is and will remain open source

Matching is layered by confidence: shared strong identifiers merge outright, probabilistic scoring only merges above a threshold each tenant chooses, and everything else queues for a human whose decisions stick. Automatic fuzzy merging ships **off** — [how matching decides →](https://github.com/guestgraph/engine/blob/main/docs/matching.md)

## 🗺️ Where we are

1. ✅ **Core** — identity resolution engine (deterministic, probabilistic-ready), guest graph, REST API
2. ✅ **Probabilistic matching** — fuzzy/ML resolution behind the same strategy interface, with review queue
3. ✅ **Timeline** — per-guest business-object associations, attributed decisions
4. ✅ **Retired guest ids** — a stored guest id resolves to the current guest after merges and splits
5. ✅ **Connectors** — ingest from real PMS/POS/booking systems; the first, for Apaleo, lives in [connector-apaleo](https://github.com/guestgraph/connector-apaleo) and brings reservations and bookings into the graph
6. ✅ **One schema per service** — the engine owns the schema `engine` and connects as a role that sees nothing else, as the connector does with its own
7. ✅ **Service conventions** — every service has the same shape by check, not by hand, from [service-conventions](https://github.com/guestgraph/service-conventions) at a pinned release
8. ✅ **Shared runtime** — one error shape and the few classes every service carries, vendored as source from the same release
9. ✅ **Removing a subscription** — an operator takes a connection's Apaleo webhook subscription away and puts it back, so tearing a deployment down leaves nothing posting to a dead address
10. ✅ **GuestGraph's own model** — [the project described](https://github.com/guestgraph/mental-model) in CompanyGraph's vocabulary: vision, values, strategies, products, the words it means something exact by and how the work is done, drawn on [guestgraph.io/model](https://guestgraph.io/model/), served to agents over MCP and answered from in the chat

Connectors for more PMS, POS, and booking systems are next. What a phase decided, and the requirements waiting for a later one, are in the engine's [roadmap notes](https://github.com/guestgraph/engine/blob/main/docs/roadmap-notes.md), which feed each slice's specification.

[guestgraph.io](https://guestgraph.io) is the home page. Managed hosting, a console and MCP access for agents to a hotel's own guest graph are planned there; the core stays open source either way.

---

*Built spec-first in the open. Early days — star the [core repo](https://github.com/guestgraph/engine) to follow along.*
