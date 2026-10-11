## Implementation Documentation

This documentation presents the step-by-step implementation of my
**NorthStar Medical Group Hybrid Identity Synchronization** project.
In this hands-on lab, I connected an on-premises Windows Server
Active Directory environment with Microsoft Entra ID to synchronize
selected test users and groups.

Working as the IAM Engineer in a fictional healthcare scenario,
I prepared the source identities, configured directory synchronization,
and validated the resulting cloud identities.

The following sections document the process from the initial
synchronization status and installer download through configuration
and validation. Screenshots support the steps, while accompanying
explanations describe what I did, why it was necessary, and what
the results demonstrated.

**Lab scope:** This project uses a fictional organization and test
accounts. It does not involve real employee or patient information.

### Step 1: Review the Initial Microsoft Entra Connect Status

I opened the Microsoft Entra admin center from my NMG-DC01
virtual machine and navigated to **Microsoft Entra Connect → Connect Sync**
to review the tenant’s initial synchronization status.

The page displayed:

- **Microsoft Entra Connect sync:** Not installed.
- **Last sync:** Sync has never run.
- **Password Hash Sync:** Disabled.

This screenshot documents the starting state of the lab before
configuring synchronization between on-premises Active Directory
and Microsoft Entra ID.


<img width="1000" alt="image" src="https://github.com/user-attachments/assets/cfc5dbcf-3fcb-4a71-9c13-2a49f8bab3e6">
![Initial Microsoft Entra Connect status](../images/step-01-entra-status.png)

**Next step:** Obtain and install Microsoft Entra Connect Sync,
then configure the connection between the two directories.
