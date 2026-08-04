# Quarantined scaffold — not published by Cisco

The OpenAPI documents in this directory were **written by API Evangelist**, modelled from Cisco's
public Meraki documentation. They were never published by Cisco and must not be presented as Cisco
artifacts, cited as evidence of what Cisco ships, or credited in a Kin Score.

They were moved here on **2026-07-31**.

## Why they were quarantined

`cisco-meraki-api.yaml` declared its own authorship honestly — `x-generated-from: documentation`,
`x-last-validated: '2026-04-18'` — and the rubric graded it accordingly (`contracts: 4 derived of 4,
100%`). It modelled **5 operations**.

Cisco publishes the real thing:

> https://github.com/meraki/openapi — 670 paths / 957 operations, v1.72.0
> https://github.com/webex/webex-openapi-specs — 1,382 paths / 2,053 operations across 9 documents

`all/cisco` is an **Index**-type repo: the umbrella record for Cisco as a company. It should point at
the product-line repos (`cisco-meraki`, `cisco-webex`) where those harvested contracts now live,
rather than carry a modelled contract of its own.

## Contents

`cisco-meraki-api.yaml` (5 operations, hand-modelled) plus the 4 per-tag files `refine-openapis`
split out of it.

## Do not

- Restore these to `_original/`.
- Re-run `refine-openapis` against them.
- Point `apis.yml` at them.
