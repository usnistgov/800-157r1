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

This section describes technical requirements for PKI-based and non-PKI-based derived PIV credentials and associated authenticators.

While the following sections focus on credential and authenticator requirements, the verifier is required to meet the corresponding verifier requirements in [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 3.1.

## PKI-Based Derived PIV Credentials {#s-3-1}

A PKI-based derived PIV credential is a derived PIV authentication certificate, which is an X.509 public key certificate that has been issued in accordance with the requirements of this document and [[COMMON]](references.md#ref-COMMON). All derived PIV credentials created under previous revisions of these guidelines are PKI-based and remain valid implementations under this SP 800-157 revision. [Appendix B](B_model.md#s-b) describes additional requirements for removable or wireless PKI-based derived PIV credentials that are used for logical access.

Authentication using PKI-based derived PIV credentials **SHALL** include a check to determine that the authentication certificate is valid and current (e.g., that the certificate is unexpired and not revoked).

### Certificate Policies for PKI-Based Derived PIV Credentials {#s-3-1-1}

Derived PIV authentication certificates **SHALL** be issued under either the `id-fpki-common-derived-pivAuth-hardware` policy (satisfying [[SP800-63B]](references.md#ref-SP-800-63B) AAL3) or the `id-fpki-common-derived-pivAuth` policy (satisfying AAL2) of [[COMMON]](references.md#ref-COMMON). All derived PIV credentials **SHALL** be deemed to satisfy [[SP800-63A]](references.md#ref-SP-800-63A) IAL3 since that is the identity proofing and issuance level associated with the PIV Card and bound to the PIV identity account.

Derived PIV authentication certificates **SHALL** comply with the *Derived PIV Authentication Certificate* profile in [[PROF]](references.md#ref-PROF).

The expiration date of a derived PIV authentication certificate is based on the issuer's certificate policy and the certificate policy specified above. There is no requirement to align the expiration date of a derived PIV authentication certificate with the expiration date of the PIV authentication certificate or the expiration of the PIV Card. This allows a derived PIV credential to continue to act as an active credential while the cardholder's PIV Card is being renewed.

### Cryptographic Specifications {#s-3-1-2}

The cryptographic algorithm and key size requirements for the derived PIV authentication certificates and
private keys are the same as the requirements for the PIV authentication certificate and private key, as
specified in [[SP800-78]](references.md#ref-SP-800-78).

For derived PIV authentication certificates issued under `id-fpki-common-pivAuth-derived-hardware`
(AAL3), the derived PIV authentication key pair **SHALL** be generated within a cryptographic
module that meets the requirements of [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 2.3.2, including being validated to [[FIPS140]](references.md#ref-FIPS140) Level 2 or higher with Level 3 physical security to
protect the derived PIV authentication private key while in storage and not permitting export
of the private key.

For derived PIV authentication certificates issued under `id-fpki-common-pivAuth-derived` (AAL2), the
derived PIV authentication key pair **SHALL** be generated within a cryptographic module that has been
validated to [[FIPS140]](references.md#ref-FIPS140) Level 1 or higher. If the key pair is generated outside of the authenticator itself, the private key **SHALL** be transferred via an authenticated protected channel as defined in [[SP800-63B]](references.md#ref-SP-800-63B), and the authenticator **SHALL** meet the requirements of [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 2.2.2, including being validated to [[FIPS140]](references.md#ref-FIPS140) Level 1 or higher.

### Allowable Authenticator Types {#s-3-1-3}

A multi-factor cryptographic authenticator as specified in [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 3.1.7.1 **SHALL** be used for PKI-based derived PIV authentication. The authenticator **SHALL** be phishing-resistant, as described in [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 3.2.5. Authenticators used at AAL3 **SHALL** meet the additional requirements described in [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 2.3.

### Activation Data {#s-3-1-4}

Activation of PKI-based derived PIV authenticators using an activation secret **SHALL** meet the requirements of [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 3.2.10. Activation using a biometric characteristic **SHALL** meet the requirements of [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 3.2.3.

If the activation secret or the biometric activation factor needs to be changed, entry of the current activation secret **SHALL** be required to change the value. The authenticator **MAY** support a PIN unblocking key (PUK) that can be used by the home agency IdMS to unblock or reset the activation secret or biometric activation factor if it has been forgotten or the permitted number of consecutive wrong attempts has been reached. If reset using PUK is unavailable and the authenticator cannot be successfully activated, the authenticator **SHALL** be invalidated as described in [Sec. 2.4](2_lifecycle.md#s-2-4). A new derived PIV credential **MAY** then be issued.

## Non-PKI-Based Derived PIV Credentials {#s-3-2}

Non-PKI-based credentials **SHALL** only be used to authenticate to verifiers that are authorized by the home agency of the associated PIV Card. All verifiers of non-PKI-based derived PIV credentials **SHALL** access the home agency IdMS in order to determine the current validity of the associated PIV identity account. Non-PKI derived PIV credentials can be used elsewhere through federation with an IdP able to access the home agency IdMS, as described in [[SP800-217]](references.md#ref-SP-800-217). 

### Allowable Authenticator Types {#s-3-2-1}

Multi-factor or single-factor cryptographic authenticators as specified in [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 3.1.7.1 and Sec. 3.1.6.1, respectively, **SHALL** be used for non-PKI-based derived PIV authentication. Cryptographic authenticators **SHALL** be phishing-resistant as described in [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 3.2.5. Examples of suitable authentication processes include client-authenticated TLS and WebAuthn [[WebAuthn]](references.md#ref-WebAuthn). Except for physical access applications specified in [Appendix D](D_pacs.md#s-d), all single-factor authenticators **SHALL** be used in conjunction with a password that meets the requirements of [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 3.1.1. Authenticators used at AAL3 **SHALL** meet the additional requirements described in [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 2.3.

### Cryptographic Specifications {#s-3-2-2}

Authenticators used as non-PKI-based derived PIV credentials **SHALL** meet the cryptographic requirements specified in [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 3.1 for the corresponding authenticator type.

### Activation Data {#s-3-2-3}

Activation of the derived PIV credential using an activation secret **SHALL** meet the requirements of [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 3.2.10. Activation using a biometric characteristic **SHALL** meet the requirements of [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 3.2.3.

If the activation secret or the biometric activation factor needs to be changed, entry of the current activation secret **SHALL** be required to change the value. If the activation secret has been forgotten or the permitted number of consecutive wrong attempts has been reached, centralized management by the home agency IdMS **SHALL** be required to reset the activation secret and attempt counter. If centralized reset is unavailable, the authenticator **SHALL** be reset and will requires re-binding to the PIV identity account, as described in [Sec. 2.2](2_lifecycle.md#s-2-2).
