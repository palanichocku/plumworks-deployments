# Car Doc legacy customer recovery review

Generated from a read-only audit on 2026-07-19. This recovery package is dry-run-only and does not authorize customer or invoice writes.

## Summary

| Recovery path | Customers | Orders |
|---|---:|---:|
| Existing-customer import-time aliases | 6 | 9 |
| Historical customer creation candidates | 12 | 56 |
| Unresolved, approved to remain skipped | — | 1 |
| Total | 18 | 66 |

- Recoverable historical financial impact: **$22,718.69**, entirely before 2025.
- Calendar year 2025 impact: **$0.00 / 0 orders**.
- January-June 2026 impact: **$0.00 / 0 orders**.
- RO 18181 is the sole unresolved order and has a **$0.00** total.

## Review requirements

All six alias entries and all twelve customer-creation entries have `reviewStatus: "approved"`, approving the 65 recoverable orders for a separately authorized future write operation. The manifest remains a crosswalk and evidence record; this approval does not itself execute recovery.

The six aliases must never replace an operational customer's current `legacy_custno`. They are alternate legacy identifiers scoped to the listed repair orders.

Special attention is required for:

- **87606676 / GERARDI K:** the raw `Cust.DBF` name is blank; the proposed name comes from repeated, consistent AR records.
- **87605435:** no real name is present. `Historical Unknown Customer 87605435` is intentionally synthetic and non-identifying.
- **87604561 / CORBIN:** source evidence is limited to legacy ID, name, and vehicle ownership.
- **87603794 / THOMAS** and **87604081 / PATEL:** common names; review the exact legacy ID, address, and vehicle evidence together.
- **87606096:** AR contains both `TROY TECH COMMONS` and `MOUND TECH COMMONS` under the same legacy ID.
- Older phone and city fields that are visibly truncated are preserved exactly. Missing digits, state values, names, and address components were not inferred.

RO 18181 is marked `approved-skip` because it has no name or phone, has a malformed vehicle reference of `0`, lacks an unambiguous owner, and carries no financial value.

## Validation boundary

The companion validator performs read-only checks for manifest structure, operational customer existence, alias uniqueness, creation collisions, raw AR customer/order consistency, invoice-date periods, and the 66-order historical total. It contains no create, update, delete, upsert, transaction, or raw execution operation.
