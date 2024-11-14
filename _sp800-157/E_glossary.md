---
layout: default
title: Glossary
navOrder: 9
navTitle: Glossary
permalink: /glossary/
anchor: s-e
section: E
---

# Glossary {#s-e}

*This appendix is informative.*

Selected terms used in this guideline are defined below. All other significant technical terms used within this document are defined in other key documents, including [[FIPS201]](references.md#ref-FIPS201), [[SP800-63A]](references.md#ref-SP-800-63A), [[SP800-63B]](references.md#ref-SP-800-63B), [[SP800-73pt1]](references.md#ref-SP-800-73pt1), and [[SP800-73pt2]](references.md#ref-SP-800-73pt2).

applicant
: A PIV cardholder who has applied for but has yet to be issued a derived PIV credential.

derived PIV application
: A standardized application based on the PIV Card's PIV application that resides on a removable or wireless cryptographic token. It hosts PKI-based derived PIV credentials and associated mandatory and optional elements.

derived PIV credential module
: A collection of objects (e.g., certificates, keys, etc.) that provide derived PIV functionality in a derived PIV application or other device.

home agency
: The government agency responsible for maintaining the PIV identity account and issuing a PIV Card. While another agency may sometimes perform the enrollment and identity proofing process, the home agency is responsible for monitoring ongoing eligibility and initiating termination if appropriate.

home agency IdMS
: An identity management system operated by the home agency or on their behalf by an authorized third party or shared service provider that houses the PIV identity accounts of cardholders.

PIV identity account
: The logical record that contains credentialing information for a given PIV cardholder. This is stored within the _home agency IdMS_ and includes PIV enrollment data, cardholder identity attributes, information regarding the cardholder's PIV card, and any derived PIV credentials bound to the account.

PKI-based derived PIV credential
: An X.509 derived PIV authentication certificate, which is issued in accordance with the requirements specified in this document, where one or more X.509 certificates on the applicant’s PIV Card serve as the original credential. The derived PIV credential is an additional common identity credential under HSPD-12 and FIPS 201 that a federal department or agency issues.

non-PKI-based derived PIV credential
: An authenticator (as defined in [[SP800-63B]](references.md#ref-SP-800-63B)) that has been bound to a PIV identity account at a subscriber's home agency that does not use the PKI-based authentication mechanisms described in [[FIPS201]](references.md#ref-FIPS201). A non-PKI-based derived PIV credential bound to the subscriber's PIV identity account can be used for federated authentication via the cardholder's home agency IdMS.

subscriber
: A PIV cardholder to whom a derived PIV credential has been issued.

verifier
: An entity that verifies the claimant's identity by verifying the claimant's possession and control of one or more authenticators using an authentication protocol. To do this, the verifier needs to confirm the authenticators' binding with the subscriber account and check that the subscriber account is active.
