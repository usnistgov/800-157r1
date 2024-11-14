---
layout: default
title: Introduction
navOrder: 1
navTitle: Introduction
permalink: /introduction/
anchor: s-1
section: 1
---
# Introduction {#s-1}

*This section is informative.*

[[FIPS 201]](references.md#ref-FIPS201) specifies a common set of identity credentials to satisfy the requirements of [[HSPD-12]](references.md#ref-HSPD-12) in a smart card form factor known as the Personal Identity Verification (PIV) Card. This publication is a companion document to FIPS 201 that specifies the use of additional common identity credentials, known as derived PIV credentials, issued by a federal department or agency and may be used when using a PIV Card is impractical. Consistent with the goals of HSPD-12, derived PIV credentials are designed to serve as a Federal Government-wide standard for a secure and reliable identity credential that supports interoperability across agencies.

## Background {#s-1-1}

FIPS 201 originally required that the PIV credential and associated keys be stored in a PIV Card. While
using the PIV Card for electronic authentication works well with many traditional desktop and laptop
computers, it needs to be better suited to other devices, such as mobile devices. In response to the growing use of mobile endpoints within
the Federal Government, FIPS 201-2 permitted the issuance of additional PKI-based credentials, referred to as
derived PIV credentials, for which the corresponding private key is stored in a cryptographic module within
a mobile device, such as a smartphone. PKI-based derived PIV credentials use the Federal Public Key Infrastructure (FPKI) to securely establish the binding between the credential and the PIV identity account. PKI-based derived PIV credentials are typically integrated into user endpoints, such as mobile devices, although they are not limited to use in these devices.

To provide additional flexibility for federal departments and agencies, FIPS 201-3 expands the set of credentials beyond those that are PKI-based and broadens their use to other types of devices in addition to mobile devices. This document &mdash; NIST Special Publication (SP) 800-157r1 (Revision 1) &mdash; describes the expanded set of derived PIV credentials in a variety of form factors. Non-PKI-based derived PIV credentials are cryptographic authenticators (as defined in [[SP800-63B]](references.md#ref-SP-800-63B)) that are phishing-resistant. They may be separate from the endpoint being authenticated and, if so, are connected to the endpoint for that purpose. Since there is no PKI infrastructure to validate and supply attributes for non-PKI-based derived PIV credentials, non-PKI-based derived PIV credentials are always used to authenticate to the home agency IdMS of the PIV cardholder from which the cardholder's PIV identity account is accessed. When access to the PIV identity account is needed outside of the cardholder's home agency &mdash; particularly when a non-PKI-based derived PIV credential is presented in authentication &mdash; federation allows for connection across security domains as detailed in [[SP800-217]](references.md#ref-SP-800-217). In the case of non-PKI derived PIV credentials, attributes are obtained from the PIV identity account rather than from the derived PIV credential itself.

> Note: The PIV identity account is frequently implemented as multiple linked database records with potentially different access restrictions within the enterprise IDMS, which is the central repository for the cardholder’s digital identities. References to the PIV identity account apply to the relevant linked record, the structure of which is determined by the issuing agency.

Derived PIV credentials leverage the current investment in the PIV infrastructure for electronic authentication and build upon the solid foundation of the well-vetted and trusted identity of the PIV cardholder as represented in the PIV identity account, achieving substantial cost savings by leveraging the identity proofing results that were already performed to issue PIV Cards. This document provides technical guidelines for the implementation of derived PIV credentials.

## Purpose and Scope {#s-1-2}

This document provides guidelines for cases in which PIV Cards are deemed impractical for authentication and specifies the use of authenticators with alternative form factors to the PIV Card that may be inserted into endpoints (e.g., USB authenticators, authenticators that are connected wirelessly to endpoints, and authenticators that are embedded in endpoints). Authenticators used as derived PIV credentials must meet the requirements for cryptographic authenticators and must be phishing-resistant. Examples of suitable authentication processes include client-authenticated TLS and WebAuthn [[WebAuthn]](references.md#ref-WebAuthn). Using alternative form factors greatly improves the usability of electronic authentication to remote IT resources while simultaneously maintaining the goals of HSPD-12 for common identification that is secure, reliable, and has government-wide interoperability.

The purpose of the derived PIV credential is to provide PIV-enabled authentication services on alternative endpoints to authenticate the credential holder to remote systems. As described in [Appendix D](D_pacs.md#s-d), derived PIV credentials can also be used for physical access.

To achieve interoperability with the PIV infrastructure and its applications, two approaches to derived PIV credentials have been selected:

1. Use of public key infrastructure (PKI) technology. PKI-based derived PIV credentials rely on the same infrastructure used for authentication with a PIV Card. Cross-domain use of PKI-based derived PIV credentials is supported in the same manner as for PIV Cards.

2. Use of non-PKI-based authenticators. Non-PKI authenticators rely on IdAM infrastructure to allow for direct authentication by the home agency. Cross-domain use of non-PKI-based derived PIV credentials is supported through federation protocols, as specified in [[SP800-217]](https://github.com/usnistgov/800-157r1-dev/pull/references.md#ref-SP-800-217).

The derived PIV credentials specified in this document are issued at authentication assurance level (AAL) 2 or 3. Derived PIV credentials are issued at identity assurance level (IAL) 3, which is the identity proofing and issuance level associated with the PIV Card and bound to the PIV identity account, as per [[FIPS201]](references.md#ref-FIPS201).

Derived PIV credentials are based on the general concept of post-enrollment authenticator binding in [[SP800-63B]](references.md#ref-SP-800-63B), which leverages identity proofing and vetting associated with an existing subscriber account using current and valid authenticators to bind additional authenticators to that account. Identity proofing and vetting processes do not have to be repeated to issue a derived PIV credential. Instead, the user proves possession and control of a valid PIV Card to bind a derived PIV credential to their PIV identity account. The PIV Card may be used as the basis for issuing other types of derived credentials, but those credentials would not be bound to the PIV identity account and are therefore outside of this document's scope.

While non-PKI derived PIV credentials are different in nature from PIV Cards and PKI-based derived PIV credentials, they are nevertheless considered to be derived PIV credentials due to their binding to the cardholder's PIV identity account. Other authenticator requirements such as strength (AAL) and phishing resistance are additionally required for suitability as derived PIV credentials. 

Derived PIV credentials are:

* Issued based on possession and control of the PIV Card,
* Represented in the PIV identity account at the home agency IdMS, and
* Issued in accordance with this document.

This document provides technical guidelines on:

* The primary life cycle activities for the derived PIV credential (i.e., initial issuance, maintenance, and termination) and the requirements for each activity to ensure security and
* The derived PIV credential, including cryptographic specifications, permitted implementation types, mechanisms for activation, use of the credential, and certificate policies, if applicable.

This publication includes an informative appendix that provides recommendations for including digital signature and key management keys on devices that host a derived PIV credential. It also includes an annex with guidelines for the issuance and use of derived PIV credentials for facility access.

## Audience {#s-1-3}

This document is intended for stakeholders who are responsible for procuring, designing, implementing, and managing deployments of derived PIV credentials for mobile devices and other endpoints.

## Requirements Notation and Conventions {#s-1-4}

This standard uses the following typographical conventions in text:

- Specific terms in **CAPITALS** represent normative requirements. When these same terms are not in **CAPITALS**, the term does not represent a normative requirement. 
    - The terms "**SHALL**" and "**SHALL NOT**" indicate requirements to be strictly followed to conform to the publication and from which no deviation is permitted.
    - The terms "**SHOULD**" and "**SHOULD NOT**" indicate that among several possibilities, one is recommended as particularly suitable without mentioning or excluding others, that a certain course of action is preferred but not necessarily required, or that (in the negative form) a certain possibility or course of action is discouraged but not prohibited.
    - The terms "**MAY**" and "**NEED NOT**" indicate a course of action permissible within the limits of the publication.
    - The terms "**CAN**" and "**CANNOT**" indicate a possibility and capability &mdash; whether material, physical, or causal &mdash; or, in the negative, the absence of that possibility or capability.


## Document Structure {#s-1-5}

This document is organized as follows. Each section is labeled as either normative (i.e., mandatory for compliance) or informative (i.e., not mandatory).

* Section 2 describes derived PIV credential life cycle activities and related requirements. This section is *normative*.
* Section 3 describes the technical requirements for implementing derived PIV credentials. This section is *normative*.
* Appendix A contains guidance on digital signature and key management keys. This appendix is *informative*.
* Appendix B provides detailed interface requirements for PKI-based removable (non-embedded) and PKI-based wireless implementations for logical access. This appendix is *normative* for implementing PKI-based derived PIV credentials on removable (non-embedded) or wireless cryptographic authenticators.
* Appendix C provides examples of issuance processes for derived PIV credentials. This appendix is *informative*.
* Appendix D provides detailed requirements for using derived PIV credentials in physical access control systems (PACS). This appendix is *normative* for derived PIV credentials used for physical access.
* Appendix E contains a glossary of selected terms used in this document. This appendix is *informative*.
* Appendix F defines acronyms and other abbreviations used in this document. This appendix is *informative*.
* Appendix G lists changes made to this document since its initial release. This appendix is *informative*.

## Key Terminology {#s-1-6}

Certain key PIV terms have assigned meanings within the context of this document. The term *PIV cardholder* refers to a person who possesses a valid PIV Card, regardless of whether they have been issued a derived PIV credential. The term *applicant* refers to a PIV cardholder who has applied for but has yet to be issued a derived PIV credential, and the term *subscriber* refers to a PIV cardholder to whom a derived PIV credential has been issued.
