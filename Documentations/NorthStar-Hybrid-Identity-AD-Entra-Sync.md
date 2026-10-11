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


<img width="1000" alt="image" src="https://github.com/otraore26/NorthStar-Hybrid-Identity-AD-Entra-Sync/blob/8e40f26b953d54c2f51f96670b0deada976af3ef/Screenshots/step-01-entra-connect-initial-status.png">

**Next step:** Obtain and install Microsoft Entra Connect Sync,
then configure the connection between the two directories.


### Step 2: Download Microsoft Entra Connect Sync

I accessed the **Get started** section under Microsoft Entra Connect
in the Microsoft Entra admin center and initiated the installer download.

The browser’s Downloads panel displayed **AzureADConnect.msi**
with the download in progress.

**Purpose:** Obtain the installer needed to configure synchronization
between on-premises Active Directory and Microsoft Entra ID.

**Screenshot:**

<img width="1000" alt="image" src="https://github.com/otraore26/NorthStar-Hybrid-Identity-AD-Entra-Sync/blob/8e40f26b953d54c2f51f96670b0deada976af3ef/Screenshots/Step-02-entra-connect-welcome-license-terms.png">

**Next step:** Once the download finishes, launch the installer
to begin setup.


### Step 3: Install the Required Synchronization Components

I proceeded to the **Install required components** page in the
Microsoft Entra Connect Sync setup wizard on my **NMG-DC01**
virtual machine.

The wizard detected no existing synchronization service and began
installing the **Synchronization Service**. I left the optional
customization settings unselected.

**Purpose:** Install the components needed to configure synchronization
between on-premises Active Directory and Microsoft Entra ID.

**Screenshot:**

<img width="1000" alt="image" src="https://github.com/otraore26/NorthStar-Hybrid-Identity-AD-Entra-Sync/blob/8e40f26b953d54c2f51f96670b0deada976af3ef/Screenshots/Step-3%20install-required-sync-components.png">
![Installing Microsoft Entra Connect Sync components](<images/Step-3 install-required-sync-components.png>)

**Next step:** Once installation finishes, continue to the
**User sign-in** page to select the authentication method.


### Step 4: Select the User Sign-In Method

I proceeded to the **User sign-in** page in the Microsoft Entra
Connect Sync setup wizard on my **NMG-DC01** virtual machine.

At this stage, I selected **Password Hash Synchronization**
and checked **Enable single sign-on**.

**Purpose:** Choose the sign-in method and request single sign-on
configuration as part of the hybrid identity setup.

**Screenshot:**
<img width="1000" alt="image" src="https://github.com/otraore26/NorthStar-Hybrid-Identity-AD-Entra-Sync/blob/8e40f26b953d54c2f51f96670b0deada976af3ef/Screenshots/Step-4User%20Sign%20In.png">

**Next step:** Continue to **Connect to Microsoft Entra**
to authenticate to the Microsoft Entra ID tenant.


### Step 5: Select the On-Premises Active Directory Forest

I proceeded to the **Connect your directories** page in the
Microsoft Entra Connect Sync setup wizard.

The directory type was set to **Active Directory**, and
**NMGM.com** was selected in the **Forest** dropdown.

At this stage, the wizard displayed **No directories are currently
configured**, indicating that the selected forest had not yet
been added.

**Purpose:** Identify the on-premises Active Directory forest
to connect to Microsoft Entra ID for synchronization.

**Screenshot:**

![Selecting the NMGM.com Active Directory forest](<images/Step-5 select-ad-forest-nmgm.png>)

**Next step:** Click **Add Directory** and provide the required
AD forest account information to configure the directory connection.
