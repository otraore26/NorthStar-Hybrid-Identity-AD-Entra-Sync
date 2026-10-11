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


### Step 10: Configure User Identification and the Source Anchor

I proceeded to the **Uniquely identifying your users** page
in the Microsoft Entra Connect Sync setup wizard.

I selected **Users are represented only once across all directories**
and **Let Azure manage the source anchor**, rather than manually
choosing a specific attribute.

**Purpose:** Define how users are identified and how their
on-premises identities are linked to corresponding identities
in Microsoft Entra ID.

**Screenshot:**

<img width="1000" alt="image" src="https://github.com/otraore26/NorthStar-Hybrid-Identity-AD-Entra-Sync/blob/1f9faa4a6e5dbe5c215ee3c899f7be44c7e22821/Screenshots/Step-10%20%20User-identification-and-source-anchor.png">



**Next step:** Click **Next** to review the
**Filter users and devices** settings.


### Step 11: Configure User and Device Filtering

I proceeded to the **Filter users and devices** page in the
Microsoft Entra Connect Sync setup wizard.

I selected **Synchronize all users and devices** for the
**NMGM.com** forest. No group was specified for filtering,
so synchronization was not restricted to a selected pilot group.

**Purpose:** Include all eligible users and devices within the
previously configured directory scope, subject to synchronization rules.

**Screenshot:**

<img width="1000" alt="image" src="https://github.com/otraore26/NorthStar-Hybrid-Identity-AD-Entra-Sync/blob/1f9faa4a6e5dbe5c215ee3c899f7be44c7e22821/Screenshots/Step-11%20%20select-sync-all-users-and-devices.png">


**Next step:** Click **Next** to review and select the
**Optional features** for the lab.


### Step 12: Select Optional Synchronization Features

I proceeded to the **Optional features** page in the
Microsoft Entra Connect Sync setup wizard.

The following options were selected:

- **Password hash synchronization**
- **Password writeback**
- **Group writeback**

A warning icon appeared beside **Group writeback**, requiring
further review. This screenshot records the selected options
before configuration; it does not confirm successful operation.

**Purpose:** Specify the additional synchronization and writeback
features to include in the lab configuration.

**Screenshot:**

<img width="1000" alt="image" src="https://github.com/otraore26/NorthStar-Hybrid-Identity-AD-Entra-Sync/blob/1f9faa4a6e5dbe5c215ee3c899f7be44c7e22821/Screenshots/Step-12%20Optional-password-sync-and-writeback-settings.png">

**Next step:** Click **Next** to review the **Group Writeback**
configuration and any related warnings.


### Step 13: Review the Group Writeback Configuration and Warning

I proceeded to the **Group Writeback** page in the
Microsoft Entra Connect Sync setup wizard.

The **Group writeback forest** was set to **NMGM.com**.
The page displayed the available on-premises containers and
organizational units for the group writeback destination.

A warning stated that **NMGM.com did not have the Active Directory
schema for Exchange**. According to the warning, mail and Exchange
attributes would not be written back, limiting integration with
on-premises Exchange hybrid.

No destination was visibly selected, and the **Next** button
was disabled at this stage.

**Purpose:** Review the group writeback destination and identify
configuration limitations before continuing.

**Screenshot:**
<img width="1000" alt="image" src="https://github.com/otraore26/NorthStar-Hybrid-Identity-AD-Entra-Sync/blob/ace733280a2e09253a28d9a4a9048193eed2b883/Screenshots/Step-13%20%20group-writeback-exchange-schema-warning.png">

**Next step:** Review the warning, confirm the intended group
writeback destination, and document the configuration decision
before proceeding.
### Step 14: Provide Credentials for Single Sign-On

I proceeded to the **Enable single sign-on** page in the
Microsoft Entra Connect Sync setup wizard.

I provided domain administrator credentials for the **NMGM.com**
forest using **Enter credentials**.

A green check mark appeared beside the button, indicating that
the credentials were accepted. The **Next** button was enabled,
allowing me to continue.

**Purpose:** Provide the credentials required for the wizard
to configure the on-premises forest for single sign-on.

**Screenshot:**

<img width="1000" alt="image" src="https://github.com/otraore26/NorthStar-Hybrid-Identity-AD-Entra-Sync/blob/dda4e1de0d244fc145d308e7fc14530e352a7c5c/Screenshots/Step-14%20%20single-sign-on-credentials-accepted.png">

**Next step:** Click **Next** to review the final configuration
settings before installation.


### Step 15: Review the Final Synchronization Configuration

I proceeded to the **Ready to configure** page in the
Microsoft Entra Connect Sync setup wizard.

The configuration summary listed the following actions:

- Configure the synchronization services.
- Install the authentication agent and enable **Pass-through authentication**.
- Enable **Single sign-on**.
- Configure connectors for **NMGM.com** and **NMGM.onmicrosoft.com**.
- Configure the **Source Anchor Attribute**.
- Enable **Password hash synchronization**.
- Enable **Password writeback** and **Group writeback**.
- Enable the **Microsoft Entra ID Export Deletion Threshold (500)**.

The final summary showed **Pass-through authentication** as the
sign-in method, with **Password hash synchronization** also enabled.

**Start the synchronization process when configuration completes**
was checked. **Enable staging mode** was unchecked.

**Purpose:** Review the selected settings before applying the
configuration and starting synchronization.

**Screenshot:**

<img width="1000" alt="image" src="https://github.com/otraore26/NorthStar-Hybrid-Identity-AD-Entra-Sync/blob/4ad7d020987762ff89578877ed9acda6c4fd6651/Screenshots/Step-15%20Review-ready-to-configure-settings.png">

**Next step:** Click **Install** to apply the configuration,
then review the completion status and any warnings.

### Step 16: Confirm Configuration Completion

The Microsoft Entra Connect Sync wizard displayed
**Configuration complete**, confirming that configuration
succeeded and the synchronization process had been initiated.

The completion page also displayed the following information:

- **Active Directory Recycle Bin:** Not enabled for **NMGM.com**;
  enabling it was recommended.
- **Trusted Platform Module (TPM):** Recommended to improve
  the security of the synchronization server.
- **Source anchor:** Configured to use **mS-DS-ConsistencyGuid**.
- **Seamless SSO:** Additional configuration through
  **Group Policy** was required for the user sign-in experience.

This screenshot confirms successful configuration and the start
of synchronization. Validation of synchronized identities is
documented in the following steps.

**Purpose:** Record the configuration result and identify
follow-up configuration and validation tasks.

**Screenshot:**

<img width="1000" alt="image" src="https://github.com/otraore26/NorthStar-Hybrid-Identity-AD-Entra-Sync/blob/4ad7d020987762ff89578877ed9acda6c4fd6651/Screenshots/Step-16%20Entra-connect-configuration-complete.png">

**Next step:** Click **Exit**, open the Microsoft Entra admin
center, and verify the synchronization status and test identities.


### Step 17: Confirm Microsoft Entra Connect Is Enabled

I opened the **Microsoft Entra admin center** and reviewed
the tenant dashboard after completing the configuration.

The **Tenant status** card displayed
**Microsoft Entra Connect: Enabled** with a green check mark.

The dashboard also showed the following tenant totals:

- **16 users**
- **13 groups**
- **1 device**
- **1 application**

These totals represent objects in the tenant. They do not
confirm that every object was synchronized from on-premises
Active Directory.

**Purpose:** Confirm that the tenant recognizes Microsoft
Entra Connect as enabled following configuration.

**Screenshot:**


<img width="1000" alt="image" src="https://github.com/otraore26/NorthStar-Hybrid-Identity-AD-Entra-Sync/blob/4ad7d020987762ff89578877ed9acda6c4fd6651/Screenshots/Step-17%20Entra-dashboard-connect-enabled.png">


**Next step:** Open **View Entra Connect** to review the latest
synchronization status, then inspect test users and groups
to verify their synchronization source and expected attributes

### Step 18: Verify Synchronized Users in Microsoft Entra ID

I navigated to **Entra ID → Users → All users** in the
Microsoft Entra admin center.

The page displayed **16 users found**. Visible test accounts,
including **James Whitfield**, **Jane Cooper**, and **Karen Mills**,
showed **Yes** in the **On-premises sync enabled** column,
confirming their synchronization from on-premises Active Directory.

My **Ousmane Traore** account showed **No** in the same column,
distinguishing it from the synchronized test accounts.

**Purpose:** Verify that test users appear in Microsoft Entra ID
and confirm their on-premises synchronization status.

**Screenshot:**
<img width="1000" alt="image" src="https://github.com/otraore26/NorthStar-Hybrid-Identity-AD-Entra-Sync/blob/06f6e22bcb3429141b8a5b43bc28c54aff8b99de/Screenshots/Step-18%20%20Synchronized%20Users%20in%20Microsoft%20Entra%20ID.png">


### Step 19: Review Department Groups in Microsoft Entra ID

I navigated to **Entra ID → Groups → All groups** in the
Microsoft Entra admin center.

The page displayed **13 groups found**, including the following
department groups with the group type **Security**:

- **Finance-Users**
- **HR-Users**
- **IT-Users**
- **Operations-Users**

This screenshot confirms that the department groups are present
in Microsoft Entra ID. Their synchronization source and
membership require verification in each group's properties.

**Purpose:** Confirm that the expected department security
groups are visible in the cloud directory.

**Screenshot:**

<img width="1000" alt="image" src="https://github.com/otraore26/NorthStar-Hybrid-Identity-AD-Entra-Sync/blob/9f450089323c304e192ed58d1ca9b277b6c4dce6/Screenshots/Screenshot%202026-10-11%20010256.png">


**Next step:** Open a department group's properties to verify
its on-premises synchronization status, then compare its
members with the corresponding Active Directory group.


### Step 20: Verify the HR-Users Group Synchronization Source

I opened **Groups → All groups → HR-Users** in the
Microsoft Entra admin center and reviewed the **Overview** page.

The group displayed the following details:

- **Source:** Windows Server AD
- **Type:** Security
- **Membership type:** Assigned
- **Total direct members:** 4
- **Users:** 4
- **Groups and devices:** 0

The **Windows Server AD** source confirms that **HR-Users**
is synchronized from the on-premises directory. The overview
also confirms that the cloud group contains four user members.

**Purpose:** Verify the HR group's on-premises origin,
group type, and membership count in Microsoft Entra ID.

**Screenshot:**

<img width="1000" alt="image" src="https://github.com/otraore26/NorthStar-Hybrid-Identity-AD-Entra-Sync/blob/7ef4767eac03cbe2ff8fa527cc6a5824beeb9aad/Screenshots/HR%20Users.png">

**Next step:** Open **Members** and compare the four listed
users with the membership of **HR-Users** in Active Directory
to validate membership consistency.
