# Initiative — New Business Models (NBM)

| Field | Value |
|---|---|
| Slug | `nbm-new-business-models` |
| Status | Discovery — initialisation |
| Discovery lead | Christophe |
| Product group | Demand Digital |
| Impacted products | To be confirmed (potentially all — see [product map](../../../docs/context/02-products/product-map.md)) |
| Other product groups | To identify |
| Shared context | [docs/context](../../../docs/context/README.md) |

## Starting point (facts)

- Decathlon's supply chain and the Demand Digital products are designed for a **single integrated-retailer business model**.
- **One by 30** calls for diversification through new business models; some are already addressed, **not industrialised nor scalable**.
- Group vision: *Enable S&OP by aligning multi-dimensional forecast and inventory planning through a unified experience to optimise inbound flow management.*
- Supply Chain Blueprint 2030 is **not finalised** — any dependency on it is a hypothesis.

## Problem statement

*To be formalised — first objective of the discovery.*

## Related initiatives — Wholesale / Resell

The two workstreams below are distinct initiatives. The Business PO-flag approach is not part of the SAP Scheduling Agreement POC, and no dependency between them is assumed.

| Initiative | Scope | Working documents |
|---|---|---|
| [SAP Scheduling Agreement POC](../sap-scheduling-agreement-poc/README.md) | Digital proposal to assess a Wholesale commitment flow with standard SAP Contracts and Scheduling Agreements; fit/gap is not yet decided. | [POC spec](../../specs/spec-poc-commitment-process-sap/SPEC.md) |
| [Wholesale Demand & Inventory](../wholesale-demand-inventory/README.md) | Business work on planning inputs and the in-season Wholesale PO-flag approach, including the downstream synchronization gap. | [A4 business document](../wholesale-demand-inventory/research/a4-process-demand-inventory-management.md) |

## Folder layout

| Path | Content |
|---|---|
| `research/` | Deep-recon outputs, interviews, as-is analyses |
| `brief.md` | Problem / opportunity brief (product brief or PRFAQ) |
| `../../specs/spec-<slug>/` | Canonical BMad specification |
| `decisions.md` | Cross-product decisions log |
| `handoff/<product>.md` | What each product project must take over |

## Next steps

1. Frame the problem: `bmad-forge-idea` and/or `bmad-deep-recon` (type `domain`).
2. Formalise: `bmad-product-brief` or `bmad-prfaq` → `brief.md`.
