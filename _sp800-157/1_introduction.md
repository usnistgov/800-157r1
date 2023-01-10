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

[[FIPS 201]](references.md#ref-FIPS201) specifies a common set of identity credentials to satisfy the requirements of [[HSPD-12]](references.md#ref-HSPD-12) in a smart card form factor known as the Personal Identity Verification (PIV) Card. This publication is a companion document to FIPS 201 that specifies the use of additional common identity credentials, known as derived PIV credentials, that are issued by a federal department or agency and may be used when the use of a PIV Card is not practical. Consistent with the goals of HSPD-12, derived PIV credentials are designed to serve as a Federal Government-wide standard for a secure and reliable identity credential that supports interoperability across agencies.

## Background {#s-1-1}

FIPS 201 originally required that the PIV credential and associated keys be stored in a PIV Card. While
the use of the PIV Card for electronic authentication works well with many traditional desktop and laptop
computers, it is not well-suited to other devices, such as mobile devices. In response to the growing use of mobile endpoints within
the Federal Government, FIPS 201-2 permitted the issuance of additional PKI-based credentials, referred to as
derived PIV credentials, for which the corresponding private key is stored in a cryptographic module within
a mobile device, such as a smartphone. PKI-based derived PIV credentials use the Federal PKI Infrastructure to securely establish the binding between the credential and the PIV identity account. PKI-based derived PIV credentials are typically integrated into user endpoints, such as mobile devices, although they are not limited to use in these devices.

In order to provide additional flexibility for federal departments and agencies, FIPS 201-3 expands the set of credentials beyond those that are PKI-based and broadens their use to other types of devices in addition to mobile devices. The technical details for the expanded set of derived PIV credentials is specified in this revision of SP 800-157 (SP 800-157, Revision 1) in a variety of form factors. Non-PKI-based derived PIV credentials are authenticators (as defined in [[SP800-63B]](references.md#ref-SP-800-63B)) that may be separate from the endpoint being authenticated and, if so, are connected to the endpoint for that purpose. Since there is no PKI infrastructure to validate and supply attributes for non-PKI-based derived PIV credentials, non-PKI-based derived PIV credentials are always used to authenticate to the home agency of the PIV cardholder from which the cardholder's PIV identity account is accessed. When access to the PIV identity account is needed outside of the home agency &mdash; particularly when a non-PKI-based derived PIV credential is presented in authentication &mdash; federation allows connection across security domains as detailed in [[SP800-217]](references.md#ref-SP-800-217).

Derived PIV credentials leverage the current investment in the PIV infrastructure for electronic authentication and build upon the solid foundation of the well-vetted and trusted identity of the PIV cardholder as represented in the PIV identity account, achieving substantial cost savings by leveraging the identity proofing results that were already performed to issue PIV Cards. This document provides technical guidelines for the implementation of derived PIV credentials.

## Purpose and Scope {#s-1-2}

This document provides guidelines for cases in which the use of PIV Cards is deemed impractical for authentication. This guideline specifies the use of authenticators with alternative form factors to the PIV Card that may be inserted into endpoints, such as USB authenticators, authenticators that are connected wirelessly to endpoints, or authenticators that are embedded in endpoints. Authenticators used as derived PIV credentials must meet the requirements for either hardware or software cryptographic authenticators. The use of alternative form factors greatly improves the usability of electronic authentication to remote IT resources while simultaneously maintaining the goals of HSPD-12 for common identification that is secure, reliable, and has government-wide interoperability.

The purpose of the derived PIV credential is to provide PIV-enabled authentication services on alternative endpoints in order to authenticate the credential holder to remote systems.

To achieve interoperability with the PIV infrastructure and its applications, two approaches to derived PIV credentials have been selected:

1. Use of public key infrastructure (PKI) technology. PKI-based derived PIV credentials rely on the same infrastructure as that used for authentication with a PIV Card.

2. Use of non-PKI-based authenticators. When non-PKI-based authenticators are used, derived PIV credentials are only used to authenticate with the home agency of the associated PIV Card. Interoperability with other agencies is achieved through the use of federation protocols, as specified in [[SP800-217]](references.md#ref-SP-800-217).

The derived PIV credentials specified in this document are issued at authentication assurance level (AAL) 2 or 3.

Derived PIV credentials are based on the general concept of post-enrollment authenticator binding in [[SP800-63B]](references.md#ref-SP-800-63B), which leverages identity proofing and vetting associated with an existing subscriber account using current and valid authenticators to bind additional authenticators to that account. Identity proofing and vetting processes do not have to be repeated to issue a derived PIV credential. Instead, the user proves possession and control of a valid PIV Card to bind a derived PIV credential to their PIV identity account. While the PIV Card may be used as the basis for issuing other types of derived credentials, the issuance of these other credentials is outside of the scope of this document. 

Derived PIV credentials are:

* Issued based on possession and control of the PIV Card,
* Represented in the PIV identity account at the home agency, and
* Issued in accordance with this document.

This document provides technical guidelines on:

* The primary lifecycle activities for the derived PIV credential &mdash; initial issuance, maintenance, and termination &mdash; and the requirements for each activity to ensure security and
* The derived PIV credential, including cryptographic specifications, types of implementation that are permitted, mechanisms for activation and use of the credential, and certificate policies if applicable.

This publication also includes an informative annex that provides recommendations for the inclusion of digital signature and key management keys on devices that host a derived PIV credential.

## Audience {#s-1-3}

This document is intended for stakeholders who will be responsible for procuring, designing, implementing, and managing deployments of derived PIV credentials for mobile devices and other endpoints.

## Requirements Notation and Conventions {#s-1-4}

This standard uses the following typographical conventions in text:

- Specific terms in **CAPITALS** represent normative requirements. When these same terms are not in **CAPITALS**, the term does not represent a normative requirement. 
    - The terms "**SHALL**" and "**SHALL NOT**" indicate requirements to be strictly followed in order to conform to the publication and from which no deviation is permitted.
    - The terms "**SHOULD**" and "**SHOULD NOT**" indicate that among several possibilities, one is recommended as particularly suitable without mentioning or excluding others, that a certain course of action is preferred but not necessarily required, or that (in the negative form) a certain possibility or course of action is discouraged but not prohibited.
    - The terms "**MAY**" and "**NEED NOT**" indicate a course of action permissible within the limits of the publication.
    - The terms "**CAN**" and "**CANNOT**" indicate a possibility and capability &mdash; whether material, physical, or causal &mdash; or, in the negative, the absence of that possibility or capability.


## Document Structure {#s-1-5}

This document is organized as follows. Each section is labeled as either normative (i.e., mandatory for compliance) or informative (i.e., not mandatory).

* Section 2 describes derived PIV credential lifecycle activities and related requirements. This section is *normative*.
* Section 3 describes the technical requirements for implementing derived PIV credentials. This section is *normative*.
* Appendix A contains guidance on digital signature and key management keys. This appendix is *informative*.
* Appendix B provides detailed interface requirements for PKI-based removable (non-embedded) and PKI-based wireless hardware implementations. This appendix is *normative* for implementation of PKI-based derived PIV credentials on removable (non-embedded) or wireless hardware cryptographic tokens.
* Appendix C provides example issuance processes for derived PIV credentials. This appendix is *informative*.
* Appendix D contains a glossary of selected terms used in this document. This appendix is *informative*.
* Appendix E defines acronyms and other abbreviations used in this document. This appendix is *informative*.
* Appendix F provides a list of changes made to this document since its initial release. This appendix is *informative*.

## Key Terminology {#s-1-6}

Certain key PIV terms have assigned meanings within the context of this document. The term *PIV cardholder* refers to a person who possesses a valid PIV Card, regardless of whether they have been issued a derived PIV credential. The term *applicant* refers to a PIV cardholder who has applied for but not yet been issued a derived PIV credential, and the term *subscriber* refers to a PIV cardholder to whom a derived PIV credential has been issued.
