---
layout: default
title: Glossary
navOrder: 8
navTitle: Glossary
permalink: /glossary/
anchor: s-d
section: D
---

# Glossary {#s-d}

*This appendix is informative.*

Selected terms used in the guideline are defined below. All other significant technical terms used within this document are defined in other key documents, including [[FIPS201]](references.md#ref-FIPS201), [[SP800-63A]](references.md#ref-SP-800-63A), [[SP800-63B]](references.md#ref-SP-800-63B), and [[SP800-73]](references.md#ref-SP-800-73).

applicant
: A PIV cardholder who has applied for but has not yet been issued a derived PIV credential.

derived PIV application
: A standardized application based on the PIV Card's PIV application that resides on a removable or wireless hardware cryptographic token. It hosts a PKI-based derived PIV credential and associated mandatory and optional elements.

home agency
: The government agency responsible for maintaining the PIV identity account and issuing a PIV Card. While another agency may perform the enrollment and identity proofing process in some cases, the home agency is responsible for monitoring ongoing eligibility and initiating termination if appropriate.

PKI-based derived PIV credential
: An X.509 derived PIV authentication certificate, which is issued in accordance with the requirements specified in this document where the PIV authentication certificate on the applicant’s PIV Card serves as the original credential. The derived PIV credential is an additional common identity credential under HSPD-12 and FIPS 201 that is issued by a federal department or agency.

non-PKI-based derived PIV credential
: An authenticator that has been bound to a PIV identity account at a subscriber's home agency and that can be used for federated authentication to applications as an alternative to the subscriber's PIV Card.

subscriber
: A PIV cardholder to whom a derived PIV credential has been issued.

verifier
: An entity that verifies the claimant's identity by verifying the claimant's possession and control of one or more authenticators using an authentication protocol. To do this, the verifier needs to confirm the binding of the authenticators with the subscriber account and check that the subscriber account is active.
