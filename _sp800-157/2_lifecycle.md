---
layout: default
title: Lifecycle Activities and Related Requirements
navOrder: 2
navTitle: Lifecycle
permalink: /lifecycle/
anchor: s-2
section: 2
---

# Lifecycle Activities and Related Requirements {#s-2}

*This section is normative.*

The lifecycle activities for a derived PIV credential are initial issuance, maintenance, and termination. At a more detailed level, the lifecycle activities for PKI-based and non-PKI-based derived PIV credentials differ considerably from each other. This section describes these lifecycle activities and provides requirements and recommendations as appropriate.

Issuers of derived PIV credentials **SHALL** document the process for each of the lifecycle activities described below. In accordance with [[HSPD-12]](references.md#ref-HSPD-12), the reliability of the derived PIV credential issuer **SHALL** be established through an official accreditation process.

## Derived PIV Credential Lifecycle Activities {#s-2-1}

The derived PIV credential lifecycle consists of the three classes of activities described above. The activities that take place at the manufacturer during fabrication and pre-personalization of the authenticator (as applicable) are not considered part of this lifecycle model. [Figure 1](2_lifecycle.md#fig-1) presents the PKI-based derived PIV credential activities alongside the PIV Card lifecycle activities. [Figure 2](2_lifecycle.md#fig-2) presents the corresponding lifecycle activities for non-PKI-based derived PIV credentials.

[Figure 1. PKI-based derived PIV credential lifecycle activities](2_lifecycle.md#fig-1){:name="fig-1"}
{:latex-ignore="true"}

![Flowchart of lifecycle activities associated with PKI-based derived PIV credentials]({{site.baseurl}}/{{page.collection}}/images/Fig2-1.png 'PKI-based derived PIV credential lifecycle activities'){:latex-src="Fig2-1.pdf" latex-fig="1" latex-place="h"}

[Figure 2. Non-PKI-based derived PIV credential lifecycle activities](2_lifecycle.md#fig-2){:name="fig-2"}
{:latex-ignore="true"}

![Flowchart of lifecycle activities associated with non-PKI-based derived PIV credentials]({{site.baseurl}}/{{page.collection}}/images/Fig2-2.png 'Non-PKI-based derived PIV credential lifecycle activities'){:latex-src="Fig2-2.pdf" latex-fig="2" latex-place="h"}

The lifecycle of a derived PIV credential begins with the issuance of a derived PIV credential on an approved device or authenticator associated with the applicant. This may be part of the process of issuing a PIV Card or a subsequent process. Mobile devices with derived PIV credentials are managed as described in [[SP800-124]](references.md#ref-SP-800-124).

The maintenance activities for a PKI-based derived PIV credential are the same as for other X.509 public key certificates. Certificate re-key is typically used to replace a certificate that is nearing expiration. Certificate modification is used to replace a certificate if information about the subscriber that appears in the certificate, such as their name, needs to be changed.

While non-PKI-based derived PIV credentials are not typically re-keyed and do not contain PII about the subscriber, they may require maintenance, such as replacing the activation secret or biometric factor used to activate the physical authenticator.  Instead of re-keying, the current non-PKI-based derived PIV credential **SHALL** be invalidated and the initial issuance process (except for the device or authenticator approval process) repeated to bind a new derived PIV credential. When a non-PKI-based derived PIV credential is lost, stolen, or damaged, the issuer **SHALL** invalidate the credential to prevent its further use.

When an authenticator that contains the private key corresponding to a PKI-based derived PIV credential is lost, stolen, or damaged, the issuer **SHALL** prevent further use of the affected credential by either collecting and destroying the associated private key or by revoking the associated certificate. These processes are described in [Sec. 2.4](2_lifecycle.md#s-2-4). If the subscriber becomes ineligible to possess a PIV Card, all derived PIV credentials for that subscriber are revoked or otherwise invalidated.

## Initial Issuance {#s-2-2}

The issuance of a derived PIV credential is an instance of the post-enrollment binding of an authenticator described in [[SP800-63B]](references.md#ref-SP-800-63B). Issuance **SHALL** be performed in accordance with the requirements that apply to cryptographic authenticators as well as the requirements in this section. The term *issuance* is used in cases where the device or authenticator is provided to the subscriber as well as when the device or authenticator is already in the subscriber's possession. [Appendix C](C_examples.md#s_c) provides sample issuance processes for derived PIV credentials.

Derived PIV credentials **SHALL** be issued only by the home agency of the associated PIV identity account. Derived PIV credentials **SHALL** be issued only to devices (such as mobile devices) or authenticators that are approved by the home agency. Agencies **MAY** establish blanket approvals for particular device types or **MAY** individually authorize specific devices or authenticators for issuance and use by a cardholder. Authorization policies for issuance **SHALL** be documented by each issuer.

Derived PIV credentials **MAY** be issued remotely or in person. At the time of issuance, the applicant **SHALL** authenticate to the derived PIV credential issuer using their PIV Card. This authentication **SHALL** be performed using the PKI-AUTH authentication mechanism described in Sec. 6.2.3.1 of [[FIPS201]](references.md#ref-FIPS201). This authentication **MAY** be performed remotely. In addition to authenticating the cardholder, performing the PKI-AUTH authentication mechanism verifies that the applicant is currently eligible to possess a PIV Card. All derived PIV credentials **SHALL** be issued in accordance with [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 6.1.2.1.

All derived PIV credentials for use at AAL3 **SHALL** be issued in accordance with the following additional requirements. The applicant **SHALL** identify themself using a biometric sample that can be verified against their PIV Card or against the biometric information in their enrollment record. If the issuance process consists of two or more transactions, the applicant **SHALL** identify themself using a biometric sample that can be verified against either their PIV Card or against a biometric that was recorded in a previous transaction. The issuer **SHALL** retain the biometric sample used to verify the applicant for future reference.

After the applicant has been authenticated, a derived PIV credential **MAY** be issued and associated with the cardholder's PIV identity account. The newly issued derived PIV credential **SHALL** be represented in the cardholder's PIV identity account.

 When a new derived PIV credential is associated with a PIV identity account, the issuer **SHALL** promptly notify the PIV cardholder of the binding of a derived PIV credential through an independent means that would not afford an attacker the opportunity to interfere with the notification. More than one independent notification method **MAY** be used to ensure prompt receipt by the cardholder.

Derived PIV credentials **SHALL** meet the requirements for authentication assurance level (AAL) 2 or 3 specified in [[SP800-63B]](references.md#ref-SP-800-63B). Derived PIV credentials that meet AAL3 requirements also fulfill the requirements of AAL2 and can be used in circumstances that require authentication at AAL2. All derived PIV credentials at both AAL2 and AAL3 **SHALL** meet the requirements for phishing resistance defined in [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 5.2.5.

This guideline does not preclude the issuance of multiple derived PIV credentials to the same applicant on the basis of the same PIV Card. This could increase the risk that one of the derived PIV credentials will be lost/stolen without the loss being reported or that the subscriber will inappropriately provide one of them to someone else. Accordingly, issuers **MAY** place a limit on the number of active derived PIV credentials that a subscriber may have.

### PKI-based Derived PIV Credential Issuance {#s-2-2-1}

Issuance of a PKI-based derived PIV credential requires the generation of a public/private keypair followed by the creation of a corresponding authentication certificate by the CSP. For a derived PIV credential capable of being used at AAL3, the keypair **SHALL** be generated in the device (authenticator or endpoint) that will house the derived PIV credential. The device **SHALL** send the certificate signing request that contains the public key to the CSP, which **SHALL** return an X.509 authentication certificate that **SHALL** be stored on the credential. The CSP **SHALL** retain a copy of the issued certificate for use should revocation be required. For a derived PIV credential that is issued for use only at AAL2, the same procedure **MAY** be used, or the CSP **MAY** generate a keypair and corresponding certificate and send the certificate and private key to the device over an authenticated protected channel for installation. The CSP **SHALL** immediately and securely delete its copy of the private key.

The private key **SHALL** be stored on the device in a manner that makes it accessible only upon entry of the correct activation secret or presentation of a biometric factor that matches a stored biometric image or template. This **SHALL** be accomplished either through the use of strong access controls for the stored private key or through decryption of the private key using an encryption key that is derived from the activation secret.

### Non-PKI-based Derived PIV Credential Issuance {#s-2-2-2}

The applicant **SHALL** be provided with or supply an approved physical authenticator for the highest AAL that the derived PIV credential will be used to authenticate. If the authenticator is not directly provided by the issuer (i.e., the home agency), the issuer **SHALL** verify that the authenticator's characteristics (e.g., single-factor or multi-factor) meet the requirements of [[SP800-63B]](references.md#ref-SP-800-63B) for the highest authentication assurance level at which it will be used (AAL2 or AAL3), including [[FIPS140]](references.md#ref-FIPS140) requirements.

The issuance process for a multi-factor authenticator **SHALL** prompt the applicant to establish a memorized secret or biometric activation factor (or both) for the authenticator and successfully authenticate using that authenticator. The issuance process with a single-factor authenticator **SHALL** prompt the applicant to register a memorized secret that meets the requirements of [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 5.1.1 and that will be verified along with the physical authenticator in the authentication process.

## Maintenance {#s-2-3}

The maintenance activities required for derived PIV credentials depend on the type of derived PIV credential (PKI-based or non-PKI-based) being used. Maintenance activities include rekeying, modification of certificates, and replacement of an activation factor (biometric or memorized secret) as appropriate.

Derived PIV credentials are unaffected when the subscriber replaces their PIV Card with a new one (reissuance) or when the PIV Card is lost, stolen, or damaged. The ability for the subscriber to use a derived PIV credential is especially useful while waiting for a new PIV Card to be issued. In such circumstances, the subscriber continues to be able to use the derived PIV credential to gain logical access to remote federally controlled information systems from their endpoint. 

Updating the activation data (biometric or memorized secret, such as a PIN) or resetting the activation retry count for a derived PIV credential **SHALL** be performed in accordance with [Sec. 3.1.4](3_requirements.md#s-3-1-4) for PKI-based derived PIV credentials or [Sec. 3.2.3](3_requirements.md#s-3-2-3) for non-PKI-based derived PIV credentials.

### PKI-based Derived PIV Credential Maintenance {#s-2-3-1}

PKI-based derived PIV credentials require typical maintenance activities applicable to asymmetric cryptographic credentials, including rekeying and modification. These activities **MAY** be performed either remotely or in person and **SHALL** be performed in accordance with the certificate policy under which the derived PIV authentication certificate is issued. When certificate rekeying or modification is performed remotely for a derived PIV credential, communication between the issuer and the cryptographic module in which the derived PIV authentication private key is stored **SHALL** only occur over mutually authenticated secure sessions between tested and validated cryptographic modules.

Some maintenance activities for the subscriber’s PIV Card may trigger corresponding maintenance activities for the derived PIV credential since the derived PIV credential will need to be reissued if any information about the subscriber that appears in the credential changes. For example, if the subscriber’s PIV Card is reissued as a result of a change in the subscriber’s name and the subscriber’s name appears in the derived PIV authentication certificate, a new derived PIV authentication certificate with the new name **SHALL** be issued and the previous certificate invalidated.

### Non-PKI-based Derived PIV Credential Maintenance

The maintenance activities for non-PKI-based derived PIV credentials are somewhat simpler than for PKI-based derived PIV credentials since the former do not contain information about the cardholder and do not carry a specific expiration date. Identity information **SHALL** be maintained in the PIV identity account and **SHALL** be updated when needed.

Updating a separate memorized secret used with a single-factor authenticator for use at AAL2 **SHALL** be performed in a mutually authenticated protected session with the home agency. The update **SHALL** require the entry of the current memorized secret used for activation. If resetting the memorized secret is required because the subscriber has forgotten the memorized secret or has reached the retry limit, it **SHALL** be done in accordance with [Sec. 3.2.3](3_requirements.md#s-3-2-3).

## Invalidation {#s-2-4}

When an authenticator associated with a derived PIV credential is compromised (e.g., lost, stolen, or damaged), that derived PIV credential **SHALL** be invalidated as described below.

All derived PIV credentials associated with a given PIV Card **SHALL** be invalidated when the associated PIV identity account is terminated, typically due to the cardholder's loss of PIV Card eligibility. Issuers of derived PIV credentials **SHALL** continuously monitor the associated PIV identity account to determine its termination status. Meeting this requirement is simplified because the subject's PIV Card, cardholder eligibility, and all derived PIV credentials are maintained in one account &mdash; the PIV identity account &mdash; and maintained by the home agency.

The issuer of the derived PIV credential **SHALL NOT** solely rely on tracking the revocation status of the PIV authentication certificate as a means of tracking the termination status of the PIV Card. This is because there are situations in which the PIV authentication certificate is not revoked even though the PIV Card has been terminated and subsequently replaced with a new card. This may happen, for example, when a terminated PIV Card is collected and either zeroized or destroyed by an agency. In this case and in accordance with [[FIPS201]](references.md#ref-FIPS201), the corresponding PIV authentication certificate does not need to be revoked.

### PKI-based Derived PIV Credential Invalidation {#s-2-4-1}

If the derived PIV authentication private key was created and stored on a hardware module that does not permit export of the private key and the token is collected and either zeroized or destroyed, then the derived PIV authentication certificate **SHOULD** be revoked. In all other cases, the derived PIV authentication certificate **SHALL** be revoked.

### Non-PKI-based Derived PIV Credential Invalidation {#s-2-4-2}

Non-PKI-based derived PIV credentials are always directly verified by the home agency of the associated PIV Card. Therefore, termination of a non-PKI-based derived PIV credential **SHALL** be accomplished by invalidating the reference to the associated authenticator in the PIV identity account so that the authenticator cannot be used to authenticate to the home agency. Separate hardware-based authenticators **MAY** be collected from the subscriber, but this is not required.
