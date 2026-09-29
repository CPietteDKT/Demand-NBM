# Initiative — Wholesale Demand & Inventory (Resell)

| Field | Value |
|---|---|
| Slug | `wholesale-demand-inventory` |
| Status | Business working initiative — discovery |
| Product group | Demand Digital |
| Parent portfolio | [New Business Models](../nbm-new-business-models/README.md) |
| Business process | Wholesale / Resell planning inputs across horizons and in-season PO handling |

## Current understanding

- Wholesale Resell quantities are entered in `PQZD` and `SSV` for anticipation.
- In season, Wholesale POs are flagged and excluded from the requirements calculation, but the approach does not work end to end because downstream synchronization is missing.
- The A4 working document also describes To-Be proposals; these are not automatically validated decisions.

## Scope boundary

This Business initiative is separate from the Digital [SAP Scheduling Agreement POC](../sap-scheduling-agreement-poc/README.md). The two initiatives describe different approaches; no dependency or combined solution is assumed.

## Working documents

- [A4 Demand & Inventory Management — Business working document](./research/a4-process-demand-inventory-management.md)

## Open point

The A4 document classifies PO exclusion in the MRP calculation as a To-Be evolution, while the Business clarification describes a current in-season approach that fails because downstream synchronization is missing. Reconcile these descriptions and identify the missing synchronization before treating the process state as settled.
