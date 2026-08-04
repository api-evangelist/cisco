# Quarantined — derived from a quarantined spec

`cisco-agentic-access.yml` classified 5 operations read from
`openapi/cisco-meraki-api.yaml`, a specification **API Evangelist wrote** and which was quarantined
to `../../openapi/_scaffold/` on 2026-07-31. An execution contract derived from a modelled spec
describes an API that does not exist as described, so it was withdrawn rather than re-pointed.

`all/cisco` is an **Index** repo — the umbrella record for Cisco as a company. It carries no
contracts of its own. The real agentic-access contracts, regenerated from Cisco's published
OpenAPI, live with the product lines:

| repo | operations classified |
|---|---|
| `all/cisco-meraki/agentic-access/` | 957 |
| `all/cisco-webex/agentic-access/`  | 2,053 |

Removing this artifact will cost `all/cisco` points on the `agentic_access` agent-readiness
dimension. That is the correct outcome: the points were resting on a modelled spec.
