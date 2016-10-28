---
title: Smart Card Group Policy and Registry Settings
description: "Windows Server Security"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-smart-cards
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 125c6279-4b20-4c12-95f1-7083461fe965
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
---
# Smart Card Group Policy and Registry Settings

>Applies To: Windows Server&reg; 2016, Windows Server&reg; 2012 R2, Windows Server&reg; 2012

This topic for the IT professional and smart card developer describes the Group Policy settings, registry key settings, local security policy settings, and credential delegation policy settings that are available for configuring smart cards.

The following sections and tables list the smart card-related Group Policy settings and registry keys that can be set on a per-computer basis. If you use domain Group Policy Objects (GPOs), you can edit and apply Group Policy settings to local or domain computers.

-   [Primary Group Policy settings for smart cards](#BKMK_1)

    -   [Allow certificates with no extended key usage certificate attribute](#BKMK_AllowCertificatesWithNoExtendedKeyUsageCertificateAttribute)

    -   [Allow ECC certificates to be used for logon and authentication](#BKMK_AllowECCCertificatesToBeUsedForLogonAndAuthentication)

    -   [Allow Integrated Unblock screen to be displayed at the time of logon](#BKMK_AllowIntegratedUnblockScreenToBeDisplayedAtTheTimeOfLogon)

    -   [Allow signature keys valid for Logon](#BKMK_AllowSignatureKeysValidForLogon)

    -   [Allow time invalid certificates](#BKMK_AllowTimeInvalidCertificates)

    -   [Allow user name hint](#BKMK_AllowUserNameHint)

    -   [Configure root certificate clean up](#BKMK_ConfigureRootCertificateCleanUp)

    -   [Display string when smart card is blocked](#BKMK_DisplayStringWhenSmartCardIsBlocked)

    -   [Filter duplicate logon certificates](#BKMK_FilterDuplicateLogonCertificates)

    -   [Force the reading of all certificates from the smart card](#BKMK_ForceTheReadingOfAllCertificatesFromTheSmartCard)

    -   [Notify user of successful smart card driver installation](#BKMK_NotifyUserOfSuccessfulSmartCardDriverInstallation)

    -   [Prevent plaintext PINs from being returned by Credential Manager](#BKMK_PreventPlaintextPINsFromBeingReturnedByCredentialManager)

    -   [Reverse the subject name stored in a certificate when displaying](#BKMK_ReverseTheSubjectNameStoredInaCertificateWhenDisplaying)

    -   [Turn on certificate propagation from smart card](#BKMK_TurnOnCertificatePropagationFromSmartCard)

    -   [Turn on root certificate propagation from smart card](#BKMK_TurnOnRootCertificatePropagationFromSmartCard)

    -   [Turn on Smart Card Plug and Play service](#BKMK_TurnOnSmartCardPlugAndPlayService)

-   [Base CSP and KSP registry keys](#BKMK_2)

-   [CRL checking registry keys](#BKMK_3)

-   [Additional smart card Group Policy settings and registry keys](#BKMK_4)

## <a name="BKMK_1"></a>Primary Group Policy settings for smart cards
The following smart card Group Policy settings are located in Computer Configuration\Administrative Templates\Windows Components\Smart Card.

The registry keys are in the following locations:

-   HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\SmartCardCredentialProvider

-   HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\CertProp

> [!NOTE]
> Smart card reader registry information is located in HKEY_LOCAL_MACHINE\Software\Microsoft\Cryptography\Calais\Readers.
> 
> Smart card registry information is located in HKEY_LOCAL_MACHINE\Software\Microsoft\Cryptography\Calais\SmartCards.

The following table lists the default values for these GPO settings. Variations are documented under the policy descriptions in this topic.

|Server Type or GPO|Default Value|
|-----------|---------|
|Default Domain Policy|Not configured|
|Default Domain Controller Policy|Not configured|
|Stand-Alone Server Default Settings|Not configured|
|Domain Controller Effective Default Settings|Disabled|
|Member Server Effective Default Settings|Disabled|
|Client Computer Effective Default Settings|Disabled|

### <a name="BKMK_AllowCertificatesWithNoExtendedKeyUsageCertificateAttribute"></a>Allow certificates with no extended key usage certificate attribute
This policy setting allows certificates without an enhanced key usage (EKU) set to be used for sign in.

> [!NOTE]
> Enhanced key usage certificate attribute is also known as extended key usage.

In versions of Windows prior to Windows Vista, smart card certificates that are used to sign in require an EKU extension with a smart card logon object identifier. This policy setting can be used to modify that restriction.

When this policy setting is enabled, certificates with the following attributes can also be used to sign in with a smart card:

-   Certificates with no EKU

-   Certificates with an All Purpose EKU

-   Certificates with a Client Authentication EKU

When this policy setting is disabled or not configured, only certificates that contain the smart card logon object identifier can be used to sign in with a smart card.

|Item|Description|
|----|--------|
|Registry key|AllowCertificatesWithNoEKU|
|Applicable operating system versions|This policy applies to those versions designated in the **Applies To** list at the beginning of this topic.|
|Default values|No changes per operating system versions<br /><br />Disabled and not configured are equivalent|
|Policy management|Restart requirement: None<br /><br />Sign off requirement: None<br /><br />Policy conflicts: None|
|Notes and resources||

### <a name="BKMK_AllowECCCertificatesToBeUsedForLogonAndAuthentication "></a>Allow ECC certificates to be used for logon and authentication
This policy setting allows you to control whether elliptic curve cryptography (ECC) certificates on a smart card can be used to sign in to a domain. When this setting is enabled, ECC certificates on a smart card can be used to sign in to a domain. When this setting is disabled or not configured, ECC certificates on a smart card cannot be used to sign in to a domain.

|Item|Description|
|----|--------|
|Registry key|EnumerateECCCerts|
|Applicable operating system versions|This policy applies to those versions designated in the **Applies To** list at the beginning of this topic excluding Windows Server 2008 and Windows Vista.|
|Default values|No changes per operating system versions<br /><br />Disabled and not configured are equivalent|
|Policy management|Restart requirement: None<br /><br />Sign off requirement: None<br /><br />Policy conflicts: None|
|Notes and resources|This policy setting only affects a user's ability to sign in to a domain. ECC certificates on a smart card that are used for other applications, such as document signing, are not affected by this policy setting.<br /><br />If you use an ECDSA key to sign in, you must also have an associated ECDH key to permit sign-in when you are not connected to the network.|

### <a name="BKMK_AllowIntegratedUnblockScreenToBeDisplayedAtTheTimeOfLogon"></a>Allow Integrated Unblock screen to be displayed at the time of logon
This policy setting lets you determine whether the integrated unblock feature is available in the sign-in user interface (UI). The feature was introduced as a standard feature in the Credential Security Support Provider in Windows Vista.

When this setting is enabled, the integrated unblock feature is available. When this setting is disabled or not configured, the feature is not available.

|Item|Description|
|----|--------|
|Registry key|AllowIntegratedUnblock|
|Applicable operating system versions|This policy applies to those versions designated in the **Applies To** list at the beginning of this topic.|
|Default values|No changes per operating system versions<br /><br />Disabled and not configured are equivalent|
|Policy management|Restart requirement: None<br /><br />Sign off requirement: None<br /><br />Policy conflicts: None|
|Notes and resources|To use the integrated unblock feature, the smart card must support it. Check with the hardware manufacturer to verify that the smart card supports this feature.<br /><br />You can create a custom message that is displayed when the smart card is blocked by configuring the policy setting [Display string when smart card is blocked](Smart-Card-Group-Policy-and-Registry-Settings.md#BKMK_DisplayStringWhenSmartCardIsBlocked).|

### <a name="BKMK_AllowSignatureKeysValidForLogon"></a>Allow signature keys valid for Logon
This policy setting lets you allow signature key-based certificates to be enumerated and available for sign in. When this setting is enabled, any certificates available on the smart card with a signature-only key are listed on the sign-in screen. When this setting is disabled or not configured, certificates available on the smart card with a signature-only key are not listed on the sign-in screen.

|Item|Description|
|----|--------|
|Registry key|AllowSignatureOnlyKeys|
|Applicable operating system versions|This policy applies to those versions designated in the **Applies To** list at the beginning of this topic.|
|Default values|No changes per operating system versions<br /><br />Disabled and not configured are equivalent|
|Policy management|Restart requirement: None<br /><br />Sign off requirement: None<br /><br />Policy conflicts: None|
|Notes and resources||

### <a name="BKMK_AllowTimeInvalidCertificates"></a>Allow time invalid certificates
This policy setting permits those certificates that are expired or not yet valid to be displayed for sign-in.

Prior to Windows Vista, certificates were required to contain a valid time and to not expire. To be used, the certificate must be accepted by the domain controller. This policy setting only controls which certificates are displayed on the client computer.

When this setting is enabled, certificates are listed on the sign-in screen whether they have an invalid time or their time validity has expired. When this setting is disabled or not configured, certificates that are expired or not yet valid are not listed on the sign-in screen.

|Item|Description|
|----|--------|
|Registry key|AllowTimeInvalidCertificates|
|Applicable operating system versions|This policy applies to those versions designated in the **Applies To** list at the beginning of this topic.|
|Default values|No changes per operating system versions<br /><br />Disabled and not configured are equivalent|
|Policy management|Restart requirement: None<br /><br />Sign off requirement: None<br /><br />Policy conflicts: None|
|Notes and resources||

### <a name="BKMK_AllowUserNameHint"></a>Allow user name hint
This policy setting lets you determine whether an optional field is displayed during sign-in and provides a subsequent elevation process that allows users to enter their user name or user name and domain, which associates a certificate with the user. If this setting is enabled, an optional field is displayed that allows users to enter their user name or user name and domain. If this setting is disabled or not configured, the field is not displayed.

|Item|Description|
|----|--------|
|Registry key|X509HintsNeeded|
|Applicable operating system versions|This policy applies to those versions designated in the **Applies To** list at the beginning of this topic.|
|Default values|No changes per operating system versions<br /><br />Disabled and not configured are equivalent|
|Policy management|Restart requirement: None<br /><br />Sign off requirement: None<br /><br />Policy conflicts: None|
|Notes and resources||

### <a name="BKMK_ConfigureRootCertificateCleanUp"></a>Configure root certificate clean up
This policy setting allows you to manage the cleanup behavior of root certificates. Certificates are verified by using a trust chain, and the trust anchor for the digital certificate is the Root Certification Authority (CA). A CA can issue multiple certificates with the root certificate as the top certificate of the tree structure. A private key is used to sign other certificates. This creates an inherited trustworthiness for all certificates immediately under the root certificate. When this setting is enabled, you can set the following cleanup options:

-   **No cleanup**. When the user signs out or removes the smart card, the root certificates used during their session persist on the computer.

-   **Clean up certificates on smart card removal**. When the smart card is removed, the root certificates are removed.

-   **Clean up certificates on log off**. When the user signs out of Windows, the root certificates are removed.

When this policy setting is disabled or not configured, root certificates are automatically removed when the user signs out of Windows.

|Item|Description|
|----|--------|
|Registry key|RootCertificateCleanupOption|
|Applicable operating system versions|This policy applies to those versions designated in the **Applies To** list at the beginning of this topic.|
|Default values|No changes per operating system versions<br /><br />Disabled and not configured are equivalent|
|Policy management|Restart requirement: None<br /><br />Sign off requirement: None<br /><br />Policy conflicts: None|
|Notes and resources||

### <a name="BKMK_DisplayStringWhenSmartCardIsBlocked"></a>Display string when smart card is blocked
When this policy setting is enabled, you can create and manage the displayed message that the user sees when a smart card is blocked. When this setting is disabled or not configured (and the integrated unblock feature is also enabled), the system???s default message is displayed to the user when the smart card is blocked.

|Item|Description|
|----|--------|
|Registry key|IntegratedUnblockPromptString|
|Applicable operating system versions|This policy applies to those versions designated in the **Applies To** list at the beginning of this topic.|
|Default values|No changes per operating system versions<br /><br />Disabled and not configured are equivalent|
|Policy management|Restart requirement: None<br /><br />Sign off requirement: None<br /><br />Policy conflicts: This policy setting is only effective when the [Allow Integrated Unblock screen to be displayed at the time of logon](Smart-Card-Group-Policy-and-Registry-Settings.md#BKMK_AllowIntegratedUnblockScreenToBeDisplayedAtTheTimeOfLogon) policy is enabled.|
|Notes and resources||

### <a name="BKMK_FilterDuplicateLogonCertificates"></a>Filter duplicate logon certificates
This policy setting lets you use a filtering process to configure which valid sign-in certificates are displayed. During the certificate renewal period, a user???s smart card can have multiple valid sign-in certificates issued from the same certificate template, which can cause confusion about which certificate to select. This behavior can occur when a certificate is renewed and the old certificate has not expired yet.

Two certificates are determined to be the same if they are issued from the same template with the same major version and they are for the same user (this is determined by their UPN). When this policy setting is enabled, filtering occurs so that the user will only see the most current valid certificates from which to select. If this setting is disabled or not configured, all the certificates are displayed to the user.

This policy setting is applied to the computer after the [Allow time invalid certificates](Smart-Card-Group-Policy-and-Registry-Settings.md#BKMK_AllowTimeInvalidCertificates) policy setting is applied.

|Item|Description|
|----|--------|
|Registry key|FilterDuplicateCerts|
|Applicable operating system versions|This policy applies to those versions designated in the **Applies To** list at the beginning of this topic.|
|Default values|No changes per operating system versions<br /><br />Disabled and not configured are equivalent|
|Policy management|Restart requirement: None<br /><br />Sign off requirement: None<br /><br />Policy conflicts: None|
|Notes and resources|If there are two or more of the same certificates on a smart card and this policy setting is enabled, the certificate that is used to sign in to computers running Windows 2000, Windows XP, or Windows Server 2003 will be displayed. Otherwise, the certificate with the most distant expiration time will be displayed.|

### <a name="BKMK_ForceTheReadingOfAllCertificatesFromTheSmartCard"></a>Force the reading of all certificates from the smart card
This policy setting allows you to manage how Windows reads all certificates from the smart card for sign-in. During sign in, Windows reads only the default certificate from the smart card unless it supports retrieval of all certificates in a single call. This policy setting forces Windows to read all the certificates from the smart card.

When this policy setting is enabled, Windows attempts to read all certificates from the smart card regardless of the CSP feature set. When disabled or not configured, Windows attempts to read only the default certificate from smart cards that do not support retrieval of all certificates in a single call. Certificates other than the default are not available for sign in.

|Item|Description|
|----|--------|
|Registry key|ForceReadingAllCertificates|
|Applicable operating system versions|This policy applies to those versions designated in the **Applies To** list at the beginning of this topic.|
|Default values|No changes per operating system versions<br /><br />Disabled and not configured are equivalent|
|Policy management|Restart requirement: None<br /><br />Sign off requirement: None<br /><br />Policy conflicts: None **Important:** Enabling this policy setting can adversely impact performance during the sign in process in certain situations.|
|Notes and resources|Contact the smart card vendor to determine if your smart card and associated CSP support the required behavior.|

### <a name="BKMK_NotifyUserOfSuccessfulSmartCardDriverInstallation"></a>Notify user of successful smart card driver installation
This policy setting allows you to control whether a confirmation message is displayed to the user when a smart card device driver is installed. When this policy setting is enabled, a confirmation message is displayed when a smart card device driver is installed. When this setting is disabled or not configured, a smart card device driver installation message is not displayed.

|Item|Description|
|----|--------|
|Registry key|ScPnPNotification|
|Applicable operating system versions|This policy applies to those versions designated in the **Applies To** list at the beginning of this topic excluding Windows Server 2008 and Windows Vista.|
|Default values|No changes per operating system versions<br /><br />Disabled and not configured are equivalent|
|Policy management|Restart requirement: None<br /><br />Sign off requirement: None<br /><br />Policy conflicts: None|
|Notes and resources|This policy setting applies only to smart card drivers that have passed the Windows Hardware Quality Labs (WHQL) testing process.|

### <a name="BKMK_PreventPlaintextPINsFromBeingReturnedByCredentialManager"></a>Prevent plaintext PINs from being returned by Credential Manager
This policy setting prevents Credential Manager from returning plaintext PINs. Credential Manager is controlled by the user on the local computer, and it stores credentials from supported browsers and Windows applications. Credentials are saved in special encrypted folders on the computer under the user???s profile. When this policy setting is enabled, Credential Manager does not return a plaintext PIN. When this setting is disabled or not configured, plaintext PINs can be returned by Credential Manager.

|Item|Description|
|----|--------|
|Registry key|DisallowPlaintextPin|
|Applicable operating system versions|This policy applies to those versions designated in the **Applies To** list at the beginning of this topic excluding Windows Vista. This policy was introduced in Windows Vista SP1.|
|Default values|No changes per operating system versions<br /><br />Disabled and not configured are equivalent|
|Policy management|Restart requirement: None<br /><br />Sign off requirement: None<br /><br />Policy conflicts: None|
|Notes and resources|If this policy setting is enabled, some smart cards may not work in computers running Windows. Consult the smart card manufacturer to determine whether this policy setting should be enabled.|

### <a name="BKMK_ReverseTheSubjectNameStoredInaCertificateWhenDisplaying"></a>Reverse the subject name stored in a certificate when displaying
When this policy setting is enabled, it causes the display of the subject name to be reversed from the way it is stored in the certificate during the sign-in process.

To help users distinguish one certificate from another, the user principal name (UPN) and the common name are displayed by default. For example, when this setting is enabled, if the certificate subject is CN=User1, OU=Users, DN=example, DN=com and the UPN is user1@example.com, "User1" is displayed with "user1@example.com." If the UPN is not present, the entire subject name is displayed. This setting controls the appearance of that subject name, and it might need to be adjusted for your organization.

|Item|Description|
|----|--------|
|Registry key|ReverseSubject|
|Applicable operating system versions|This policy applies to those versions designated in the **Applies To** list at the beginning of this topic.|
|Default values|No changes per operating system versions<br /><br />Disabled and not configured are equivalent|
|Policy management|Restart requirement: None<br /><br />Sign off requirement: None<br /><br />Policy conflicts: None|
|Notes and resources||

### <a name="BKMK_TurnOnCertificatePropagationFromSmartCard"></a>Turn on certificate propagation from smart card
This policy setting allows you to manage the certificate propagation that occurs when a smart card is inserted. The certificate propagation service applies when a signed-in user inserts a smart card in a reader that is attached to the computer. This action causes the certificate to be read from the smart card. The certificates are then added to the user's Personal store.

If you enable or do not configure this policy setting, certificate propagation occurs when the user inserts the smart card. When this setting is disabled, certificate propagation does not occur and the certificates will not be made available to applications such as Outlook.

|Item|Description|
|----|--------|
|Registry key|CertPropEnabled|
|Applicable operating system versions|This policy applies to those versions designated in the **Applies To** list at the beginning of this topic.|
|Default values|No changes per operating system versions<br /><br />Enabled and not configured are equivalent|
|Policy management|Restart requirement: None<br /><br />Sign off requirement: None<br /><br />Policy conflicts: This policy setting must be enabled to allow the [Turn on root certificate propagation from smart card](Smart-Card-Group-Policy-and-Registry-Settings.md#BKMK_TurnOnRootCertificatePropagationFromSmartCard) setting to work when it is enabled.|
|Notes and resources||

### <a name="BKMK_TurnOnRootCertificatePropagationFromSmartCard"></a>Turn on root certificate propagation from smart card
This policy setting allows you to manage the root certificate propagation that occurs when a smart card is inserted. The certificate propagation service applies when a signed-in user inserts a smart card in a reader that is attached to the computer. This action causes the certificate to be read from the smart card. The certificates are then added to the user's Personal store. When this policy setting is enabled or not configured, root certificate propagation occurs when the user inserts the smart card.

|Item|Description|
|----|--------|
|Registry key|EnableRootCertificate Propagation|
|Applicable operating system versions|This policy applies to those versions designated in the **Applies To** list at the beginning of this topic.|
|Default values|No changes per operating system versions<br /><br />Enabled and not configured are equivalent|
|Policy management|Restart requirement: None<br /><br />Sign off requirement: None<br /><br />Policy conflicts: For this policy setting to work, the [Turn on certificate propagation from smart card](Smart-Card-Group-Policy-and-Registry-Settings.md#BKMK_TurnOnCertificatePropagationFromSmartCard) policy setting must also be enabled.|
|Notes and resources||

### <a name="BKMK_TurnOnSmartCardPlugAndPlayService"></a>Turn on Smart Card Plug and Play service
This policy setting allows you to control whether Smart Card Plug and Play is enabled. This means that your users can use smart cards from vendors who have published their drivers through Windows Update without needing special middleware. These drivers will be downloaded in the same way as drivers for other devices in Windows. If an appropriate driver is not available from Windows Update, a PIV-compliant minidriver that is included with any of the supported versions of Windows is used for these cards.

When the Smart Card Plug and Play policy setting is enabled or not configured, and the system attempts to install a smart card device driver the first time a smart card is inserted in a smart card reader. If this policy setting is disabled a device driver is not installed when a smart card is inserted in a smart card reader.

|Item|Description|
|----|--------|
|Registry key|EnableScPnP|
|Applicable operating system versions|This policy applies to those versions designated in the **Applies To** list at the beginning of this topic excluding Windows Server 2008 and Windows Vista.|
|Default values|No changes per operating system versions<br /><br />Enabled and not configured are equivalent|
|Policy management|Restart requirement: None<br /><br />Sign off requirement: None<br /><br />Policy conflicts: None|
|Notes and resources|This policy setting applies only to smart card drivers that have passed the Windows Hardware Quality Labs (WHQL) testing process.|

## <a name="BKMK_2"></a>Base CSP and Smart Card KSP registry keys
The following registry keys can be configured for the base cryptography service provider (CSP) and the smart card key storage provider (KSP). The following tables list the keys. All keys use the DWORD type.

The registry keys for the Base CSP are located in the registry in HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\Defaults\Provider\Microsoft Base Smart Card Crypto Provider.

The registry keys for the smart card KSP are located in HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Cryptography\Providers\Microsoft Smart Card Key Storage Provider.

### Registry keys for the base CSP and smart card KSP

|Registry Key|Description|
|--------|--------|
|**AllowPrivateExchangeKeyImport**|A non-zero value allows RSA exchange (for example, encryption) private keys to be imported for use in key archival scenarios.<br /><br />Default value: 00000000|
|**AllowPrivateSignatureKeyImport**|A non-zero value allows RSA signature private keys to be imported for use in key archival scenarios.<br /><br />Default value: 00000000|
|**DefaultPrivateKeyLenBits**|Defines the default length for private keys, if desired.<br /><br />Default value: 00000400<br /><br />Default key generation parameter: 1024-bit keys|
|**RequireOnCardPrivateKeyGen**|This key sets the flag that requires on-card private key generation (default). If this value is set, a key generated on a host can be imported into the smart card. This is used for smart cards that do not support on-card key generation or where key escrow is required.<br /><br />Default value: 00000000|
|**TransactionTimeoutMilliseconds**|Default timeout values allow you to specify whether transactions that take an excessive amount of time will fail.<br /><br />Default value: 000005dc1500<br /><br />The default timeout for holding transactions to the smart card is 1.5 seconds.|

### Additional registry keys for the smart card KSP

|Registry Key|Description|
|--------|--------|
|**AllowPrivateECDHEKeyImport**|This value allows Ephemeral Elliptic Curve Diffie-Hellman (ECDHE) private keys to be imported for use in key archival scenarios.<br /><br />Default value: 00000000|
|**AllowPrivateECDSAKeyImport**|This value allows Elliptic Curve Digital Signature Algorithm (ECDSA) private keys to be imported for use in key archival scenarios.<br /><br />Default value: 00000000|

## <a name="BKMK_3"></a>CRL checking registry keys
The following table lists the keys and the corresponding values to turn off certificate revocation list (CRL) checking at the Key Distribution Center (KDC) or client. To manage CRL checking, you need to configure settings for both the KDC and the client.

### CRL checking registry keys

|Registry Key|Details|
|--------|------|
|HKEY_LOCAL_MACHINE\SYSTEM\CCS\Services\Kdc\UseCachedCRLOnlyAndIgnoreRevocationUnknownErrors|Type = DWORD<br /><br />Value = 1|
|HKEY_LOCAL_MACHINE\SYSTEM\CCS\Control\LSA\Kerberos\Parameters\UseCachedCRLOnlyAndIgnoreRevocationUnknownErrors|Type = DWORD<br /><br />Value = 1|

## <a name="BKMK_4"></a>Additional smart card Group Policy settings and registry keys
In a smart card deployment, additional Group Policy settings can be used to enhance ease-of-use or security. Two of these policy settings that can complement a smart card deployment are:

-   Turning off delegation for computers

-   Interactive logon: Do not require CTRL+ALT+DEL (not recommended)

The following smart card-related Group Policy settings are located in Computer Configuration\Windows Settings\Security Settings\Local Policies\Security Options.

### Local security policy settings

|Group Policy Setting|Registry Key|Default|Description|
|------------|--------|------|--------|
|[Interactive logon: Require smart card](../group-managed-service-accounts/security-options/Interactive-logon-Require-smart-card.md)|scforceoption|Disabled|This security policy setting requires users to sign in to a computer by using a smart card.<br /><br />**Enabled** Users can only sign in to the computer by using a smart card.<br /><br />**Disabled** Users can sign in to the computer by using any method.|
|[Interactive logon: Smart card removal behavior](../group-managed-service-accounts/security-options/Interactive-logon-Smart-card-removal-behavior.md)|scremoveoption|This policy setting is not defined, which means that the system treats it as **No Action**.|This setting determines what happens when the smart card for a signed-in user is removed from the smart card reader. The options are:<br /><br />-   **No Action**<br />-   **Lock Workstation** The workstation is locked when the smart card is removed, allowing users to leave the area, take their smart card with them, and still maintain a protected session.<br />-   **Force Logoff** The user is automatically signed out when the smart card is removed.<br />-   **Disconnect if a Remote Desktop Services session** Removal of the smart card disconnects the session without signing out the user. This allows the user to reinsert the smart card and resume the session later, or at another computer that is equipped with a smart card reader, without having to sign in again. If the session is local, this policy setting functions identically to the **Lock Workstation** option. **Note:**     Remote Desktop Services was called Terminal Services in previous versions of Windows Server.|

From the Local Security Policy Editor (secpol.msc), you can edit and apply system policies to manage credential delegation for local or domain computers.

The following smart card-related Group Policy settings are located in Computer Configuration\Administrative Templates\System\Credentials Delegation.

Registry keys are located in HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Lsa\Credssp\PolicyDefaults.

> [!NOTE]
> In the following table, fresh credentials are those that you are prompted for when running an application.

### Credential delegation policy settings

|Group Policy Setting|Registry Key|Default|Description|
|------------|--------|------|--------|
|**Allow Delegating Fresh Credentials**|AllowFreshCredentials|Not Configured|This policy setting applies:<br /><br />-   When server authentication was achieved through a trusted X509 certificate or Kerberos protocol.<br />-   To applications that use the CredSSP component (for example, Remote Desktop Services).<br /><br />**Enabled** You can specify the servers where the user's fresh credentials can be delegated.<br /><br />**Not Configured** After proper mutual authentication, delegation of fresh credentials is permitted to Remote Desktop Services running on any computer.<br /><br />**Disabled** Delegation of fresh credentials to any computer is not permitted. **Note:** This policy setting can be set to one or more service principal names (SPNs). The SPN represents the target server where the user credentials can be delegated. A single wildcard character is permitted when specifying the SPN, for example:<ul><li>Use *TERMSRV/\** for Remote Desktop Session Host (RD Session Host) running on any computer.</li><li>Use *TERMSRV/host.humanresources.fabrikam.com* for RD Session Host running on the host.humanresources.fabrikam.com computer.</li><li>Use *TERMSRV/\*.humanresources.fabrikam.com* for RD Session Host running on all computers in .humanresources.fabrikam.com</li></ul>|
|**Allow Delegating Fresh Credentials with NTLM-only Server Authentication**|AllowFreshCredentialsWhenNTLMOnly|Not Configured|This policy setting applies:<br /><br />-   When server authentication was achieved by using NTLM.<br />-   To applications that use the CredSSP component (for example, Remote Desktop).<br /><br />**Enabled** You can specify the servers where the user's fresh credentials can be delegated.<br /><br />**Not Configured** After proper mutual authentication, delegation of fresh credentials is permitted to RD Session Host running on any computer (TERMSRV/\*).<br /><br />**Disabled** Delegation of fresh credentials is not permitted to any computer. **Note:** This policy setting can be set to one or more SPNs. The SPN represents the target server where the user credentials can be delegated. A single wildcard character (\*) is permitted when specifying the SPN.See the **Allow Delegating Fresh Credentials** policy setting description for examples.|
|**Deny Delegating Fresh Credentials**|DenyFreshCredentials|Not Configured|This policy setting applies to applications that use the CredSSP component (for example, Remote Desktop).<br /><br />**Enabled** You can specify the servers where the user's fresh credentials cannot be delegated.<br /><br />**Disabled** or **Not Configured** A server is not specified. **Note:** This policy setting can be set to one or more SPNs. The SPN represents the target server where the user credentials cannot be delegated. A single wildcard character (\*) is permitted when specifying the SPN.See the **Allow Delegating Fresh Credentials** policy setting description for examples.|

If you are using Remote Desktop Services with smart card logon, you cannot delegate default and saved credentials. The registry keys in the following table, which are located at HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Lsa\Credssp\PolicyDefaults, and the corresponding Group Policy settings are ignored.

|Registry key|Corresponding Group Policy setting|
|--------|-------------------|
|AllowDefaultCredentials|Allow Delegating Default Credentials|
|AllowDefaultCredentialsWhenNTLMOnly|Allow Delegating Default Credentials with NTLM-only Server Authentication|
|AllowSavedCredentials|Allow Delegating Saved Credentials|
|AllowSavedCredentialsWhenNTLMOnly|Allow Delegating Saved Credentials with NTLM-only Server Authentication|


