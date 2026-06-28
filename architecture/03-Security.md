# 03 – Security Foundation

# Purpose

The purpose of this phase is to establish a secure administrative model for the Cloud Consult Lab environment by implementing Microsoft Entra Privileged Identity Management (PIM), privileged role governance and the principle of least privilege following Microsoft's Zero Trust security model.



# Environment Overview

| Property             | Value                                          |
| -------------------- | ---------------------------------------------- |
| Identity Platform    | Microsoft Entra ID                             |
| License              | Microsoft Entra ID P2                          |
| Security Model       | Zero Trust                                     |
| Privileged Access    | Microsoft Entra Privileged Identity Management |
| Administrative Model | Group-based privileged administration          |



# Design Decisions

The following security design decisions were made before implementation:

* Privileged administrative roles are assigned to dedicated Security Groups.
* Administrative users receive privileged access through group membership instead of direct role assignments.
* Microsoft Entra Privileged Identity Management (PIM) is used to provide Just-In-Time (JIT) administrative access.
* Dedicated administrative accounts are separated from standard user accounts.
* A dedicated Break Glass account provides emergency administrative access.
* Administrative roles follow the principle of least privilege.
* Permanent administrative access is minimized.



# Implementation

## Administrative Security Groups

| Group Name                            | Assignment | Microsoft Entra Role          |
| ------------------------------------- | ---------- | ----------------------------- |
| sg_pim_global_administrators          | Eligible   | Global Administrator          |
| sg_pim_privileged_role_administrators | Eligible   | Privileged Role Administrator |
| sg_pim_intune_administrators          | Eligible   | Intune Administrator          |
| sg_pim_security_administrators        | Eligible   | Security Administrator        |

All privileged roles are assigned through Microsoft Entra Privileged Identity Management (PIM).

Administrative users receive privileged access through Security Group membership.



## Administrative Accounts

| Account  | Purpose              | Assignment                     |
| -------- | -------------------- | ------------------------------ |
| ga-pauli | Daily administration | Eligible through PIM           |
| bg-admin | Emergency access     | Permanent Global Administrator |



## Implemented Security Controls

The following controls have been implemented:

* Microsoft Entra ID P2
* Microsoft Entra Privileged Identity Management
* Group-based privileged administration
* Eligible Global Administrator role
* Eligible Privileged Role Administrator role
* Eligible Intune Administrator role
* Eligible Security Administrator role
* Break Glass account



# Configuration

The following security configuration has been completed:

* Microsoft Entra Privileged Identity Management enabled
* Administrative role groups created
* Eligible role assignments configured
* Break Glass administrative account configured
* Group-based privileged administration implemented

The following configuration will be completed during this phase:

* Authentication Methods
* Multi-Factor Authentication
* Conditional Access
* Azure Role Based Access Control (RBAC)
* Identity Protection
* Security policy validation



# Validation

## Completed Tasks

* [x] Microsoft Entra ID P2 activated
* [x] Microsoft Entra Privileged Identity Management enabled
* [x] Privileged administrative Security Groups created
* [x] Global Administrator configured as Eligible
* [x] Privileged Role Administrator configured as Eligible
* [x] Intune Administrator configured as Eligible
* [x] Security Administrator configured as Eligible
* [x] Break Glass account configured
* [x] PIM activation successfully tested

## Pending Tasks

* [ ] Configure Authentication Methods
* [ ] Configure Multi-Factor Authentication
* [ ] Configure Conditional Access
* [ ] Configure Azure RBAC
* [ ] Configure Identity Protection
* [ ] Validate administrative access model



# Evidence

| Item                  | Screenshot                                               |
| --------------------- | -------------------------------------------------------- |
| PIM Overview          | images/screenshots/security/pim-assignments.png             |




# Lessons Learned

* Privileged access should be assigned through dedicated Security Groups rather than directly to users.
* Microsoft Entra Privileged Identity Management significantly reduces standing administrative privileges.
* Break Glass accounts should remain separate from daily administrative activities.
* Group-based privileged administration simplifies long-term management and auditing.
* Just-In-Time administrative access aligns with Microsoft Zero Trust recommendations.



# Next Phase

The next phase continues the Security Foundation implementation.

Objectives:

* Configure Authentication Methods
* Configure Multi-Factor Authentication
* Configure Conditional Access policies
* Configure Azure Role Based Access Control (RBAC)
* Configure Microsoft Entra Identity Protection
* Validate the Zero Trust administrative model
