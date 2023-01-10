---
layout: default
title: Example Issuance Processes
navOrder: 7
navTitle: Examples
permalink: /examples/
anchor: s-c
section: C
---

# Example Issuance Processes {#s-c}

*This appendix is informative.*

The issuance process for a derived PIV credential varies depending on whether the derived PIV credential is being issued at AAL2 or AAL3. [Section 2.2](2_lifecycle.md#s-2-2) specifies the requirements for initial issuance. This appendix provides two example issuance processes that satisfy those requirements: one at AAL2 and another at AAL3.

## Example Issuance of a Derived PIV Credential at AAL2 {#s-c-1}

The following is an example of a PKI-based derived PIV credential.

An employee requires a mobile device for work. The mobile device is ordered, and a request for the issuance of a derived PIV credential is submitted to the agency’s approval authority.

Following receipt of the device and approval, the employee starts the binding process remotely &mdash; such as from their home &mdash; by visiting a derived PIV credential website operated by or on behalf of their PIV Card's home agency. The website requires TLS client authentication using the PIV authentication certificate on the employee’s PIV Card. The employee performs this step from a desktop computer since they cannot use their PIV Card on a mobile device. By requiring and validating a PIV Authentication certificate when connecting to the website, the server authenticates the employee and verifies that the employee is still eligible to possess a PIV Card. If the employee successfully authenticates to the server, the issuer generates and displays a binding secret to the employee.

The employee then runs a provisioning application on the mobile device. The application asks the employee to identify themself and enter the binding secret that was previously provided from the desktop website to create an activation secret, which will subsequently be used to authenticate to the cryptographic module. The application generates a key pair within the device’s cryptographic module and submits the binding secret and newly generated public key to the PIV issuer as part of a certificate request. The PIV issuer authenticates the employee by verifying that the binding secret in the certificate request matches the one that it previously issued and forwards the public key to the CA, which signs and issues the derived PIV credential (i.e., the derived PIV authentication certificate). The provisioning application loads the derived PIV authentication certificate on the mobile device. The PIV Card issuer enters information about the new derived PIV credential into the subscriber's PIV identity account. The cardholder is notified of the binding of the new derived PIV credential.

Normative requirements for this process are given in [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 6.1.2.4 and in [Sec. 2.2](#s-2-2) of this document.

## Example Binding of a Derived PIV Credential at AAL3 {#s-c-2}

An employee requires a derived PIV credential to access a relying party using one or more endpoints that do not accommodate the direct use of a PIV Card. The employee requests a non-PKI-based authenticator capable of authentication at AAL3 and approval to use that authenticator as a derived PIV credential. The request is approved by the agency’s approval authority.

After receiving the approval and authenticator, the employee starts the binding process by authenticating with their PIV Card at a derived PIV credential website operated by or on behalf of the PIV cardholder's home agency. The employee additionally provides a biometric sample that can be verified against their PIV Card. The website requires TLS client authentication using the PIV authentication certificate on the employee’s PIV Card. The employee then inserts (connects) the authenticator to be used as a derived PIV credential and registers (binds) that credential, including establishing a second authentication factor (activation secret or biometric characteristic) if that has not already been done. The website determines whether the authenticator meets AAL3 requirements. Upon successful registration, the subscriber's key and appropriate metadata are stored for use by the home agency's endpoint for non-PKI-based PIV authentication. The PIV Card issuer enters information about the new derived PIV credential into the subscriber's PIV identity account. The cardholder is notified of the binding of the new derived PIV credential.

If the authenticator uses verifier name binding as described in [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 5.2.5.2, the website used to register the authenticator has to share the same domain name as will be used by the home agency to authenticate the subscriber so that the same keys are used for registration and authentication.

