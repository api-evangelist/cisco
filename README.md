# Cisco (cisco)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Cisco provides a comprehensive suite of APIs across its networking, security, collaboration, and cloud infrastructure platforms. Through Cisco DevNet, developers can access REST APIs, SDKs, and developer tools for Meraki, Webex, Catalyst Center, ACI, ISE, Intersight, ThousandEyes, SD-WAN, and other Cisco products.

**URL:** [https://raw.githubusercontent.com/api-evangelist/cisco/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/cisco/refs/heads/main/apis.yml)

**Run:** [Capabilities Using Naftiko](https://github.com/naftiko/fleet?utm_source=api-evangelist&utm_medium=readme&utm_campaign=company-api-evangelist&utm_content=repo)

## Tags:

 - Collaboration, Enterprise, Networking, Security, SD-WAN

## Timestamps

- **Created:** 2024-01-01
- **Modified:** 2026-04-18

## APIs

### Cisco Meraki Dashboard API
RESTful API for managing Cisco Meraki cloud-managed networking devices.

### Cisco Webex API
REST API for Webex collaboration platform.

### Cisco Catalyst Center API
REST API for intent-based networking with Cisco Catalyst Center.

### Cisco ACI API
REST API for Cisco Application Centric Infrastructure.

### Cisco ISE API
REST API for Cisco Identity Services Engine.

### Cisco Intersight API
REST API for Cisco Intersight cloud operations platform.

### Cisco SD-WAN API
REST API for Cisco SD-WAN management.

### Cisco ThousandEyes API
REST API for digital experience monitoring.

## Features

| Name | Description |
|------|-------------|
| Network Automation | Automate network device configuration across campus, branch, and data center environments. |
| Intent-Based Networking | Define business intent and let the network translate it into device configurations. |
| Cloud-Managed Networking | Manage distributed networks from the cloud with Meraki APIs. |
| Digital Experience Monitoring | Monitor end-to-end digital experiences with ThousandEyes. |
| Zero Trust Security | Implement zero-trust network access policies with ISE APIs. |
| Infrastructure as Code | Define and manage network infrastructure programmatically. |

## Use Cases

| Name | Description |
|------|-------------|
| Network Configuration Management | Automate network device configuration changes across thousands of devices. |
| Security Policy Automation | Programmatically manage access control policies and security groups. |
| Collaboration Integration | Build bots and integrations on the Webex platform. |
| Cloud Infrastructure Management | Manage hybrid cloud infrastructure with Intersight APIs. |
| Network Monitoring and Analytics | Collect and analyze network telemetry data. |

## Integrations

| Name | Description |
|------|-------------|
| Ansible | Network automation modules for Cisco platforms. |
| Terraform | Terraform providers for Cisco ACI, Intersight, and Meraki. |
| ServiceNow | ITSM integration for automated incident management. |
| Splunk | Security and network analytics integration. |
| Python | Python SDKs for all major Cisco platforms. |

## Artifacts

Machine-readable API specifications organized by format.

### OpenAPI

- [cisco-meraki (see all/cisco-meraki/openapi/)](https://raw.githubusercontent.com/api-evangelist/cisco-meraki/refs/heads/main/openapi/cisco-meraki-organizations-api-openapi.json)

### JSON Schema

- [cisco-meraki-api-device-schema.json](json-schema/cisco-meraki-api-device-schema.json)
- [cisco-meraki-api-network-schema.json](json-schema/cisco-meraki-api-network-schema.json)
- [cisco-meraki-api-organization-schema.json](json-schema/cisco-meraki-api-organization-schema.json)

### JSON-LD

- [cisco-context.jsonld](json-ld/cisco-context.jsonld)

### Examples

- [cisco-meraki-api-device-example.json](examples/cisco-meraki-api-device-example.json)
- [cisco-meraki-api-network-example.json](examples/cisco-meraki-api-network-example.json)
- [cisco-meraki-api-organization-example.json](examples/cisco-meraki-api-organization-example.json)

## Capabilities

Naftiko capabilities organized as shared per-API definitions composed into customer-facing workflows.

### Shared Per-API Definitions

- [meraki.yaml](capabilities/shared/meraki.yaml)

### Workflow Capabilities

- [network-management.yaml](capabilities/network-management.yaml)

## Vocabulary

- [cisco-vocabulary.yaml](vocabulary/cisco-vocabulary.yaml)

## Rules

- [cisco-spectral-rules.yml](rules/cisco-spectral-rules.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
