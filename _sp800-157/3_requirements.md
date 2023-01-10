---
layout: default
title: Technical Requirements
navOrder: 3
navTitle: Requirements
permalink: /requirements/
anchor: s-3
section: 3
---

# Technical Requirements {#s-3}

*This section is normative.*

This section describes technical requirements for both PKI-based and non-PKI-based derived PIV credentials and associated authenticators.

While the following sections focus on credential and authenticator requirements, the verifier is required to meet the corresponding verifier requirements in [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 5.1.

## PKI-based Derived PIV Credentials {#s-3-1}

A PKI-based derived PIV credential is a derived PIV authentication certificate, which is an X.509 public key certificate that has been issued in accordance with the requirements of this document and [[COMMON]](references.md#ref-COMMON). All derived PIV credentials created under previous revisions of these guidelines are PKI-based and remain valid implementations under this revision of SP 800-157. Additional requirements for PKI-based derived PIV credentials that are removable or wireless are found in [Appendix B](B_model.md#s-b).

Authentication using PKI-based derived PIV credentials **SHALL** include a check to determine that the authentication certificate is valid and current (e.g., that the certificate is unexpired and not revoked).

### Certificate Policies for Derived PIV Credentials {#s-3-1-1}

Derived PIV authentication certificates **SHALL** be issued under either the `id-fpki-common-derived-pivAuth-hardware` policy (satisfying [[SP800-63B]](references.md#ref-SP-800-63B) AAL3) or the `id-fpki-common-derived-pivAuth` policy (satisfying AAL2) of [[COMMON]](references.md#ref-COMMON). All derived PIV credentials **SHALL** be deemed to satisfy [[SP800-63A]](references.md#ref-SP-800-63A) IAL3 since that is the identity proofing and issuance level associated with the PIV Card and bound to the PIV identity account.

Derived PIV authentication certificates **SHALL** comply with the *Derived PIV Authentication Certificate* profile in [[PROF]](references.md#ref-SP-800-78).

The expiration date of a derived PIV authentication certificate is based on the certificate policy of the
issuer. There is no requirement to align the expiration date of a derived PIV authentication certificate
with the expiration date of the PIV authentication certificate or the expiration of the PIV Card. However,
in many cases, aligning the expiration dates will simplify lifecycle management.

### Cryptographic Specifications {#s-3-1-2}

The cryptographic algorithm and key size requirements for the derived PIV authentication certificates and
private keys are the same as the requirements for the PIV authentication certificate and private key, as
specified in [[SP800-78]](references.md#ref-SP-800-78).

For derived PIV authentication certificates issued under `id-fpki-common-pivAuth-derived-hardware`
(AAL3), the derived PIV authentication key pair **SHALL** be generated within a hardware cryptographic
module that meets the requirements of [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 4.2.2, including being validated to [[FIPS140]](references.md#ref-FIPS140) Level 2 or higher with Level 3 physical security to
protect the derived PIV authentication private key while in storage and not permitting export
of the private key.

For derived PIV authentication certificates issued under `id-fpki-common-pivAuth-derived` (AAL2), the
derived PIV authentication key pair **SHALL** be generated within a cryptographic module that has been
validated to [[FIPS140]](references.md#ref-FIPS140) Level 1 or higher. If the key pair is generated outside of the authenticator itself, the private key **SHALL** be transferred via an authenticated protected channel as defined in [[SP800-63B]](references.md#ref-SP-800-63B), and the authenticator **SHALL** meet the requirements of [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 4.2.2, including being validated to [[FIPS140]](references.md#ref-FIPS140) Level 1 or higher. 

### Allowable Authenticator Types {#s-3-1-3}

Phishing-resistant multi-factor cryptographic authenticators **SHALL** be used for PKI-based derived PIV authentication. A multi-factor cryptographic device authenticator as specified in [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 5.1.9.1 **SHALL** be used for derived PIV authentication at AAL3. Either a multi-factor cryptographic device authenticator or a multi-factor cryptographic software authenticator as specified in [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 5.1.8.1 **SHALL** be used for derived PIV authentication at AAL2.

### Activation Data {#s-3-1-4}

Activation of the derived PIV authenticator using a memorized secret **SHALL** meet the requirements of [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 5.2.11. Activation using a biometric characteristic **SHALL** meet the requirements of [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 5.2.3. Unlocking the device that houses a derived PIV authenticator (e.g., mobile phone) **SHALL NOT** be considered activation of the authenticator. Separate entry of the activation secret or presentation of a biometric factor **SHALL** be performed to use the authenticator. The same secret or biometric factor used to unlock the device **MAY** be used to activate the authenticator.

If the memorized secret used for activation or the biometric activation factor needs to be changed, entry of the current memorized secret **SHALL** be required to change the value. If the activation secret has been forgotten or the permitted number of consecutive wrong attempts has been reached, the home agency **SHALL** be required to input the PIN unblocking key (PUK). If the PUK is not implemented by the authenticator or cannot be provided, either the authenticator certificates **SHALL** be revoked or the associated private keys **SHALL** be destroyed or zeroized. A new derived PIV credential MAY then be obtained.

## Non-PKI-based Derived PIV Credentials {#s-3-2}

When used, non-PKI-based credentials **SHALL** be used to authenticate only to the home agency of the associated PIV Card.

### Allowable Authenticator Types {#s-3-2-1}

Phishing-resistant multi-factor or single-factor cryptographic authenticators **SHALL** be used for non-PKI-based derived PIV authentication. A multi-factor cryptographic device authenticator as specified in [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 5.1.9.1 or a single-factor cryptographic device authenticator as specified in [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 5.1.7.1 **SHALL** be used for derived PIV authentication at AAL3. Either a cryptographic device authenticator or a multi-factor cryptographic software authenticator as specified in [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 5.1.8.1 or a single-factor cryptographic software authenticator as specified in [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 5.1.6.1 **SHALL** be used for derived PIV authentication at AAL2. All single-factor authenticators **SHALL** be used in conjunction with a memorized secret that meets the requirements of [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 5.1.1.1.

### Cryptographic Specifications {#s-3-2-2}

Authenticators used as non-PKI-based derived PIV credentials **SHALL** meet the cryptographic requirements specified in [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 5.1 for the corresponding authenticator type.

### Activation Data {#s-3-2-3}

Activation of a multi-factor authenticator being used as a derived PIV credential using a memorized secret **SHALL** meet the requirements of [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 5.2.11. Activation using a biometric characteristic **SHALL** meet the requirements of [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 5.2.3. Unlocking the device that houses the authenticator (e.g., mobile phone) **SHALL NOT** be considered activation of the authenticator. Separate entry of the activation secret or presentation of a biometric factor **SHALL** be performed to use the authenticator. The same activation secret or biometric factor used to unlock the device **MAY** be used to activate the authenticator.

If the memorized secret used for activation or the biometric activation factor needs to be changed, entry of the current activation secret **SHALL** be required to change the value. If the activation secret has been forgotten or the permitted number of consecutive wrong attempts has been reached, the activation secret and attempt counter MAY be reset by centralized management by the home agency. If centralized reset is not available, the authenticator **SHALL** be reset and require re-binding to the PIV identity account, as described in Sec. 3.3.

## Binding Derived PIV Credentials

Binding a derived PIV credential to a PIV identity account can be accomplished through a connection to a PIV-authenticated endpoint, a direct connection to the PIV Card, or the use of the external authenticator binding procedure, as described in [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 6.1.2.4. In all cases, binding **SHALL** require the use of the PIV-AUTH authentication mechanism specified in [[FIPS201]](references.md#ref-FIPS201).

