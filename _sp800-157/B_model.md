---
layout: default
title: Data Model and Interfaces for Removable PKI-based Hardware Cryptographic Devices
navOrder: 6
navTitle: Model
permalink: /model/
anchor: s-b
section: B
---

# Data Model and Interfaces for Removable or Wireless PKI-based Hardware Cryptographic Devices {#s-b}

*This appendix is normative.*

This appendix provides data model and interface requirements for PKI-based derived PIV applications that are implemented on removable or wireless hardware cryptographic tokens.

## Derived PIV Application Data Model and Representation

The data model and representation requirements for derived PIV applications are based on the requirements for PIV Card applications, as described in [[SP800-73]](references.md#ref-SP-800-73) Part 1. The specifications for the mandatory and optional data objects listed below are the same as the specifications for the corresponding data objects on a PIV Card application, as described in [[SP800-73]](references.md#ref-SP-800-73) Part 1.

### Derived PIV Application Identifier

The application identifier (AID) of the derived PIV application **SHALL** be (in hexadecimal):

```
A0 00 00 03 08      00 00 20 00       01 00
```

The derived PIV application can be selected as the current application on the removable hardware cryptographic token by providing the full AID listed above or by providing the right truncated version, as follows (hexadecimal):

```
A0 00 00 03 08       00 00 20 00
```

### Derived PIV Application Data Model Elements

The derived PIV application **SHALL** contain the following mandatory interoperable data object:

X.509 Certificate for Derived PIV Authentication
: The read access control rule for the X.509 certificate for derived PIV authentication and the PKI cryptographic function access rule for the corresponding private key are as described for the X.509 certificate for PIV authentication in Sec. 3.1.3 of [[SP800-73]](references.md#ref-SP-800-73) Part 1.

The following data objects **MAY** also be present:

X.509 Certificate for Digital Signature
: The read access control rule for the X.509 certificate for digital signature and the PKI cryptographic function access rule for the corresponding private key are as described in Sec. 3.2.1 of [[SP800-73]](references.md#ref-SP-800-73) Part 1.

X.509 Certificate for Key Management
: The read access control rule for the X.509 certificate for key management and the PKI cryptographic function access rule for the corresponding private key are as described in Sec. 3.2.2 of [[SP800-73]](references.md#ref-SP-800-73) Part 1.

Discovery Object
: The requirements for the discovery object are as described in Sec. 3.3.2 of [[SP800-73]](references.md#ref-SP-800-73) Part 1, except for the following:

    - References to “PIV card application AID” are replaced by “derived PIV application AID.”
    - References to “PIV card application PIN” are replaced by “derived PIV activation secret.”
    - The first byte of the PIN usage policy **SHALL** be set to `0x40` to indicate that the virtual contact interface (VCI) is not implemented, `0x48` to indicate that a pairing code is required to establish a VCI, or `0x4C` to indicate that no pairing code is required to establish a VCI. This also means that neither the global PIN nor the on-card biometric comparison (OCC) satisfies the access control rules for command execution and data object access within the derived PIV application.

Key History Object
: Up to 20 retired key management private keys **MAY** be stored in the derived PIV application. The Key History Object **SHALL** be present in the derived PIV application if the derived PIV application contains any retired key management private keys but **MAY** be present even if no such keys are present in the derived PIV application. The requirements for the key history object are as described in Sec. 3.3.3 of [[SP800-73]](references.md#ref-SP-800-73) Part 1, except for the following:

    - References to *keysWithOnCardCerts* **SHOULD** be interpreted as keys for which the corresponding certificate is populated within the derived PIV application.
    - References to *keysWithOffCardCerts* **SHOULD** be interpreted as keys for which the corresponding certificate is not populated within the derived PIV application.
    - References to *offCardCertURL* **SHOULD** be interpreted as a URL that points to a file containing the certificates that correspond to all of the retired key management private keys within the derived PIV application, including those for which the corresponding certificate is stored within the derived PIV application.

Retired X.509 Certificates for Key Management
: The read access control rules for the retired X.509 certificates for key management and the PKI cryptographic function access rules for corresponding private keys are as described in Sec. 3.3.4 of [[SP800-73]](references.md#ref-SP-800-73) Part 1.

Security Object
: The security object **SHALL** be present in the derived PIV application if the discovery object, the key history object, or the optional pairing code reference data container is present. The requirements for the security object are as described in Sec. 3.1.7 of [[SP800-73]](references.md#ref-SP-800-73) Part 1, except for the following:

    - The security object for a derived PIV application is signed using a private key whose corresponding public key is contained in a PIV content signing certificate that satisfies the requirements for certificates used to verify signatures on cardholder unique identifiers (CHUID), as specified in Sec. 4.2.1 of [[FIPS201]](references.md#ref-FIPS201).
    - The signature field of the Security Object, tag `0xBB`, **SHALL** include the derived PIV credential issuer’s certificate.
    - All unsigned data objects (i.e., the discovery object, the key history object, and the pairing code reference data container) within the derived PIV application **SHALL** be included in the security object.

Secure Messaging Certificate Signer
: Derived PIV credential applications that support the virtual contact interface (VCI) capability **SHALL** include the secure messaging certificate signer object described in Sec. 3.3.7 of [[SP800-73]](references.md#ref-SP-800-73) Part 1.

Pairing Code Reference Data Container
: Derived PIV credential applications that support the virtual contact interface (VCI) using a pairing code **SHALL** include the pairing code reference data container described in Sec. 3.3.8 of [[SP800-73]](references.md#ref-SP-800-73) Part 1.

~~~
\clearpage
~~~
{:latex-literal="true"}

#### Derived PIV Application Data Object Containers and Associated Access Rules

Section 3.5 of [[SP800-73]](references.md#ref-SP-800-73) Part 1 provides the container IDs and access rules for the mandatory and optional data objects for a derived PIV application with the following mappings:

[Table 1. Mapping of Data Objects](B_model.md#table-1){:name="table-1"}
{:latex-ignore="true"}

| Derived PIV Application Data Object | PIV Card Application Data Object |
|-------------------------------------|----------------------------------|
| X.509 Certificate for Derived PIV Authentication | X.509 Certificate for PIV Authentication |
| Security Object | Security Object |
| X.509 Certificate for Digital Signature | X.509 Certificate for Digital Signature |
| X.509 Certificate for Key Management | X.509 Certificate for Key Management |
| Discovery Object | Discovery Object |
| Key History Object | Key History Object |
| Retired X.509 Certificate for Key Management [1:20] | Retired X.509 Certificate for Key Management [1:20] |
| Secure Messaging Certificate Signer | Secure Messaging Certificate Signer |
| Pairing Code Reference Data Container | Pairing Code Reference Data Container |
{:latex-table="1" latex-caption="Mapping of Data Objects"}

The detailed data model specifications for each of the data objects of the derived PIV application are the same as the specifications for the corresponding data objects (mapped per [Table 1](B_model.md#table-1)) of the PIV Card application as described in Appendix A of [[SP800-73]](references.md#ref-SP-800-73) Part 1, except for the following:

- The security object for the derived PIV application is optional. It is required if the optional discovery object, the optional key history object, or the optional pairing code reference data container is present.

- The minimum capacity for the security object container **SHALL** be 3000 bytes in order to allow space for the derived PIV credential issuer’s certificate.

### Derived PIV Application Data Objects Representation

The ASN.1 object identifiers (OID) and “basic encoding rules – tag length value” (BER-TLV) tags for the mandatory and optional data objects within the derived PIV application are the same as for the corresponding data objects (mapped per [Table 1](B_model.md#table-1)) of the PIV Card application, as described in Sec. 4 of [[SP800-73]](references.md#ref-SP-800-73) Part 1.

### Derived PIV Application Data Types and Their Representation

This appendix provides a description of the data types used in the derived PIV application command interface.

#### Derived PIV Application Key References and Security Conditions of Use

Key references are assigned to keys and secrets of the derived PIV application. Table 6-1 of [[SP800-78]](references.md#ref-SP-800-78) and Table 4 of [[SP800-73]](references.md#ref-SP-800-73) Part 1 define the key reference values that **SHALL** be used on the derived PIV application interfaces with the following mappings:

[Table 2. Mapping of Key Types](B_model.md#table-2){:name="table-2"}
{:latex-ignore="true"}

| Derived PIV Key Type | PIV Key Type |
| --- | --- |
| Derived PIV Activation Secret | PIV Card Application PIN |
| Activation Secret Unblocking Key | PIN Unblocking Key |
| Derived PIV Authentication Key | PIV Authentication Key |
| Derived PIV Token Management Key | Card Management Key |
| Digital Signature Key | Digital Signature Key |
| Key Management Key | Key Management Key |
| Retired Key Management Key | Retired Key Management Key |
| Derived PIV Secure Messaging Key | PIV Secure Messaging Key |
{:latex-table="2" latex-caption="Mapping of Key Types"}

The key reference specifications in Sec. 5.1 of [[SP800-73]](references.md#ref-SP-800-73) Part 1 are applicable to the corresponding keys included in the derived PIV application (mapped per [Table 2](B_model.md#table-2)), except for the following:

- References to “PIV Card application” are replaced with “derived PIV application.”

- References in the “Security Condition for Use” column to “PIN or OCC” are replaced with “derived PIV activation secret.”

#### Derived PIV Application Cryptographic Algorithm and Mechanism Identifiers

The algorithm identifiers for the cryptographic algorithms that **MAY** be recognized on the derived PIV application interfaces are the symmetric and asymmetric identifiers specified in Table 6-2 and Table 6-3 of [[SP800-78]](references.md#ref-SP-800-78). The cryptographic mechanism identifiers that **MAY** be recognized on the derived PIV application interfaces are those specified in Table 5 of [[SP800-73]](references.md#ref-SP-800-73) Part 1.

#### Derived PIV Application Status Words

The status words that **MAY** be returned on the derived PIV application command interface are as specified in Sec. 5.6 of [[SP800-73]](references.md#ref-SP-800-73) Part 1.

### Derived PIV Authentication Mechanisms

The derived PIV application supports the following validation steps:

- Credential validation (CredV) is established by verifying the certificates retrieved from the derived PIV application and checking the validity and revocation status of these certificates.

- Derived PIV application holder validation (HolderV) is established when the authenticator holder proves knowledge of the derived PIV activation secret associated with the derived PIV credential that contains valid and unrevoked certificates.

The derived PIV application facilitates a single authentication mechanism, which is a cryptographic challenge and response authentication protocol that uses the derived PIV authentication private key as described in Appendix B.1.2 of [[SP800-73]](references.md#ref-SP-800-73) Part 1 with the following translations:

- References to “PIV application” are replaced with “derived PIV application.”
- References to “PIV auth certificate” are replaced with “derived PIV authentication certificate.”
- References to “PIV Card app ID” are replaced with “derived PIV application ID.”

The authentication can also be performed wirelessly over a virtual contact interface (VCI) if a VCI has been established with the derived PIV application.

## Derived PIV Application Token Command Interface

This appendix contains the technical specifications for the command interface to the derived PIV application surfaced by the card edge of the integrated circuit card (ICC) that represents the removable hardware cryptographic token. The command interface for the derived PIV application **SHALL** implement all of the card commands supported by the PIV Card application as described in [[SP800-73]](references.md#ref-SP-800-73) Part 2, which include:

- SELECT
- GET DATA
- VERIFY
- CHANGE REFERENCE DATA
- RESET RETRY COUNTER
- GENERAL AUTHENTICATE
- PUT DATA
- GENERATE ASYMMETRIC KEY PAIR

The specifications for the token command interface **SHALL** be the same as the specifications for the corresponding card edge commands for a PIV Card as described in [[SP800-73]](references.md#ref-SP-800-73) Part 2, except for the following deviations:

- References to “PIV Card application” are replaced with “derived PIV application.”
- References to “PIV data objects” are replaced with “derived PIV data objects.”
- References to “PIV authentication key” are replaced with “derived PIV authentication key.”
- The derived PIV activation secret **SHALL** satisfy the criteria specified in Appendix B.2.1 of this document rather than Sec. 2.4.3 of [[SP800-73]](references.md#ref-SP-800-73) Part 2.
- In Appendix A:
    - References to “PIV Card application administrator” are replaced with “derived PIV application administrator.”
    - References to “card management key” are replaced with “derived PIV token management key.”

The token platform **SHALL** support a default selected application, which is the selected application that immediately following a cold or warm reset. This default application may be the derived PIV application or another application.

### Authentication of an Individual

Knowledge of a memorized secret (specifically the derived PIV activation secret) is the means by which an individual can be authenticated to the derived PIV application.

The derived PIV activation secret **SHALL** be between 6 and 8 bytes in length. If the actual length of the derived PIV activation secret is less than 8 bytes, it **SHALL** be padded to 8 bytes with `0xFF` when presented to the token command interface. The `0xFF` padding bytes **SHALL** be appended to the actual value of the secret. The bytes that comprise the derived PIV activation secret **SHALL** be limited to values `0x30` – `0x39`, `0x41` – `0x5A`, and `0x61` – `0x7A`: the ASCII values for the decimal digits '0' – '9'; upper case characters 'A' – 'Z'; and lower case characters 'a' – 'z'. For example,

- Actual derived PIV activation secret: “Part21” or (hexadecimal) `50 61 72 74 32 31`
- Padded derived PIV activation secret presented to the card command interface (hexadecimal): `50 61 72 74 32 31 FF FF`

The derived PIV application **SHALL** enforce the minimum length requirement of 6 bytes for the derived PIV activation secret (i.e., **SHALL** verify that at least the first 6 bytes of the value presented to the card command interface are in the range `0x30` – `0x39`, `0x41` – `0x5A`, or `0x61` – `0x7A`) as well as the other formatting requirements specified in this section.
