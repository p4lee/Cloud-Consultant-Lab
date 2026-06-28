# 02 – Identity Foundation

# Purpose

The purpose of this phase is to establish a secure identity foundation for the Cloud Consult Lab environment. The objective is to implement administrative accounts, security groups, group-based licensing and identity governance following Microsoft security best practices and the principle of least privilege.



# Environment Overview

| Property | Value |
|----------|-------|
| Tenant | Cloud Consult Lab |
| Primary Domain | cloud-consult-lab.site |
| Identity Platform | Microsoft Entra ID |
| Authentication | Cloud-only |
| Administrative Model | Dedicated Administrative Accounts |
| Licensing | Group-based licensing |
| Privileged Access | Microsoft Entra ID P2 |


# Design Decisions

The following design decisions were made before implementing identities:

- Dedicated administrative accounts are used instead of personal accounts.
- Emergency access is provided through a dedicated Break Glass account.
- Administrative access will be managed using Microsoft Entra Privileged Identity Management (PIM).
- Security Groups are created before assigning Azure roles.
- Microsoft licenses are assigned using Security Groups instead of direct user assignments.
- Administrative accounts are separated from standard user accounts.
- Cloud-only identity architecture is used.



# Implementation

## Administrative Accounts

| Display Name | User Principal Name | Purpose |
|--------------|--------------------|---------|
| Global Administrator Pauli | ga-pauli@cloud-consult-lab.site | Daily administrative account |
| Break Glass Administrator | bg-admin@cloud-consult-lab.site | Emergency access account |
| Test User | test.user@cloud-consult-lab.site | User acceptance and Intune testing |



## Security Groups

| Group Name | Purpose |
|------------|---------|
| sg_global_administrators | Global Administrator role assignments |
| sg_intune_users | Microsoft Intune user assignments |
| sg_pim_eligible_administrators | Eligible administrators managed through PIM |
| sg_test_users | Test user assignments |
| sg_vm_administrators | Azure Virtual Machine administration |

All groups are configured as:

- Security Group
- Assigned membership

Group owner:

- ga-pauli



## License Groups

| Group Name                    | Assigned License               |
|-------------------------------|--------------------------------|
| lic_m365_businesspremium      | Microsoft 365 Business Premium |
| lic_entra_id_p2               | Microsoft Entra ID P2          |

Licenses are assigned through Security Groups instead of direct user assignment.

Current licensed administrative user:

- ga-pauli

Benefits of group-based licensing:

- Centralized license management
- Simplified administration
- Consistent user provisioning
- Reduced administrative overhead
- Enterprise best practice



# Configuration

The following identity configuration has been completed:

- Custom domain verified
- Organization name configured
- Dedicated administrator accounts
- Break Glass account created
- Security Groups created
- License Groups created
- Group ownership configured
- Microsoft 365 Business Premium Trial activated
- Microsoft Entra ID P2 Trial activated
- Group-based licensing implemented

The following configuration will be completed during the next phase:

- Azure Role Based Access Control (RBAC)
- Privileged Identity Management (PIM)
- Conditional Access
- Multi-Factor Authentication
- Administrative Unit configuration (if required)



# Validation

## Completed Tasks

- [x] Custom domain verified
- [x] Organization name configured
- [x] Administrative accounts created
- [x] Break Glass account created
- [x] Test user created
- [x] Security Groups created
- [x] License Groups created
- [x] Group ownership assigned
- [x] Microsoft 365 Business Premium Trial activated
- [x] Microsoft Entra ID P2 Trial activated
- [x] Group-based licensing configured

## Pending Tasks

- [ ] Azure RBAC assignments
- [ ] Privileged Identity Management configuration
- [ ] Conditional Access
- [ ] Multi-Factor Authentication
- [ ] Identity protection policies



# Evidence

| Item                     | Screenshot                                             |
|--------------------------|--------------------------------------------------------|
| Tenant Overview          | images/screenshots/identity/tenant-overview.png        |
| Custom Domain            | images/screenshots/identity/custom-domain.png          |
| Users                    | images/screenshots/identity/users.png                  |
| Security Groups          | images/screenshots/identity/security-groups.png        |
| License Groups           | images/screenshots/identity/license-groups.png         |
| Assigned Licenses        | images/screenshots/identity/group-based-licensing.png  |
| User License Assignment  | images/screenshots/identity/user-license-assignment.png|



# Lessons Learned

- Dedicated administrative accounts significantly improve security.
- Group-based licensing is more scalable than assigning licenses directly to users.
- Security Groups simplify Azure RBAC administration.
- A verified custom domain creates a professional enterprise identity environment.
- Administrative and standard user accounts should always be separated.
- Identity governance should be implemented before assigning privileged roles.


# Next Phase

The next phase focuses on Privileged Access Management.

Objectives:

- Configure Azure Role Based Access Control (RBAC)
- Configure Microsoft Entra Privileged Identity Management (PIM)
- Assign Global Administrator as an Eligible role
- Configure Break Glass permanent access
- Configure Multi-Factor Authentication
- Configure Conditional Access policies
- Implement least privilege administrative access