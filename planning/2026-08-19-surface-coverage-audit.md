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

---

# Part 2 — What was built (2026-08-19)

## 4. The soft-404 pattern across the Cisco family

Four Cisco-owned developer hosts answer **HTTP 200 with a byte-identical HTML shell for
every path**, including invented control paths. Each was verified with a nonsense-path probe:

| host | status for `/openapi.json` | status for an invented path | identical body |
|---|---|---|---|
| `dev.splunk.com` | 200 | 200 | 6,638 bytes |
| `intersight.com` | 200 | 200 | 3,784 bytes |
| `api.duosecurity.com` | 200 | 200 | 130,977 bytes |
| `docs.appdynamics.com` | 200 | 200 | 122,628 bytes |

This is the most dangerous failure mode in the catalog. A harvester that trusts a 200 will
record four OpenAPI documents that do not exist, and the Kin Score will credit them as
first-party. It is also, from Cisco's side, the single cheapest thing to fix: return a 404.

By contrast `developer.cisco.com` returns **real, falsifiable 404s** for `llms.txt` and
`/.well-known/api-catalog`. Absence there is honest. That distinction is worth making to them
directly — one part of Cisco is doing this correctly and the other is not.

## 5. Contracts harvested

| repo | source | result |
|---|---|---|
| `cisco-meraki` | `github.com/meraki/openapi` | refreshed **v1.72.0 → v1.73.0**, 992 operations (+35) |
| `cisco-meraki` | `github.com/meraki/secure-connect-openapi` | Secure Connect, 31 operations — **new to the catalog** |
| `webex` | `github.com/webex/webex-openapi-specs` | 9 documents refreshed, 1,385 paths / **2,056 operations** |
| `cisco-psirt` | `github.com/CiscoPSIRT/openVulnAPI` | OAS 3.0.3, 30 operations — **new** |
| `cisco-crosswork` | `github.com/CiscoDevNet/crosswork-openapi-spec` | **33 specs / 428 operations** across CDG, CNC, COE, NCAHI, ZTP — **new** |

Every harvested document carries `info.x-provenance` (`method: harvested`, `first_party: true`)
plus `x-evidence` source URLs, and every per-tag split carries the same block with a
`derived_view` note and a `derived_from` filename. **Marker coverage is 100% on all four repos.**

One upstream defect found: `NCAHI/3.1APIs/auth.swagger.json` in Cisco's own public Crosswork
repository is **malformed JSON** — a trailing comma at line 147. The harvester refused it rather
than repairing it. Worth reporting back to them; it is a one-character fix in a file they publish.

## 6. The Meraki over-split, caught and reversed

Running the standard refine pass on Meraki produced **429 per-tag files carrying 4,162 operation
instances for 1,023 distinct operations — 4.07x duplication**. Meraki declares 411 distinct tags
but only 16 distinct *first* tags, and the first tags are the real product areas. Re-split by
first tag: **20 files, 1,023 operations, 1.00x duplication, 100% provenance coverage.**

This is a general engine finding, not a Cisco one. Any provider that tags an operation with a
product area *and* a resource *and* a capability will over-split the same way.

## 7. Derived specs marked, so they stop being credited in full

`build_provenance.py` records an unmarked spec as `unknown`, and `score.rb` credits `unknown`
**in full**. That is the 2026-07-31 defect restated: a spec API Evangelist wrote from a vendor's
HTML docs earns the vendor full `contract_quality` credit for craftsmanship it had no part in.

**121 specs across 14 Cisco-family repos** were marked `method: derived`, `first_party: false`,
each carrying the specific 2026-08-19 probe result that justifies the call — the four soft-404
findings above, or "served by each customer's own appliance", or a real 404.

Expect these scores to **fall** on the next rebuild. That is the correct outcome, and it is the
number we can defend in a room with Cisco.

## 8. Structure: the family is now one company

`ParentCompany` and `Subsidiary` were already registered in `properties.yml` and used by **zero**
repos across all/*. Cisco is the first real use. 34 repos now carry a `ParentCompany` pointer with
`x-relationship` (product | acquisition | initiative) and `x-acquired` year; `cisco` carries 27
`Subsidiary` entries, `webex` 3, `splunk` 4.

Four duplicates retired into `network/_data/retired.yml` (165 page redirects):

| retired | into | why |
|---|---|---|
| `cisco-webex` | `webex` | same product; `webex` had 4,604 built pages to 127 and is the domain-derived slug. The current provenance-stamped specs were ported to the survivor first. |
| `cisco-systems` | `cisco` | duplicate company index; all seven of its APIs are now the parent or separately profiled members |
| `cisco-directory-connectors` | `cisco-directory-connector` | plural/singular pair, no callable contract on either |
| `cisco-spark` | `webex` | dead brand — renamed Webex Teams in 2018, scored 5.7 |

123 unique blog posts were ported from `cisco-systems` into `cisco` before retirement.

## 9. Fifteen providers added

`thousandeyes` · `intersight` · `cisco-catalyst-center` · `cisco-aci` · `cisco-ise` ·
`cisco-catalyst-sdwan` · `cisco-umbrella` · `cisco-secure-firewall` · `cisco-xdr` ·
`cisco-psirt` · `cisco-support-apis` · `cisco-crosswork` · `agntcy` · `splunk-soar` ·
`splunk-observability`

Each carries an `x-contract-status` (`real` | `gated` | `soft404` | `on-prem` | `none` | `spec`)
and an `x-contract-note` recording what the 2026-08-19 probe actually found. **No entry claims a
contract API Evangelist could not fetch, and no entry has an AE-authored spec standing in for one.**

## 10. Still open

- **IOS-XE — the biggest contract surface in the catalog and still unprofiled.**
  `CiscoDevNet/cisco-ios-xe-openapi-swagger` carries **979 swagger documents for release 26.1.1
  alone**, across eight model families (native-config, oper, cfg, ietf, openconfig, mib, rpc,
  other), over five releases — roughly **4,477 spec documents**, plus YANG trees, a telemetry
  index and Postman collections. It needs its own splitting strategy (by model family, not by
  tag) and probably its own report.
- **Splunk's real number.** Splunk sits at 66.7 "exemplar" on three AE-authored specs, now marked
  derived. Its 48 Observability specs are unreachable. The rebuild will restate this.
- **The Cisco MCP estate is unprofiled** — 18 MCP servers across CiscoDevNet, cisco-open and
  splunk, plus the `cisco-open/mcptoolkit-*` suite in which Cisco is authoring an **MCP Description
  document format**. That is Cisco doing standards work on the agent tier and nobody has said so.
- **AGNTCY deserves the standards pipeline, not the company pipeline.** 53 active repos publishing
  OASF, DIR, SLIM and Identity specifications is a standards body in the shape of a GitHub org.

---

# Part 3 — Corrections. I was wrong about Cisco, and the error is instructive.

The enrichment wave (15 agents, 935 artifacts, zero failures) **overturned almost every
"no contract" verdict in Part 1**. My probes checked `developer.cisco.com` and each product's
own host. Cisco's specifications are not there. They are on **`pubhub.devnetcloud.com`**, the
DevNet documentation CDN, and on **`cdn.intersight.com`** — and they are enumerable from each
DevNet project's own `config.json` manifest.

## What Cisco actually publishes, verified

| repo | operations | source | verification |
|---|---:|---|---|
| `intersight` | **5,091** | `cdn.intersight.com` — 27.5MB master OpenAPI 3.0.2 + 11 per-service docs | SHA-256 byte match |
| `cisco-catalyst-sdwan` | **4,138** | DevNet CDN, per-operation OpenAPI 3.1.0 fragments (2,841 paths) | contact `vmanage@cisco.com` |
| `cisco-secure-firewall` | **1,833** | `CiscoDevNet/scc-public-api-docs` — 9.5MB cdFMC spec + 13 SCC specs | GitHub, first-party |
| `cisco-ise` | **1,247** | `pubhub.devnetcloud.com`, 103 docs enumerated from Cisco's own manifest | SHA-256 byte match |
| `cisco-crosswork` | 624 | `CiscoDevNet/crosswork-openapi-spec` | GitHub, first-party |
| `cisco-xdr` | 581 | `visibility.amp.cisco.com/iroh/*/swagger.json` + CTIA | real 404s on controls |
| `thousandeyes` | 326 | DevNet CDN (27 docs) | API host 401s; docs CDN is open |
| `cisco-umbrella` | 256 | DevNet CDN, 26 docs from Cisco's docs-nav config | SHA-256 byte match |
| `cisco-catalyst-center` | 185 | Cisco-published Assurance specs + MCP server w/ 516 tools | Cisco EULA/license blocks |
| `agntcy` | 106 | ACP, OASF Schema API, 2× Identity + 34 protobufs | `schema.oasf.outshift.com` callable |
| `splunk-observability` | 242 | extracted from the RSC payload of Splunk's own reference pages | **not first-party** |

**613 specifications, 14,659 operations, 100% provenance-marked** — 565 harvested first-party,
48 reconstructed. Add the pre-existing family and Cisco's catalogued surface is now roughly
**20,500 operations**.

`pubhub.devnetcloud.com` returns **real 404s** on invented paths. It is a trustworthy host. We
simply never looked at it.

## The correction that matters most

Part 1 said "the gap is not Cisco's, it is ours." That was right, and it was more right than I
knew. Cisco publishes **an order of magnitude more machine-readable surface than the catalog
credited**, and the reason we missed it is the reason their customers miss it:

**Cisco's specifications are not where anyone would look for them.** They are not on the product
host, not linked from `/.well-known/api-catalog` (there isn't one), not in an `llms.txt` (there
isn't one). They are on a documentation CDN, discoverable only by reading a JavaScript
documentation viewer's internal config manifest. A first-party OpenAPI that requires
reverse-engineering a docs SPA to locate is published in the letter and unpublished in the effect.

That is the finding to take to them, and it is a *good news* finding: **you already did the hard
part. 14,659 operations of it. The remaining work is an index and a 404.**

## Splunk Observability — the honest middle

The 48 Splunk Observability specs are Splunk's own OpenAPI objects, lifted out of the React
Server Component payload of Splunk's reference pages. The operations and schemas are Splunk's;
the assembly into standalone documents is ours. They are stamped `method: reconstructed`,
`first_party: false`, and grade to the derived floor. **Splunk gets no first-party credit for a
spec file it does not serve** — but the work is preserved and correctly labelled, and it is the
sharpest possible demonstration of what a soft-404 farm costs its own vendor.

## Defects found in Cisco's published artifacts

Reported, not repaired — repairing them would destroy the provenance.

- **860 of 1,490 ISE operations (58%) carry no `operationId`.** Codegen and agent tool-naming
  cannot bind to them.
- **30 of 69 legacy ISE Swagger 2.0 files contain literal TAB characters** and fail a strict YAML
  parse. They are stored exactly as served and are the reason 30 of 103 ISE documents could not
  be split.
- **95 of 103 ISE documents declare no `securitySchemes`**, though every ISE API requires HTTP Basic.
- **ISE `servers[]` leaks Cisco lab appliance addresses** — `https://10.56.60.25:443`,
  `https://iseui-vm11.cisco.com:443` — instead of the templated on-premises form.
- **`NCAHI/3.1APIs/auth.swagger.json` in the public Crosswork repo is malformed JSON** (trailing
  comma, line 147).
- **41.6% of Webex operationIds contain spaces** (780 of 1,876) while Meraki has 0 of 957 — an
  inconsistency inside Cisco's own portfolio that breaks codegen and agent tool naming.
- **240 deprecated Catalyst SD-WAN operations** and 515 distinct `x-roles-required` RBAC
  expressions are published but not summarized anywhere consumable.

## A defect in OUR pipeline, found by running it

The wave's agents wrote honest authorship markers under **`x-apievangelist-derivation`** — a key
`build_provenance.py` does not read. `score.rb` would have graded all 48 Splunk Observability
specs `unknown` and credited them **in full**. The pipeline was being honest in a dialect the
scorer does not speak. Corrected here by rewriting to canonical `x-provenance`; the pipeline
prompt itself still needs the fix, or every future wave recreates the gap.

---

# Part 4 — Retirement executed (2026-08-19)

Kin ran `all/0-working/cisco/retire-repos.sh`. Verified:

- **All four repos archived on GitHub** (`cisco-webex`, `cisco-systems`,
  `cisco-directory-connectors`, `cisco-spark` — `isArchived: true`).
- **All four local clones deleted.** This matters: `build-listing.py` enumerates `all/*`, so a
  retired slug keeps listing until the clone is gone.
- **Survivors intact** — `webex` 194 specs / 55 blogs, `cisco` 155 blogs (its own 32 plus the 123
  ported from `cisco-systems`), `cisco-directory-connector` 4 specs.
- **No dangling references.** No live family repo points a `ParentCompany`, `Subsidiary` or
  `x-parent` at a retired slug.

`build-listing.py` was re-run. The four retired slugs still have a `_providers/<slug>.md` page,
and the fifteen new providers do not yet have one — **both resolve on the next apis.io rebuild and
neither should be fixed by hand.** `PROVIDERS_DIR` is in `COLLECTION_DIRS`, so a full build wipes
and regenerates that directory from `all/*`: the retired slugs cannot come back (no clone) and the
new ones appear for the first time. `build_tombstones()` then emits the 165 redirects from
`network/_data/retired.yml`.

## Final state

**38 live Cisco-family repos · 947 specifications · 18,072 operations · 998 registered APIs ·
100% provenance marker coverage** — 778 harvested first-party, 121 derived, 48 reconstructed,
**zero unknown**. Network-wide marker coverage is 4.6%.

One late fix: `cisco-catalyst-center`'s 27 agent-written specs had bypassed the refine step and so
were never registered in `apis.yml` (2 entries for 27 specs). Refined, stamped and registered —
29 specs, 30 API entries, 185 operations. It was the only repo affected; a scan of the whole family
found no other spec/registration mismatch.

## What is genuinely left

1. **The apis.io rebuild** — nothing scores until then. Expect the fifteen new providers to enter
   high and the fourteen derived-marked repos to fall. Both are correct.
2. **IOS-XE** — ~4,477 spec documents across 8 model families and 5 releases. Still the biggest
   unprofiled contract surface in the catalog.
3. **Fix the pipeline prompt** in `all/0-working/build-enrich-workflows.py` so agents write
   canonical `info.x-provenance` instead of `x-apievangelist-derivation`, and re-emit both workflow
   variants. Until that lands every future wave recreates the unmarked-spec gap.
4. **Re-profile AGNTCY through `pipeline-standards`** rather than the company pipeline.
5. **Cisco's MCP estate** — 18 servers plus the `cisco-open/mcptoolkit-*` suite, where Cisco is
   authoring an MCP Description document format. Unprofiled.
