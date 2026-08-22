# GuestGraph

**The open-source guest identity graph for hospitality.** → [**guestgraph.io**](https://guestgraph.io)

Guest data lives scattered across the PMS, POS, booking engine, loyalty program, wifi portal, and review platforms — each with its own keys and its own version of the truth. GuestGraph resolves those scattered records into one unified, explainable golden profile per guest: the guest graph.

## 🧭 Where to start

| Repository | What it is |
|---|---|
| [**engine**](https://github.com/guestgraph/engine) | The core: identity resolution engine, guest graph, REST API |
| [**talks**](https://github.com/guestgraph/talks) | Talks about it — start with the [10-minute introduction](https://guestgraph.io/talks/intro/) |
| [**guestgraph.github.io**](https://github.com/guestgraph/engine.github.io) | The site at [guestgraph.io](https://guestgraph.io) — landing page and logo |

**New here?** The [10-minute introduction](https://guestgraph.io/talks/intro/) is the
fastest way in: why a returning guest looks like five strangers, what it costs to merge them
wrongly, and how every decision stays explainable and reversible. DE · EN.

## 🧱 Principles

- **Source records are immutable** — the golden profile is derived and can always be recomputed; corrections arrive as new records, never as edits
- **Every merge is explainable and reversible** — identity resolution you can audit and trust
- **Tenant-scoped from day one** — one instance serves many brands, properties, or customers
- **API-first** — everything the engine can do is reachable over the REST API
- **Apache 2.0** — the core is and will remain open source

Matching is layered by confidence: shared strong identifiers merge outright, probabilistic
scoring only merges above a threshold each tenant chooses, and everything else queues for a
human whose decisions stick. Automatic fuzzy merging ships **off** —
[how matching decides →](https://github.com/guestgraph/engine/blob/main/docs/matching.md)

## 🗺️ Where we are

Identity resolution — deterministic and probabilistic — and the guest timeline are built.
Connectors for real PMS, POS, and booking systems are next.

The full roadmap, and what each phase actually delivered, lives with the code:
[**roadmap →**](https://github.com/guestgraph/engine#roadmap)

[guestgraph.io](https://guestgraph.io) is the home page. Managed hosting, API, and MCP services
are planned there; the core stays open source either way.

---

*Built spec-first in the open. Early days — star the [core repo](https://github.com/guestgraph/engine) to follow along.*
