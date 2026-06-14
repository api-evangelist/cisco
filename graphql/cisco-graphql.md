# Cisco GraphQL Schema

This is a conceptual GraphQL schema for Cisco's APIs, unifying resources from Cisco Meraki, Webex, Catalyst Center (DNA Center), and NSO (Network Services Orchestrator). Cisco provides REST APIs through its DevNet developer platform at https://developer.cisco.com/, and this schema represents a unified GraphQL interface over those services.

## Coverage

### Cisco Meraki
The Meraki Dashboard API manages cloud-controlled networking hardware — wireless access points, switches, security appliances, and cameras. Resources include organizations, networks, devices, clients, SSIDs, VLANs, firewall rules, and traffic shaping policies.

### Cisco Webex
The Webex API powers collaboration — messaging rooms, meetings, memberships, recordings, transcripts, webhooks, bots, and administrative user and license management.

### Cisco Catalyst Center (DNA Center)
The Catalyst Center API provides intent-based networking for campus and branch environments — device inventory, interfaces, topology, sites, IP pools, templates, policies, QoS, issues, tasks, and tags.

### Cisco NSO
The NSO (Network Services Orchestrator) API manages multi-vendor network services — service models, device southbound management, configuration rollbacks, alarms, sync operations, modules, and commits.

## Schema Source

- Meraki API: https://developer.cisco.com/meraki/api-v1/
- Webex API: https://developer.webex.com/docs/api/getting-started
- Catalyst Center API: https://developer.cisco.com/docs/dna-center/api/
- NSO API: https://developer.cisco.com/docs/nso/
- DevNet GitHub: https://github.com/CiscoDevNet

## Types Summary

The schema defines 80 named types across four product areas:

**Meraki (21 types):** Organization, Network, Device, DeviceStatus, Client, ClientUsage, AccessPoint, Switch, MXFirewall, SSID, VLAN, TrafficShaping, ContentFiltering, FirewallRule, L3FirewallRule, L7FirewallRule, MXFirewallSettings, SecurityEvent, Alert, Inventory, License

**Webex (16 types):** Room, Message, Membership, Team, TeamMembership, Meeting, MeetingInvitee, Recording, Transcript, Webhook, Person, Bot, AdminUser, WebexLicense, WebexEvent, DeviceActivation

**Catalyst Center / DNA Center (19 types):** CatalystDevice, CatalystInterface, Topology, PathTrace, Site, Building, Floor, IPPool, Template, TemplateProject, Policy, QoSPolicy, NetworkIssue, CommandRunner, Task, FileInfo, NetworkTag, NetworkUser, NetworkRole

**NSO (12 types):** NSOService, NSODevice, NSODeviceGroup, NSOConfiguration, NSOConfiguration, NSORollback, NSOAlarm, NSOLiveStatus, NSOSync, NSODeviceCLI, NSOModule, NSOTemplate, NSOCommit

**Shared / Root (12 types):** Query, Mutation, Subscription, PageInfo, SortOrder, TimeRange, GeoLocation, Annotation, AuditLog, HealthScore, TagLabel, MetricDataPoint
