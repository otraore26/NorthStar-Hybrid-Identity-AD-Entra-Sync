<img width="1000" alt="image" src="https://github.com/otraore26/NorthStar-Hybrid-Identity-AD-Entra-Sync/blob/189256df27b6ba819f5af9c46c6c32107a0ed35e/Screenshots/NorthStar%20Hybrid%20Identity%20Lab.png">

# NorthStar Medical Group: Hybrid Identity Synchronization

**Project status:** Completed within the documented scope  
**Scenario:** Fictional healthcare organization  
**Focus:** Active Directory · Microsoft Entra ID · Hybrid Identity

## Project Overview

NorthStar Medical Group is a fictional healthcare organization
expanding its use of cloud services. This project connected its
on-premises Active Directory environment with Microsoft Entra ID
using Microsoft Entra Connect Sync.

I configured directory synchronization, verified synchronized test
users, and confirmed that department security groups appeared in
Microsoft Entra ID. I also verified that the **HR-Users** group
displayed **Windows Server AD** as its source and contained
**four direct user members**.

During implementation, I investigated an authentication failure
caused by an incorrect server clock and documented the resolution.

This project establishes the foundation for a separate
**Joiner-Mover-Leaver (JML)** identity lifecycle project.

## Step-by-Step Documentation

The complete implementation guide includes **20 documented steps**,
configuration screenshots, troubleshooting notes, and validation results.

[View the complete implementation documentation](https://github.com/otraore26/NorthStar-Hybrid-Identity-AD-Entra-Sync/blob/main/Documentations/NorthStar-Hybrid-Identity-AD-Entra-Sync.md)

## Project Objectives

- Connect the existing Active Directory lab to Microsoft Entra ID.
- Configure Microsoft Entra Connect Sync.
- Define the directory synchronization scope.
- Verify test user synchronization and department group visibility.
- Confirm the synchronization source of a department security group.
- Troubleshoot an implementation issue.
- Document configuration decisions and validation evidence.

## Fictional Scenario and My Role

NorthStar Medical Group used on-premises Active Directory to manage
employee identities. As the organization adopted cloud services,
it needed those identities to be available in Microsoft Entra ID.

Acting as the **IAM Engineer** in this scenario, I configured the
connection between the directories, reviewed setup warnings,
resolved an authentication issue, and validated cloud identities.

## Lab Environment

| Component | Configuration and purpose |
|---|---|
| Lab server | **NMG-DC01**, the Windows Server virtual machine used for the lab |
| Virtualization | Oracle VirtualBox |
| Source directory | Active Directory Domain Services — **NMGM.com** |
| Synchronization tool | Microsoft Entra Connect Sync |
| Cloud directory | Microsoft Entra ID — **NMGM.onmicrosoft.com** |
| Test users | Used to verify on-premises synchronization status |
| Department groups | **Finance-Users**, **HR-Users**, **IT-Users**, and **Operations-Users** |

## Synchronization Configuration

| Setting | Documented configuration |
|---|---|
| Connected forest | **NMGM.com** |
| Domain and OU filtering | **Sync all domains and OUs** |
| User and device filtering | **Synchronize all users and devices**, subject to synchronization rules |
| Final sign-in method | **Pass-through authentication** |
| Password hash synchronization | Selected in the final configuration |
| Single sign-on | Selected during setup |
| Password and group writeback | Selected during setup; functional testing not included |
| Source anchor | **mS-DS-ConsistencyGuid** |
| Staging mode | Unchecked |
| Start synchronization after configuration | Checked |
| Export deletion threshold | **500** |

The initial sign-in screenshot showed Password Hash Synchronization.
The final configuration summary showed Pass-through authentication
with password hash synchronization also enabled.

These settings record the lab configuration. Feature selection
alone does not confirm successful end-to-end operation.

## Implementation Summary

1. Reviewed the tenant's initial Microsoft Entra Connect status.
2. Downloaded the installer and installed synchronization components.
3. Configured authentication options and connected the AD forest.
4. Reviewed the UPN suffix and domain status.
5. Configured domain, OU, user, and device filtering.
6. Reviewed source-anchor and optional feature settings.
7. Provided credentials for single sign-on configuration.
8. Reviewed and applied the final configuration.
9. Confirmed configuration success and synchronization initiation.
10. Verified synchronized users and the HR-Users group's source.

## Validation Results

| Check | Observed result | Status |
|---|---|---|
| Connect Sync configuration | Setup completed successfully and initiated synchronization | Verified |
| Tenant connection status | Microsoft Entra Connect displayed **Enabled** | Verified |
| Test user synchronization | Visible test users displayed **On-premises sync enabled: Yes** | Verified |
| Department groups | Finance, HR, IT, and Operations security groups appeared in Entra ID | Verified |
| HR group source | **HR-Users** displayed **Windows Server AD** | Verified |
| HR membership count | Four direct user members appeared in the cloud group | Verified |

The tenant dashboard displayed **16 users** and **13 groups**.
These totals represent tenant inventory, not the number of objects
individually verified as synchronized.

### Validation Limits

The following checks were not demonstrated in the included evidence:

- Detailed user attribute comparisons between both directories.
- Member-by-member group membership comparisons with Active Directory.
- A complete review of synchronization run history and object-level errors.
- End-to-end sign-in and Seamless SSO testing.
- Password writeback and group writeback testing.

## Troubleshooting: Authentication Failure and Clock Skew

### Issue

During Microsoft Entra Connect Sync setup, application-based
authentication could not be configured.

### Investigation

I reviewed the setup logs and identified **AADSTS700027**
alongside certificate validity information.

Further investigation showed that the Windows Server VM's clock
was approximately **three hours ahead** and was using the
**Local CMOS Clock**. In this incident, the incorrect time caused
the certificate's validity period to begin in the future,
preventing authentication.

### Resolution

I configured Windows Time to synchronize with **time.windows.com**,
restarted the Windows Time service, and forced a resynchronization.

### Verification

I checked the synchronization source and confirmed that the
server's UTC time was accurate. Microsoft Entra Connect Sync
configuration subsequently completed successfully.

## Configuration Warnings and Follow-Up

| Observation | Documented status |
|---|---|
| UPN suffix **nmgm.com** displayed **Not Added** | Setup later continued; the handling of this mismatch was not captured |
| Exchange AD schema missing for group writeback | Warning documented; successful writeback was not demonstrated |
| Active Directory Recycle Bin not enabled | Enabling it was recommended by the completion page |
| TPM configuration recommended | Identified as a follow-up security improvement |
| Seamless SSO Group Policy configuration prompted | Additional client configuration and testing were not documented |

## Evidence and Screenshots

The implementation guide contains screenshots showing:

- Initial Microsoft Entra Connect status.
- Installation and directory connection settings.
- Synchronization scope and optional features.
- Configuration completion and recommendations.
- Microsoft Entra Connect displayed as enabled.
- Test users with on-premises synchronization enabled.
- Department security groups in Microsoft Entra ID.
- HR-Users showing Windows Server AD as its source.

[Open the implementation guide and screenshots](https://github.com/otraore26/NorthStar-Hybrid-Identity-AD-Entra-Sync/blob/main/Documentations/NorthStar-Hybrid-Identity-AD-Entra-Sync.md)

## Lessons Learned

- **Accurate time matters:** A server clock discrepancy interrupted
  authentication during setup.
- **Logs guide troubleshooting:** Detailed error information helped
  identify the connection between certificate validity and clock skew.
- **Installation requires validation:** I checked individual user
  synchronization flags and group properties after setup completed.
- **Scope must be explicit:** The lab included all domains and OUs
  and did not use pilot-group filtering.
- **Evidence defines the result:** Group visibility, synchronization
  source, membership counts, and functional tests establish
  different outcomes.

## Security and Privacy

- This lab used a fictional organization and test identities.
- No real employee or patient data was used.
- Passwords, access tokens, private keys, and other secrets must
  not be committed to the repository.
- Public screenshots should be reviewed and sanitized to remove
  unnecessary account and tenant identifiers.

## Conclusion

The hybrid identity synchronization project is complete within
the documented scope.

I configured Microsoft Entra Connect Sync, verified synchronized
test users, and confirmed the on-premises source of the HR-Users
security group. The project demonstrates hybrid identity
configuration, log-based troubleshooting, and evidence-based validation.

## Previous Project: Basic Employee Onboarding and AD RBAC

This project builds on my earlier NorthStar Medical Group lab,
where I created employee accounts, organized departmental OUs,
and configured security groups for role-based access control.

[View the Basic Employee Onboarding and AD RBAC project](https://github.com/otraore26/Basic-Employee-Onboarding-AD-RBAC-)

## Next Project: Joiner-Mover-Leaver Identity Lifecycle

**Status:** Planned

The next project will build on this hybrid identity environment
to demonstrate employee onboarding, role changes, and offboarding.

### Planned Scenarios

- **Joiner:** Create employee accounts, assign department groups,
  and verify synchronization to Microsoft Entra ID.
- **Mover:** Update department and group memberships, remove
  previous access, and verify the changes.
- **Leaver:** Disable accounts, remove access, revoke active
  cloud sessions, and validate offboarding.

### Planned Security Controls

- Multifactor authentication.
- Conditional Access policies.
- Role-based access and least privilege.
- Access reviews.
- Audit-log review.





































































































