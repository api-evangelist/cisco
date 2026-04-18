# Cisco (cisco)
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

- [cisco-meraki-api.yaml](openapi/cisco-meraki-api.yaml)

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
