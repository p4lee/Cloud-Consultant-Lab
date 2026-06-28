# 01 – Governance Foundation

## Purpose

The objective of this phase is to establish the governance foundation for the Cloud Consult Lab before deploying any Azure resources. The goal is to ensure that all future deployments follow consistent naming, tagging, cost management and organizational standards.


# Environment Overview

| Property       | Value                    |
| -------------- | -------------------------|
| Cloud Platform | Microsoft Azure          |
| Tenant Type    | Cloud-only               |
| Region         | North Europe             |
| Environment    | Test                     |
| Subscription   | CCLAB                    |
| IaC            | Terraform (planned)      |


# Resource Organization

A dedicated Resource Group is used to isolate all project resources.

| Resource          | Name                               |
| -------------------------------------------------------|
| Resource Group    | rg-cclab-ne-test-01                |


| Planned Resources       |
|-------------------------|
| Virtual Network         |
| Network Security Group  |
| Virtual Machine         |
| Network Interface       |
| Managed Disk            |
| Log Analytics Workspace |
| Storage Account         |
| Azure Monitor           |
| Recovery Services Vault |

Using a single Resource Group simplifies deployment, cost tracking, lifecycle management and resource cleanup. In a production enterprise environment, resources would typically be separated into multiple Resource Groups based on ownership and lifecycle.

# Naming Convention

A consistent naming convention has been defined for all Azure resources.

| Resource Type          | Naming Pattern                        | Example                   |
| ---------------------- | --------------------------------------|---------------------------|
| Resource Group         | rg-cclab-region-environment-instance  | rg-cclab-ne-test-01       |
| Virtual Network        | vnet-cclab-region-environment-instance| vnet-cclab-ne-test-01     |
| Subnet                 | snet-purpose-instance                 | snet-management-01        |
| Network Security Group | nsg-purpose-instance                  | nsg-management-01         |
| Network Interface      | nic-cclab-role-instance               | nic-cclab-mgmt-01         |
| Public IP              | pip-cclab-role-instance               | pip-cclab-mgmt-01         |
| Virtual Machine        | vm-cclab-role-instance                | vm-cclab-mgmt-01          |
| Log Analytics          | law-cclab-environment-instance        | law-cclab-test-01         |
| Storage Account        | stcclabtest01                         | stcclabtest01             |
|Recovery Services Vault | rsv-cclab-environment-instance        | rsv-cclab-test-01         |

Storage Account names must be globally unique and follow Azure naming restrictions.

# Tagging Strategy

Every Azure resource must include the following tags.

| Tag         | Value                |
| ----------- | ------------------   |
| Project     | Cloud-Consult-Lab |
| ProjectCode | CCLAB                |
| Owner       | github.com/p4lee     |
| Environment | Test                 |
| ManagedBy   | Terraform            |
| CostCenter  | Learning             |
| Department  | PersonalLab          |

The tagging strategy supports:

Cost reporting
Resource ownership
Governance
Automation
Operational management

# Cost Management

The project budget is approximately 172 EUR of Azure credits.

An Azure Budget has been configured to monitor project spending throughout the duration of the lab project. The budget includes threshold-based email notifications to help control Azure costs.

50%
80%
90%
100%

The purpose is to prevent unexpected Azure costs while demonstrating financial governance best practices.

# Regional Design

The selected deployment region is North Europe.

Reasons for this decision:

Low latency for Finland
High Azure service availability
Broad Microsoft Azure service support
Suitable region for Microsoft 365 and Azure integrations

# Governance Decisions

The following governance decisions have been made during Phase 1:

Cloud-only architecture
Single Resource Group deployment
Standardized naming convention
Standardized resource tagging
Cost monitoring through Azure Budget
North Europe as the primary deployment region
Terraform selected as the Infrastructure as Code solution


# Validation

## Completed Tasks

- [x] Azure subscription reviewed
- [x] Resource Group created
- [x] Naming convention documented
- [x] Tagging strategy documented
- [x] Azure Budget configured
- [x] Resource tags applied

## Evidence

| Item               | Screenshot |
|--------------------|------------|
| Azure Subscription | images/screenshots/governance/subscription.png |
| Resource Group     | images/screenshots/governance/resource-group.png |
| Azure Budget       | images/screenshots/governance/budget.png |
| Resource Tags      | images/screenshots/governance/resource-tags.png |


# Lessons Learned

- Governance should be established before deploying workloads.
- A consistent naming convention simplifies administration and automation.
- Resource tagging improves governance and cost management.
- A single Resource Group is appropriate for a portfolio environment, while larger enterprise environments typically use multiple Resource Groups.
- Governance decisions made early reduce rework during later deployment phases.

# Next Phase


Phase 2 focuses on establishing the identity foundation for the Cloud Consult Lab.

Objectives:

- Create administrative accounts
- Create test user
- Create security groups
- Configure role-based access control (RBAC)
- Configure Privileged Identity Management (PIM)
- Prepare the identity architecture for Conditional Access and Microsoft Intune.