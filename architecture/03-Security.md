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

## Conditional Access Security Groups

| Group Name        | Membership | Purpose                                                                                    |
|-------------------|------------|--------------------------------------------------------------------------------------------|
| sg_ca_require_mfa | Dynamic    | Targets all active users for Multi-Factor Authentication (MFA) Conditional Access policies |
| sg_ca_exclude_mfa | Assigned   | Excludes emergency access and service accounts from MFA Conditional Access policies        |

Conditional Access policies target dedicated Security Groups instead of individual users. This design improves scalability, simplifies administration and aligns with enterprise identity governance best practices.


## Operational Security Groups

| Group Name            | Membership | Purpose                                                          |
|-----------------------|------------|------------------------------------------------------------------|
| sg_intune_users       | Dynamic    | Targets users for Microsoft Intune assignments                   |
| sg_vm_administrators  | Assigned   | Azure Virtual Machine administration                             |
| sg_test_users         | Assigned   | Test user assignments for validation and user acceptance testing |

Operational Security Groups are used to simplify administration by separating workload-specific permissions from privileged administrative access.




## Administrative Accounts

| Account  | Purpose                  | Assignment                               |
|----------|--------------------------|------------------------------------------|
| ga-pauli | Daily administration     | Eligible through PIM                     |
| bg-admin | Emergency access         | Permanent Global Administrator           |
| test.user| User acceptance testing  | Member of operational groups as required |

Daily administrative account receives privileged access through PIM-enabled Security Groups. 
Break Glass account remains permanently assigned to the Global Administrator role and is excluded from Conditional Access policies to ensure emergency access.
Test User account is used to validate that a system meets requirements and works as intended in real-world scenarios before deployment.


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



## Authentication Methods

### Overview

Authentication methods have been configured to align with Microsoft's passwordless authentication strategy while maintaining secure fallback options for account recovery and exceptional scenarios.

A dedicated security group `sg_ca_require_mfa` is used to target authentication method policies. A separate exclusion group `sg_ca_exclude_mfa` is used for emergency access (break glass) accounts and service accounts that must not be affected by user MFA policies.



### Enabled authentication methods

| Method                      | Purpose                                            |
|-----------------------------|----------------------------------------------------|
| Microsoft Authenticator     | Primary MFA method and passwordless authentication |
| Passkey (FIDO2)             | Phishing-resistant passwordless authentication     |
| Temporary Access Pass (TAP) | Secure onboarding and MFA registration             |
| SMS                         | Fallback MFA method only                           |



### Disabled authentication methods

| Method                           | Reason                                                                        |
|----------------------------------|-------------------------------------------------------------------------------|
| Voice Call                       | Legacy authentication method, not recommended for new deployments             |
| Email OTP                        | Might be configured later for Azure AD B2B guest users                        |
| QR Code Authentication           |  Designed for frontline worker scenarios. Not applicable to this environment  |
| Hardware OATH Tokens             | Not required for this lab environment                                         |
| Certificate-based Authentication | Not required for this lab environment                                         |
| Verified ID                      | Out of scope for this project                                                 |



### SMS Authentication Configuration

SMS authentication is enabled only as a fallback authentication method.

Configuration:

- Authentication Method: Enabled
- Target Group: sg_ca_require_mfa
- Excluded Group: sg_ca_exclude_mfa
- Use for sign-in: Disabled

Disabling 'Use for sign-in' prevents SMS from being used as a primary authentication method while still allowing it as an MFA verification option.


### Microsoft Authenticator

Microsoft Authenticator is configured as the primary authentication method.

Configuration includes:

- Target Group: sg_ca_require_mfa
- Excluded Group: sg_ca_exclude_mfa

- Passwordless authentication
- Push notifications
- Number matching
- Passkey registration support

Microsoft Authenticator is the preferred authentication method for all standard users.


### Passkeys (FIDO2)

Passkeys are enabled to provide phishing-resistant authentication.

Configuration:

- Target Group: sg_ca_require_mfa
- Excluded Group: sg_ca_exclude_mfa
- Profile: Default passkey profile



### Temporary Access Pass (TAP)

Temporary Access Pass is enabled to support secure onboarding.

Typical onboarding flow:

1. Administrator creates a Temporary Access Pass.
2. User signs in using TAP.
3. User registers Microsoft Authenticator.
4. (Optional) User registers a Passkey (FIDO2).
5. TAP expires automatically.

This approach eliminates the need to distribute permanent passwords during onboarding.


### Authentication Design Principles

The authentication configuration follows Microsoft's Zero Trust recommendations:

- Passwordless authentication preferred wherever possible.
- Phishing-resistant authentication methods enabled.
- Legacy authentication methods minimized.
- Multiple secure authentication methods available for recovery.
- Emergency access accounts excluded from user authentication policies.

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
* [x] Configure Authentication Methods
* [x] Configure Multi-Factor Authentication

## Pending Tasks


* [ ] Configure Conditional Access
* [ ] Configure Azure RBAC
* [ ] Configure Identity Protection
* [ ] Validate administrative access model



# Evidence

| Item                            | Screenshot                                                       |
| ------------------------------- | ---------------------------------------------------------------- |
| PIM Overview                    | images/screenshots/security/pim-assignments.png                  |
| MFA settings                    | images/screenshots/security/mfa-settings.png                     |
| Authenticator settings          | images/screenshots/security/microsoft-authenticator-settings.png | 
| Authentication methods overview | images/screenshots/security/authentication-methods-overview.png  |
| Temporary Access Pass settings  | images/screenshots/security/tap-settings.png                     |
| Passkey settings                | images/screenshots/security/passkey-settings.png                 |  


# Lessons Learned

* Privileged access should be assigned through dedicated Security Groups rather than directly to users.
* Microsoft Entra Privileged Identity Management significantly reduces standing administrative privileges.
* Break Glass accounts should remain separate from daily administrative activities.
* Group-based privileged administration simplifies long-term management and auditing.
* Just-In-Time administrative access aligns with Microsoft Zero Trust recommendations.



# Next Phase

The next phase continues the Security Foundation implementation.

Objectives:

* Configure Azure Role Based Access Control (RBAC)
* Configure Microsoft Entra Identity Protection
* Validate the Zero Trust administrative model
