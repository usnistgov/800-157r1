---
layout: default
title: Physical Access
navOrder: 8
navTitle: Physical Access
permalink: /pacs/
anchor: s-d
section: D
---

# Physical Access {#s-d}

*This appendix is normative.*

Credentials on PIV cards are commonly used to identify and authenticate individuals accessing government facilities. Agencies **MAY** issue derived PIV credentials for use with physical access control systems. This appendix provides data model and interface requirements for derived PIV applications for physical access. To facilitate compatibility with PIV readers, these requirements reference the requirements for the PIV card and PIV card application specified in [[SP800-73pt2]](references.md#ref-SP-800-73pt2).

Authentication to physical access control systems (PACS) using derived PIV credentials **MAY** use the PKI-CAK or SM-AUTH authentication mechanisms described in [[SP800-73pt2]](references.md#ref-SP-800-73pt2) and [[SP800-116]](references.md#ref-SP-800-116). Derived PIV credential modules that support PACS **SHALL** support the PKI-CAK authentication mechanism. Physical access **SHALL** be supported by contactless readers that conform to [[ISO14443]](references.md#ref-ISO14443) for the card-to-reader interface and conform to [[ISO7816]](references.md#ref-ISO7816) for data transmitted over the [[ISO14443]](references.md#ref-ISO14443) link.  If readers are connected to general-purpose desktop computing systems, they **SHALL** conform to [[PCSC]](references.md#ref-PCSC) for the reader-to-host system interface and the requirements specified in [[SP800-96]](references.md#ref-SP-800-96). This standard does not specify the reader-to-host system interface in systems where the readers are not connected to general-purpose desktop computing systems.

Since the PKI-CAK and SM-AUTH authentication mechanisms are single-factor, there is no need to establish an activation factor for these physical access methods.

Issuance of derived PIV credentials that support PACS **SHALL** be done in accordance with the post-enrollment binding described in [Sec. 2.2](2_lifecycle.md#s-2-2) and the PKI-based PIV credential issuance procedures described in [Sec. 2.2.1](2_lifecycle.md#s-2-2-1). Issuance of derived PIV credentials in support of PACS without a PIV card **SHALL** follow [Sec. 2.2.3](2_lifecycle.md#s-2-2-3).

## PACS Derived PIV Application Data Model and Representation

The data model and representation requirements for the derived PIV application are based on the requirements for the PIV Card application, as described in [[SP800-73pt1]](references.md#ref-SP-800-73pt1). Test requirements and test assertions for testing the derived PIV application and associated derived PIV data objects implemented on removable hardware tokens are specified in [[SP800-166]](references.md#ref-SP-800-166), *Derived PIV Application and Data Model Test Guidelines*. The specifications for the mandatory and optional data objects listed below are the same as the specifications for the corresponding data objects on a PIV Card application, as described in [[SP800-73pt1]](references.md#ref-SP-800-73pt1), with exceptions as noted.

### Derived PIV Application Identifier

Either the PIV card application identifier (AID) defined in Sec. 2.2 of [[SP800-73pt1]](references.md#ref-SP-800-73pt1) or the derived PIV application AID, defined in [Appendix B](B_model.md#s-b), **SHALL** be used. To maximize compatibility with existing PACS readers, the AID of the PIV card application **SHOULD** be used unless the use of the derived PIV AID for logical access makes this infeasible.

For reference, the AID of the PIV card application is (in hexadecimal):

```
A0 00 00 03 08      00 00 10 00       01 00
```

The AID of the derived PIV application is (in hexadecimal):

```
A0 00 00 03 08      00 00 20 00       01 00
```

The desired application can be selected by providing the full AID listed above or a truncated version that omits the last two bytes '01 00'.

### PACS Derived PIV Application Data Model Elements {#s-d-1-2}

The derived PIV application **SHALL** contain the following data objects when used for PACS:

Derived CHUID Data Object
: The read access control rule for the derived CHUID data object is as described for the CHUID data object specified in Sec. 3.1.2 of [[SP800-73pt1]](references.md#ref-SP-800-73pt1) except that it **SHALL** be accessible only via the contactless interface. The FASC-N and card UUID contained within the derived CHUID data object **SHALL** be distinct from the corresponding values on the PIV card and any other derived PIV credential module.[^distinct] This data object is required for access control systems that use the FASC-N or the card UUID in the CHUID to look up authorization information rapidly. The derived CHUID **SHALL NOT** be used for authentication since that authentication method has been withdrawn. If the optional cardholder UUID is included in the derived CHUID data object, it **SHALL** contain the same value as the cardholder's PIV card.

The FASC-N, card UUID, expiration date, and, if present, cardholder UUID **SHALL NOT** be modified post-issuance.

[^distinct]: This will generally require multiple entries for the cardholder on the access control list &mdash; one for each of their derived PIV credential modules and the PIV card.

The expiration date included in the derived CHUID data object **SHALL** be the same as the expiration date of the derived card authentication certificate. It **SHALL** be no later than the expiration date of the content signing certificate. There is no requirement to align the expiration date included in the derived CHUID data object with the expiration date of the CHUID data object on the cardholder's PIV Card or with other certificates on the derived PIV credential. 

X.509 Certificate for Derived Card Authentication
: This data object is required for the PKI-CAK authentication mechanism. The read access control rule for the X.509 certificate for derived card authentication and the PKI cryptographic function access rule for the corresponding private key are as described for the X.509 certificate for card authentication in Sec. 3.1.4 of [[SP800-73pt1]](references.md#ref-SP-800-73pt1) with the exception that they **SHALL** only be accessible via the contactless interface. The card UUID value **SHALL** be the same as the one in the derived CHUID data object.

The derived PIV application **MAY** contain the following data objects:

Derived PIV Secure Messaging Key and Derived Card Verifiable Certificate
: The PKI cryptographic function access rule for the derived PIV secure messaging key and the read access control rule for the derived card verifiable certificate (DCVC) are as described for the secure messaging key specified in Sec. 5.1.2 of [[SP800-73pt1]](references.md#ref-SP-800-73pt1) and Sec. 4.1.5 of [[SP800-73pt2]](references.md#ref-SP-800-73pt2), respectively, except that they **SHALL** only be accessible via the contactless interface. These data objects are required for the SM-AUTH authentication mechanism. The card UUID in the derived card verifiable certificate **SHALL** be the same as that in the derived CHUID data object.

Secure Messaging Certificate Signer Object
: The read access control rule for the secure messaging certificate signer object is as described in Sec. 3.3.7 of [[SP800-73pt1]](references.md#ref-SP-800-73pt1). This data object is required for the SM-AUTH authentication mechanism.

#### PACS Derived PIV Application Data Object Containers and Associated Access Rules

Section 3.5 of [[SP800-73pt1]](references.md#ref-SP-800-73pt1) provides the container IDs and access rules for the PACS data objects for a derived PIV application with the mappings in [Table 3](D_pacs.md#table-3).

[Table 3. Mapping of PACS data objects](D_pacs.md#table-3){:name="table-3"}
{:latex-ignore="true"}

| Derived PIV Application Data Object | PIV Card Application Data Object | Specification |
|-------------------------------------|----------------------------------|---------------|
| X.509 Certificate for Derived Card Authentication | X.509 Certificate for Card Authentication | [[SP800-73pt1]](references.md#ref-SP-800-73pt1) Appendix A Table 18
| Derived CHUID Data Object | CHUID Data Object | [[SP800-73pt1]](references.md#ref-SP-800-73pt1) Appendix A Table 10
| Derived Card Verifiable Certificate | Card Verifiable Certificate | [[SP800-73pt2]](references.md#ref-SP-800-73pt2) Sec. 4.1.5
| Secure Messaging Certificate Signer | Secure Messaging Certificate Signer | [[SP800-73pt1]](references.md#ref-SP-800-73pt1) Appendix A Table 43
{:latex-table="3" latex-caption="Mapping of Data Objects"}

The detailed data model specifications for each of the PACS data objects are the same as the specifications for the corresponding data objects of the PIV Card application cited in [Table 3](D_pacs.md#table-3) above with the exception that, as specified in [Sec. D.1.2](#s-d-1-2), they are accessible only over the contactless interface, except for the Secure Messaging Certificate Signer.

Derived card authentication certificates **SHALL** be issued under the `id-fpki-common-devices` or the `id-fpki-common-devicesHardware` policy of [[COMMON]](references.md#ref-COMMON). The certificate **SHALL** also include an extended key usage (extKeyUsage) extension asserting `id-PIV-cardAuth`. Derived card authentication certificates **SHALL** comply with the *Alternative PACS Authenticator Certificate* profile in [[PROF]](references.md#ref-PROF).

The expiration date of a derived card authentication certificate is based on the issuer's certificate policy and the certificate policy specified above. There is no requirement to align the expiration date of a derived card authentication certificate with the expiration date of the card authentication certificate or the expiration of the PIV Card. This allows a derived PIV credential to continue to act as an active credential while the cardholder's PIV Card is being renewed.

For derived card authentication certificates issued under `id-fpki-common-devices`, the derived card authentication key pair **SHALL** be generated within a cryptographic module that has been validated to [[FIPS140]](references.md#ref-FIPS140) Level 1 or higher. If the key pair is generated outside of the authenticator itself, the private key **SHALL** be transferred via an authenticated protected channel as defined in [[SP800-63B]](references.md#ref-SP-800-63B), and the authenticator **SHALL** meet the requirements of [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 2.2.2, including being validated to [[FIPS140]](references.md#ref-FIPS140) Level 1 or higher.

For derived card authentication certificates issued under `id-fpki-common-devicesHardware`, the derived card authentication key pair **SHALL** be generated within a cryptographic module that has been validated to [[FIPS140]](references.md#ref-FIPS140) Level 2 or higher. If the key pair is generated outside of the authenticator itself, the private key **SHALL** be transferred via an authenticated protected channel as defined in [[SP800-63B]](references.md#ref-SP-800-63B), and the authenticator **SHALL** meet the requirements of [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 2.3.2, including being validated to [[FIPS140]](references.md#ref-FIPS140) Level 2 or higher.


If present, the derived PIV secure messaging key pair **SHALL** be generated on the authenticator itself. Its private key **SHALL NOT** be exportable. The authenticator **SHALL** be validated to [[FIPS140]](references.md#ref-FIPS140) Level 1 or higher.

The issuer **SHALL** generate the derived PIV card verifiable certificate, the derived CHUID data object, and the secure messaging certificate signer object (if required) and transfer them to the authenticator.


### Derived PIV PACS Application Data Objects Representation

The ASN.1 object identifiers (OID) and *basic encoding rules – tag length value* (BER-TLV) tags for the PACS data objects within the derived PIV application are the same as for the corresponding data objects of the PIV Card application (mapped per [Table 3](D_pacs.md#table-3)), as described in Sec. 4 of [[SP800-73pt1]](references.md#ref-SP-800-73pt1).

### Derived PIV Application PACS Data Types and Representation

This section describes the data types used in the derived PIV application PACS command interface.

#### Derived PIV Application PACS Key References and Security Conditions

Key references are assigned to keys and secrets of the derived PIV application. Table 8 of [[SP800-78]](references.md#ref-SP-800-78) and Table 4 of [[SP800-73pt1]](references.md#ref-SP-800-73pt1) define the key reference values that **SHALL** be used on the derived PIV application interfaces with the mappings in [Table 4](D_pacs.md#table-4).

[Table 4. Mapping of PACS key types](D-pacs.md#table-4){:name="table-4"}
{:latex-ignore="true"}

| Derived PIV PACS Key Type | PIV Key Type |
| --- | --- |
| Derived Card Authentication Key | Card Authentication Key |
| Derived PIV Secure Messaging Key | PIV Secure Messaging Key |
{:latex-table="4" latex-caption="Mapping of PACS Key Types"}

The key reference specifications in Sec. 5.1 of [[SP800-73pt1]](references.md#ref-SP-800-73pt1) apply to the corresponding keys included in the derived PIV application (mapped per [Table 4](D_pacs.md#table-4)) except that references to “PIV Card application” are replaced with “derived PIV application.”

#### Derived PIV Application PACS Cryptographic Algorithm and Mechanism Identifiers

The algorithm identifiers for the cryptographic algorithms that **MAY** be recognized for PACS use on the derived PIV application interfaces are the asymmetric identifiers specified in Table 9 and Table 10 of [[SP800-78]](references.md#ref-SP-800-78). The cryptographic mechanism identifiers that **MAY** be recognized on the derived PIV application interfaces are those specified in Table 5 of [[SP800-73pt1]](references.md#ref-SP-800-73pt1).

#### Derived PIV Application Status Words

The status words that **MAY** be returned for PACS use on the derived PIV application command interface are as specified in Sec. 5.6 of [[SP800-73pt1]](references.md#ref-SP-800-73pt1).

### Derived PIV PACS Authentication Mechanisms

The derived PIV application supports the following validation steps for PACS use:

- Credential validation (CredV) is established by verifying the certificates retrieved from the derived PIV application and checking the validity and revocation status of these certificates.

- As with the PKI-CAK and SM-AUTH authentication mechanisms for the PIV card, derived PIV holder validation (HolderV) for PACS is only established by possession of the derived PIV credential (i.e., these are single-factor authentication mechanisms).

Derived PIV applications that support PACS **SHALL** support PKI-CAK, a cryptographic challenge and response authentication protocol that uses the derived card authentication key as described in Appendix B.1.3 of [[SP800-73pt1]](references.md#ref-SP-800-73pt1). Derived PIV applications **MAY** also support SM-AUTH &mdash; a key establishment protocol that uses the derived PIV secure messaging key, as described in Appendix B.1.7 of [[SP800-73pt1]](references.md#ref-SP-800-73pt1). The following translations apply to the use of these protocols by a derived PIV credential:

- References to “PIV application” are replaced with “derived PIV application.”
- References to “Card auth certificate” are replaced with “derived card authentication certificate.”
- References to "SM parameters" are replaced with "derived SM parameters"
- References to “PIV Card app ID” are replaced with “derived PIV application ID.”

## Derived PIV Application Token Command Interface

This appendix contains the technical specifications for the command interface to the derived PIV application surfaced by the wireless interface to the derived PIV credential for PACS. The command interface for the derived PIV application **SHALL** implement a subset of the card commands supported by the PIV Card application, as described in [[SP800-73pt2]](references.md#ref-SP-800-73pt2), which include:

- SELECT
- GET DATA
- GENERAL AUTHENTICATE
- PUT DATA
- GENERATE ASYMMETRIC KEY PAIR

The specifications for the token command interface **SHALL** be the same as the specifications for the corresponding card edge commands for a PIV Card, as described in [[SP800-73pt2]](references.md#ref-SP-800-73pt2), except for the following deviations:

- References to “PIV Card application” are replaced with “derived PIV application.”
- References to “PIV data objects” are replaced with “derived PIV data objects.”
- References to “card authentication key” are replaced with “derived card authentication key.”
- In Appendix A:
    - References to “PIV Card application administrator” are replaced with “derived PIV application administrator.”
    - References to “card management key” are replaced with “derived PIV token management key.”

The token platform **SHALL** support a default selected application, which is the application chosen immediately following a cold or warm reset. This default application **MAY** be the derived PIV application or another application.

### Authentication of an Individual for PACS

The two authentication mechanisms for PACS are PKI-CAK and SM-AUTH, which rely only on possession of the derived PIV credential for holder validation (HolderV). Therefore, an activation secret is not used for enhanced holder validation.

## Invalidation of PACS Derived PIV

A derived PIV credential that is used for physical access **SHALL** be invalidated when the associated PIV identity account is terminated or when the PACS credential or the device on which it resides has been lost or compromised. The IdMS **SHALL** revoke the card authentication certificate associated with the lost or compromised device or all such certificates associated with the terminated PIV identity account. The home agency IdMS **SHOULD** direct all physical access control systems known to use the credential to remove it from their access control lists. 
