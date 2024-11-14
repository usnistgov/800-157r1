---
layout: default
title: Lifecycle Activities and Related Requirements
navOrder: 2
navTitle: Lifecycle
permalink: /lifecycle/
anchor: s-2
section: 2
---

# Life Cycle Activities and Related Requirements {#s-2}

*This section is normative.*

The life cycle activities for a derived PIV credential are initial issuance, maintenance, and termination. At a more detailed level, the life cycle activities for PKI-based and non-PKI-based derived PIV credentials differ considerably. This section describes these life cycle activities and provides requirements and recommendations as appropriate.

Issuers of derived PIV credentials **SHALL** document the process for each life cycle activity described below. In accordance with [[HSPD-12]](references.md#ref-HSPD-12), the reliability of the derived PIV credential issuer **SHALL** be established through an official accreditation process, as described in [[SP800-79]](referenced.md#ref-SP-800-79).

## Derived PIV Credential Life Cycle Activities {#s-2-1}

The derived PIV credential life cycle consists of the activities described above: initial issuance, maintenance, and termination. The activities at the manufacturer during fabrication and pre-personalization of the authenticator (as applicable) are not considered part of this life cycle model. [Figure 1](2_lifecycle.md#fig-1) presents the PKI-based derived PIV credential life cycle activities alongside the PIV Card life cycle activities. [Figure 2](2_lifecycle.md#fig-2) presents the corresponding life cycle activities for non-PKI-based derived PIV credentials.

[Figure 1. PKI-based derived PIV credential life cycle activities](2_lifecycle.md#fig-1){:name="fig-1"}
{:latex-ignore="true"}

![Flowchart of lifecycle activities associated with PKI-based derived PIV credentials]({{site.baseurl}}/{{page.collection}}/images/Fig2-1.png 'PKI-based derived PIV credential life cycle activities'){:latex-src="Fig2-1.pdf" latex-fig="1" latex-place="p"}

[Figure 2. Non-PKI-based derived PIV credential life cycle activities](2_lifecycle.md#fig-2){:name="fig-2"}
{:latex-ignore="true"}

![Flowchart of lifecycle activities associated with non-PKI-based derived PIV credentials]({{site.baseurl}}/{{page.collection}}/images/Fig2-2.png 'Non-PKI-based derived PIV credential life cycle activities'){:latex-src="Fig2-2.pdf" latex-fig="2" latex-place="p"}

The life cycle of a derived PIV credential begins with issuance on an approved device or authenticator associated with the applicant. This may be part of issuing a PIV Card or a subsequent process. Mobile devices with derived PIV credentials are managed, as described in [[SP800-124]](references.md#ref-SP-800-124).

The maintenance activities for a PKI-based derived PIV credential are the same as for other X.509 public key certificates. Certificate re-key is typically used to replace a certificate that is nearing expiration. Certificate modification replaces a certificate if information about the subscriber that appears on the certificate (e.g., their name) needs to be changed.

While non-PKI-based derived PIV credentials are not typically re-keyed and do not contain PII about the subscriber, they may require maintenance, such as replacing the activation secret or biometric factor used to activate the physical authenticator.  Instead of re-keying, the current non-PKI-based derived PIV credential **SHALL** be invalidated and the initial issuance process (except for the device or authenticator approval process) repeated to bind a new derived PIV credential. When a non-PKI-based derived PIV credential is lost, stolen, or damaged, the issuer **SHALL** invalidate the credential to prevent its further use.

When an authenticator with the private key that corresponds to a PKI-based derived PIV credential is lost, stolen, or damaged, the issuer **SHALL** prevent further use of the affected credential by either collecting and destroying the associated private key or revoking the associated certificate. These processes are described in [Sec. 2.4](2_lifecycle.md#s-2-4). If the subscriber becomes ineligible to possess a PIV Card, all derived PIV credentials for that subscriber are revoked or otherwise invalidated.

## Initial Issuance {#s-2-2}

Issuing a derived PIV credential is an instance of the post-enrollment binding of an authenticator described in [[SP800-63B]](references.md#ref-SP-800-63B). Issuance **SHALL** be performed in accordance with the requirements that apply to cryptographic authenticators and the requirements in this section. The term *issuance* is used when the device or authenticator is provided to the subscriber and when the device or authenticator is already in the subscriber's possession. [Appendix C](C_examples.md#s-c) provides sample issuance processes for derived PIV credentials.

Derived PIV credentials **SHALL** only be issued by the home agency of the associated PIV identity account or by a third-party organization or service provider (e.g., USAccess) authorized by the home agency. Derived PIV credentials **SHALL** only be issued to devices (e.g., mobile devices) or authenticators that are approved by the home agency. Agencies **MAY** establish blanket approvals for particular device types or **MAY** individually authorize specific devices or authenticators for issuance and use by a cardholder. Each issuer **SHALL** document its authorization policies for issuance.

Binding a derived PIV credential to a PIV identity account can be accomplished through a connection to a PIV-authenticated endpoint, a direct connection to the PIV Card, or the use of the external authenticator binding procedure described in [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 4.1.2.2. Derived PIV credentials **MAY** be issued remotely or in person. Except for derived PIV credential issuance as described in [Sec. 2.2.3](2_lifecycle.md#s-2-2-3), the binding **SHALL** require the cardholder to authenticate using their PIV Card with the PIV-AUTH authentication mechanism specified in [[FIPS201]](references.md#ref-FIPS201) Sec. 6.2.3.1. In addition to authenticating the cardholder, performing the PKI-AUTH authentication mechanism verifies that the applicant is currently eligible to possess a PIV Card. All derived PIV credentials **SHALL** be issued in accordance with [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 6.1.2.1.

Issuing agencies **SHALL** have a documented policy or process for determining the capabilities and basis for trust of the credentials they issue and the devices on which they will reside. All AAL3 derived PIV credentials **SHALL** only be issued  to devices that the home agency has determined to have been issued to the cardholder.

After the applicant has been authenticated, a derived PIV credential **MAY** be issued. The newly issued derived PIV credential **SHALL** be represented in the cardholder's PIV identity account. This implies that a third-party organization or service provider issuing derived PIV credentials needs to have access to the PIV identity account to meet this requirement.

 When a new derived PIV credential is associated with a PIV identity account, the issuer **SHALL** promptly notify the PIV cardholder. Notification **SHALL** be to an address associated with the cardholder's PIV identity account. More than one independent notification method **MAY** be used to ensure prompt receipt by the cardholder. Examples of these processes are given in [Appendix C](C_examples.md#s-c).

Derived PIV credentials **SHALL** meet the requirements for authentication assurance level (AAL) 2 or 3 specified in [[SP800-63B]](references.md#ref-SP-800-63B). Derived PIV credentials that meet AAL3 requirements also fulfill the requirements of AAL2 and can be used in circumstances that require authentication at AAL2. All derived PIV credentials at both AAL2 and AAL3 **SHALL** meet the requirements for phishing resistance defined in [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 3.2.5.

This guideline does not preclude issuing multiple derived PIV credentials to the same applicant based on the same PIV Card. However, this could increase the risk that one of the derived PIV credentials will be lost/stolen without the loss being reported or that the subscriber will inappropriately provide one to someone else. Accordingly, issuers **MAY** limit the number of active derived PIV credentials that a subscriber may have.

### PKI-Based Derived PIV Credential Issuance {#s-2-2-1}

Issuing a PKI-based derived PIV credential requires the generation of a public/private key pair followed by the creation of a corresponding authentication certificate by the certificate authority (CA). For a derived PIV credential capable of being used at AAL3, all of the following requirements apply:

* The cardholder **SHALL** be authenticated using the PIV-AUTH authentication mechanism specified in [[FIPS201]](references.md#ref-FIPS201).
* The key pair **SHALL** be generated in the device (authenticator or endpoint) that will house the derived PIV credential.
* The device **SHALL** send the certificate signing request containing the public key to the CA, which **SHALL** return an X.509 authentication certificate that **SHALL** be stored on the device (authenticator or endpoint).
* The CA **SHALL** retain a copy of the issued certificate for use should revocation be required.

For a derived PIV credential issued for use only at AAL2, the same procedure **MAY** be used, or the CA **SHALL** generate a key pair and corresponding certificate and send the certificate and private key to the device over an authenticated protected channel for installation. Following installation, the CA **SHALL** promptly and securely delete its copy of the private key.

The private key **SHALL** be stored on the device in a manner that makes it accessible only upon entry of the correct activation secret or presentation of a biometric factor that matches a stored biometric image or template. This **SHALL** be accomplished by using strong access controls for the stored private key or through decryption of the private key using an encryption key derived from the activation secret.

### Non-PKI-Based Derived PIV Credential Issuance {#s-2-2-2}

The applicant **SHALL** be provided with or supply an approved physical authenticator for the highest AAL that the derived PIV credential will be used to authenticate. If the issuer does not directly provide the authenticator, the issuer **SHALL** verify that the authenticator's characteristics (e.g., single-factor or multi-factor) meet the requirements of [[SP800-63B]](references.md#ref-SP-800-63B) for the highest authentication assurance level at which it will be used (AAL2 or AAL3), including [[FIPS140]](references.md#ref-FIPS140) requirements.

The issuance process for a multi-factor authenticator **SHALL** prompt the applicant to establish an activation secret or a biometric activation factor (or both) for the authenticator if not previously established and successfully authenticate using that authenticator. The issuance process with a single-factor authenticator **SHALL** prompt the applicant to register a password that meets the requirements of [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 3.1.1 and will be verified along with the physical authenticator in the authentication process.

### Derived PIV Issuance Without PIV Card {#s-2-2-3}

Some operational situations may motivate the issuance of a derived PIV credential when a PIV Card is unavailable. For example, it may be desirable to:

* Issue a derived PIV credential to a new subscriber in a field location where production facilities for PIV Cards are unavailable
* Issue a derived PIV credential to a cardholder who has forgotten to bring their PIV Card to work

In these and similar situations, one or more derived PIV credentials **MAY** be issued, subject to the following conditions.

The subscriber **SHALL** be issued a derived PIV credential only after all issuance requirements in [[FIPS201]](references.md#ref-FIPS201) Sec. 2.8 and 2.8.3 have been met (substituting "derived PIV credential" for "PIV Card" in those sections) and the PIV identity account has been established. Issuance **SHALL** be performed in person or at a supervised remote identity proofing station.

Since only PIV Cards (and not derived PIV credentials) can be used to bind additional derived PIV credentials, all derived PIV credentials expected to be needed **SHOULD** be issued at the same time. For example, the subscriber may need a mobile device and also a separate hardware token as derived PIV credentials.

Derived PIV credentials issued in this manner **MAY** also be enabled for physical access, as described in [Appendix D](D_pacs.md#s-d).

## Maintenance {#s-2-3}

The maintenance activities required for derived PIV credentials depend on the type of derived PIV credential (PKI-based or non-PKI-based) used. Maintenance activities include rekeying, modifying certificates, and replacing an activation factor (biometric or activation secret) as appropriate.

Derived PIV credentials are unaffected when the subscriber replaces their PIV Card with a new one (reissuance) or when it is lost, stolen, or damaged. The ability for the subscriber to use a derived PIV credential is beneficial while waiting for a new PIV Card to be issued. In such circumstances, the subscriber continues to be able to use the derived PIV credential to gain logical access to remote federally controlled information systems from their endpoint. 

Updating the activation factor (biometric or activation secret, such as a PIN) or resetting the activation retry count for a derived PIV credential **SHALL** be performed in accordance with [Sec. 3.1.4](3_requirements.md#s-3-1-4) for PKI-based derived PIV credentials or [Sec. 3.2.3](3_requirements.md#s-3-2-3) for non-PKI-based derived PIV credentials.

### PKI-Based Derived PIV Credential Maintenance {#s-2-3-1}

PKI-based derived PIV credentials require typical maintenance activities applicable to asymmetric cryptographic credentials, including rekeying and modification. These activities **MAY** be performed either remotely or in person and **SHALL** be conducted in accordance with the certificate policy under which the derived PIV authentication certificate is issued. When certificate rekeying or modification is performed remotely for a derived PIV credential, communication between the issuer and the cryptographic module in which the derived PIV authentication private key is stored **SHALL** only occur over mutually authenticated secure sessions between tested and validated cryptographic modules.

Certain maintenance activities for the subscriber's PIV Card trigger corresponding maintenance activities for the derived PIV credential. PKI-based derived PIV credentials **SHALL** be reissued if any information about the subscriber that appears in the credential changes. For example, if the subscriber's PIV Card is reissued as a result of a change in the subscriber's name and the subscriber's name appears in the derived PIV authentication certificate, a new derived PIV authentication certificate with the new name **SHALL** be issued and the previous certificate invalidated. The subscriber then uses their current PIV authentication certificate to authenticate to the issuer, which then updates the certificate in the derived PIV credential module.

~~~
\clearpage
~~~
{:latex-literal="true"}

### Non-PKI-Based Derived PIV Credential Maintenance

Maintenance activities for non-PKI-based derived PIV credentials are simpler than those for PKI-based derived PIV credentials since the former do not contain information about the cardholder nor carry a specific expiration date. Identity information **SHALL** be maintained in the PIV identity account and **SHALL** be updated when needed.

Updating a separate password used with a single-factor authenticator for use at AAL2 **SHALL** be performed in a mutually authenticated protected session with the home agency IdMS. The update **SHALL** require the entry of the current password. If resetting the password is required because the subscriber has forgotten the password or has reached the retry limit, it **SHALL** be done in accordance with [Sec. 3.2.3](3_requirements.md#s-3-2-3).

## Invalidation {#s-2-4}

When an authenticator associated with a derived PIV credential is compromised (e.g., lost, stolen, or damaged), that derived PIV credential **SHALL** be invalidated as described below.

All derived PIV credentials associated with a given PIV identity account **SHALL** be invalidated when that PIV identity account is terminated, typically due to the cardholder's loss of PIV credential eligibility. Issuers of derived PIV credentials **SHALL** continuously monitor the associated PIV identity account to determine its termination status. Meeting this requirement is simplified because the subject's PIV Card, credential eligibility, and all derived PIV credentials are maintained in one account &mdash; the PIV identity account &mdash; and maintained by the home agency IdMS.

If a PIV Card or derived PIV credential is invalidated due to loss or compromise, the home agency or issuer **SHOULD** check to see whether any derived PIV credentials have been recently (typically within the past seven days) bound to the PIV identity account and if so, determine whether they were appropriately issued to the subject. Termination of the PIV Card, which may occur due to loss or other compromise, does not usually require the invalidation of associated derived PIV credentials unless it is a result of termination of the associated PIV identity account.

The non-voluntary invalidation of a derived PIV credential **SHALL** be handled as specified in [[CSP]](references.md#ref-CSP).

### PKI-based Derived PIV Credential Invalidation {#s-2-4-1}

If the derived PIV authentication private key was created and stored on a hardware module that does not permit private key export and the token is collected and either zeroized or destroyed, then the derived PIV authentication certificate **SHOULD** be revoked. In all other cases, the derived PIV authentication certificate **SHALL** be revoked.

### Non-PKI-Based Derived PIV Credential Invalidation {#s-2-4-2}

Non-PKI-based derived PIV credentials are always directly verified by the home agency IdMS of the associated PIV Card. Therefore, termination of a non-PKI-based derived PIV credential **SHALL** be accomplished by invalidating the reference to the associated authenticator in the PIV identity account so that the authenticator cannot be used to authenticate to the home agency IdMS. Separate authenticators **MAY** be collected from the subscriber, but this is not required.
