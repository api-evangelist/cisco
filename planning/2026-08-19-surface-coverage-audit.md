# Cisco Product Surface vs. API Evangelist Coverage — Audit
Date: 2026-08-19 · Author: Kin Lane / API Evangelist
Lens: APIs.io catalog + apievangelist.com profile + Kin Score 0.11.0

## 1. What we hold today

25 repos across `all/*` carry Cisco or a Cisco-acquired brand. Scores as of the 2026-08-17 rebuild:

| repo | score | band | contracts | note |
|---|---|---|---|---|
| cisco | 54.7 | developing | 0 own (7 quarantined) | parent index, 8 named APIs |
| cisco-webex | 63.2 | strong | 9 harvested, 42 quarantined | 2,053 ops |
| cisco-expressway | 56.9 | strong | 16 | 0% provenance markers |
| cisco-voice-portal | 56.2 | strong | 23 | 0% provenance markers |
| webex | 51.6 | developing | 178 | **DUPLICATE of cisco-webex**, 1,931 ops (staler) |
| cisco-webex-meetings | 48.9 | developing | 4 | product, not company |
| cisco-systems | 45.2 | developing | 1 | **DUPLICATE of cisco** |
| cisco-secure-client | 45.1 | developing | 6 | product, not company |
| cisco-nexus | 43.5 | developing | 5 | |
| cisco-hardware | 41.7 | thin | 7 | not a product |
| cisco-directory-connector | 41.3 | thin | 3 | **DUPLICATE pair** |
| cisco-directory-connectors | 36.5 | thin | 2 | **DUPLICATE pair** |
| cisco-control-hub | 32.2 | thin | 7 | |
| cisco-meraki | 29.9 | thin | 16 | 992 real ops upstream; we hold 957 (v1.72.0 vs 1.73.0) |
| cisco-collaboration-hybrid-solutions | 28.9 | thin | 6 | |
| cisco-spark | 5.7 | minimal | 0 | dead brand since 2018 |
| splunk | 66.7 | exemplar | 3 | 14 named APIs, 1 AE-written spec, no markers |
| appdynamics | 45.8 | developing | 25 | 0% markers |
| isovalent | 46.1 | developing | 9 | |
| signalfx | 35.3 | thin | 0 | = Splunk Observability |
| duo-security | 30.5 | thin | 7 | 0% markers |
| victorops | 29.8 | thin | 0 | = Splunk On-Call |
| valtix | 29.4 | thin | 0 | = Multicloud Defense |
| kenna-security | 25.1 | emerging | 0 | folded into Vulnerability Management |
| epsagon / banzai / acacia / talos / broadsoft | 25–40 | thin | 0–4 | acquisitions, unlinked to parent |

**Structural problems, independent of score:**
- The Cisco family is a flat list of 25 unrelated entries. Nothing says Meraki, Webex, Splunk, ThousandEyes and Duo are one company. There is no parent→subsidiary→product relationship anywhere in the data.
- Four of the entries are **not companies or products**: `cisco-hardware`, `cisco-collaboration-hybrid-solutions`, `cisco-directory-connector(s)`, `cisco-secure-client`. They are documentation categories that got profiled as providers.
- Three **confirmed duplicate pairs**: `cisco`/`cisco-systems`, `cisco-webex`/`webex`, `cisco-directory-connector`/`cisco-directory-connectors`. Each pair carries a different score for the same thing.
- **17 of 25 repos have 0% provenance marker coverage** on their contracts. Per the 2026-07-31 finding, unmarked derived specs are graded as first-party and inflate contract_quality. Every "strong" band above except cisco-webex is suspect.

## 2. What Cisco actually publishes (probed 2026-08-19)

### Confirmed first-party machine-readable, NOT in the catalog

| surface | evidence | scale |
|---|---|---|
| **IOS-XE OpenAPI/Swagger** | `github.com/CiscoDevNet/cisco-ios-xe-openapi-swagger` (upd 2026-07-30) | **979 swagger docs** for 26.1.1 alone, across 8 model families (native-config, oper, cfg, ietf, openconfig, mib, rpc, other); 5 releases (17.9.x → 26.1.1) = **4,477 spec documents**; plus YANG trees, telemetry index, Postman collections |
| **Meraki Secure Connect** | `github.com/meraki/secure-connect-openapi` | `secure_connect_oas_beta.json` |
| **Crosswork** | `github.com/CiscoDevNet/crosswork-openapi-spec` | CDG + CNC swagger sets, multiple versions |
| **PSIRT openVuln** | `github.com/CiscoPSIRT/openVulnAPI` | `swagger/openVulnAPIOAS_3_0_3.yaml` — OAS 3.0.3, first-party |
| **AGNTCY (Outshift)** | `github.com/agntcy` — 53 repos, all active this week | OASF, ACP, SLIM, DIR, Identity **specifications**; Cisco-led open agent-interop stack |
| **MCP Toolkit** | `cisco-open/mcptoolkit-{contract,test,editor,mock}` (upd 2026-07-30) | Cisco is authoring an **MCP Description document** format + lifecycle tooling |
| **Foundry Security Spec** | `CiscoDevNet/foundry-security-spec` (upd 2026-08-18) | open spec for agentic-AI security evaluation |
| **MCP servers** | 18 repos across CiscoDevNet/cisco-open/splunk | Meraki (official), Webex (official), ThousandEyes (official), Splunk (official), XDR, FMC, ACI, SCC, Secure Access, ESA, RADKit, Nexus Dashboard, DevNet content search |

### Confirmed live agent endpoints
- `https://devnet.cisco.com/v1/foundation-search-mcp/mcp` — answers `tools/list` **anonymously**. Still true.
- `https://mcp.webexapis.com/mcp/webex-messaging` — OAuth-gated, serves RFC 9728 `/.well-known/oauth-protected-resource` with 9 scopes (`spark:mcp`, `spark:messages_write`, …). Still true.

### Confirmed absent (real 404s, falsifiable)
`developer.cisco.com`, `developer.webex.com`, `developer.thousandeyes.com`, `docs.agntcy.org`, `intersight.com` — no `llms.txt`, no `/.well-known/api-catalog`, no `/.well-known/security.txt`.

### Machine-invisible (the sharpest finding)
`dev.splunk.com` returns **HTTP 200 with an identical 6,638-byte Next.js shell for every path** — including `/llms.txt`, `/openapi.json`, `/.well-known/security.txt`, and a nonsense control path. It is a soft-404 farm. Splunk Observability Cloud publishes **48 OpenAPI specs** (`apm_service_topology`, `signalflow`, `detectors`, `synthetics_*`, `slo`, …) whose reference pages render at 95–150KB for humans but expose **no fetchable spec file anywhere**. Splunk's entire observability contract surface is public to people and invisible to machines.

### Named in `all/cisco/apis.yml` but with no repo and no contract
Catalyst Center, ACI/APIC, ISE, Intersight, Catalyst SD-WAN (vManage), ThousandEyes.

### Product lines with no representation at all
Umbrella / Secure Access, Secure Firewall (FMC/cdFMC), Secure Endpoint, XDR, Security Cloud Control, Email Security (ESA/CES), Talos Intelligence, AI Defense, Panoptica, Cisco Spaces, IoT Control Center (Jasper), Nexus Hyperfabric, UCS/HyperFlex, NSO, CML, Smart Licensing, Cisco Support APIs (EoX, Serial2Info, Bug, Case), Commerce (CCW), Silicon One, Motific, Splunk SOAR / ITSI / ES / Attack Analyzer / Edge Processor, Webex Contact Center as its own entry, BroadWorks.

## 3. The honest headline

Cisco's real machine-readable footprint is one of the largest in the catalog — **~4,500 IOS-XE spec documents, 992 Meraki operations, 2,053 Webex operations, 48 Splunk Observability specs, 18 MCP servers, and an entire open agent-interop standards body (AGNTCY)**. What APIs.io currently shows is 25 mostly-unrelated entries scoring 5.7–66.7, built substantially on API Evangelist's own writing rather than Cisco's.

The gap is not Cisco's. It is ours. And the correct read of it is a compliment to Cisco with a specific ask attached: *you publish more machine-readable surface than almost anyone, and almost none of it is discoverable — no catalog, no llms.txt, no index tying Meraki to Webex to Splunk to ThousandEyes.*
