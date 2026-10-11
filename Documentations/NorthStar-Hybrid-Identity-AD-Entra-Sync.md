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

<img width="1000" alt="image" src="https://github.com/otraore26/NorthStar-Hybrid-Identity-AD-Entra-Sync/blob/b6aefd54bae91b185bcf7656700b1573ab7f30fc/Screenshots/Step-5%20select-ad-forest-nmgm.png">

**Next step:** Click **Add Directory** and provide the required
AD forest account information to configure the directory connection.


### Step 6: Enter the Existing AD Forest Account

In the **AD forest account** dialog, I selected
**Use existing AD account** and entered the credentials for
the lab account **NMGM\Administrator**.

The password was masked. At this stage, the credentials had
been entered but the directory connection was not yet confirmed.

**Purpose:** Provide an Active Directory account for the wizard
to use when connecting to the on-premises forest for synchronization.

**Screenshot:**

<img width="1000" alt="image" src="https://github.com/otraore26/NorthStar-Hybrid-Identity-AD-Entra-Sync/blob/8b4a721710ce3b0ecd06accaa2640c705814222d/Screenshots/Step-6%20Enter-existing-ad-forest-account.png">


**Next step:** Click **OK** to submit the credentials, then check
that **NMGM.com** appears under **Configured directories**.

### Step 7: Confirm the Active Directory Connection

After submitting the AD forest account credentials, I returned
to the **Connect your directories** page in the Microsoft Entra
Connect Sync setup wizard.

The **Configured directories** section displayed
**NMGM.com (Active Directory)** with a green check mark,
confirming that the directory had been successfully added.
The **Next** button was now available.

**Purpose:** Verify that the on-premises Active Directory forest
was connected in the wizard before continuing configuration.

**Screenshot:**

<img width="1000" alt="image" src="https://github.com/otraore26/NorthStar-Hybrid-Identity-AD-Entra-Sync/blob/9e64c712ceed168f9feca64f9ac48e30c069d8ea/Screenshots/Step-7%20ad-directory-connection-confirmed.png">


**Next step:** Click **Next** to review the
**Microsoft Entra sign-in configuration**, including the
Active Directory UPN suffix and its matching Entra ID domain.

### Step 8: Review the UPN Suffix and Entra ID Domain Status

I proceeded to the **Microsoft Entra sign-in configuration** page
in the Microsoft Entra Connect Sync setup wizard.

The Active Directory UPN suffix **nmgm.com** displayed
**Not Added** under Microsoft Entra ID Domain. The selected
username attribute was **userPrincipalName**.

The wizard displayed a warning about sign-in when the UPN suffix
does not match a verified domain. The option to continue without
matching all UPN suffixes was unchecked, and **Next** was disabled.

**Purpose:** Check whether the on-premises user sign-in suffix
matches a verified domain in Microsoft Entra ID before proceeding.

**Screenshot:**
<img width="1000" alt="image" src="https://github.com/otraore26/NorthStar-Hybrid-Identity-AD-Entra-Sync/blob/b819ff611377ec2ba87b1488cdada63e150b0511/Screenshots/Step-8%20%20upn-suffix-domain-not-added.png">



**Next step:** Review the domain mismatch and document how it
was handled before continuing to **Domain and OU filtering**.


### Step 9: Configure Domain and OU Filtering

I proceeded to the **Domain and OU filtering** page in the
Microsoft Entra Connect Sync setup wizard.

With **NMGM.com** selected as the directory, I selected
**Sync all domains and OUs**. This included all domains and
organizational units in the connected forest at this filtering stage,
rather than limiting synchronization to specific OUs.

**Purpose:** Define the domain and organizational unit scope
for directory synchronization in the lab.

**Screenshot:**

<img width="1000" alt="image" src="https://github.com/otraore26/NorthStar-Hybrid-Identity-AD-Entra-Sync/blob/d3bf6488bc85344336fd3da87465e3771fd67294/Screenshots/Step-9%20%20Select-sync-all-domains-and-ous.png">




**Next step:** Click **Next** to configure how users are uniquely
identified across the on-premises directory and Microsoft Entra ID.
