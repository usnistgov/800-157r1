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

The issuance process for a derived PIV credential varies depending on whether it is being issued for use at AAL2 or AAL3. [Section 2.2](2_lifecycle.md#s-2-2) specifies the requirements for initial issuance. This appendix provides example issuance processes that satisfy those requirements at AAL2 and at AAL3. These examples assume the PKI-AUTH authentication mechanism will be used with a valid PIV Card to enable the issuance process.

## Example Issuance of a PKI-Based Derived PIV Credential at AAL3 {#s-c-1}

An employee requires a derived PIV credential to access a relying party application that requires authentication at AAL3. Their endpoint does not easily accommodate their PIV Card, and the application resides at a different agency that does not support federation, so a PKI-based credential is needed. A request to issue a derived PIV credential is submitted to the agency’s approval authority and is approved.

The employee visits their security office or other issuing authority. If the issuance of a derived PIV credential has been approved, they are provided with a USB authenticator capable of supporting the derived PIV application and meeting AAL3 requirements. After authenticating with their PIV Card using the PKI-AUTH authentication mechanism, the USB authenticator is provisioned, which involves the generation of a key pair for the derived PIV authentication certificate within the device's cryptographic module and export of the public key to the IDMS, which generates the certificate and loads it onto the authenticator. The employee is also prompted to establish an activation secret for the credential. The issuer enters information about the new derived PIV credential into the subscriber's PIV identity account. The employee is notified of the binding of the new derived PIV credential by email or postal notification to their address in the PIV identity account.

Additional data elements described in [Appendix B.1.2](B_model.md#s-b-1-2) may also be provisioned on the device.

## Example Issuance of a PKI-Based Derived PIV Credential at AAL2 {#s-c-2}

An employee requires a mobile device for work. The mobile device is ordered, and a request to issue a derived PIV credential is submitted to the agency’s approval authority.

Following receipt of the device and approval, the employee starts the binding process remotely &mdash; such as from their home &mdash; by visiting a derived PIV credential website operated by or on behalf of their PIV Card's home agency IDMS. The website requires TLS client authentication using the PKI-AUTH authentication method with the employee’s PIV Card. The employee performs this step from a desktop computer since they cannot use their PIV Card on a mobile device. Having authenticated the employee, the server verifies PIV credential eligibility in the employee's PIV identity account. Once the employee has successfully authenticated to the server, the issuer generates and displays a binding secret to the employee.

The employee then runs a provisioning application on the mobile device. The application asks the employee to identify themselves and enter the binding secret previously provided from the desktop website to create an activation secret, which will subsequently be used to authenticate to the cryptographic module. The application generates a key pair within the device’s cryptographic module and submits the binding secret and newly generated public key to the PIV issuer as part of a certificate request. The PIV issuer authenticates the employee by verifying that the certificate request's binding secret matches the one it previously issued and forwards the public key to the CA, which signs and issues the derived PIV credential (i.e., the derived PIV authentication certificate). The provisioning application loads the derived PIV authentication certificate on the mobile device. The PIV Card issuer enters information about the new derived PIV credential into the subscriber's PIV identity account. The cardholder is notified of the binding of the new derived PIV credential by email or postal notification to their address in the PIV identity account.

Normative requirements for this process are given in [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 4.1.2.2 and in [Sec. 2.2](2_lifecycle.md#s-2-2) of this document.

## Example Binding of a Non-PKI-Based Derived PIV Credential at AAL3 {#s-c-3}

An employee requires a derived PIV credential to access a relying party using one or more endpoints that do not accommodate the direct use of a PIV Card. The employee requests a non-PKI-based authenticator capable of authentication at AAL3 and approval to use that authenticator as a derived PIV credential. The agency’s approval authority approves the request.

After receiving the approval and authenticator, the employee starts the binding process by authenticating with their PIV Card using PKI-AUTH at a derived PIV credential website operated by or on behalf of the employee's home agency IdMS. The website requires TLS client authentication with the PKI-AUTH authentication method using the employee’s PIV Card. Having authenticated the employee, the server verifies eligibility to possess a PIV Card. The employee then inserts (connects) the authenticator to be used as a derived PIV credential and registers (binds) that credential, including establishing a second authentication factor (activation secret or biometric characteristic) if that has not already been done. The website determines whether the authenticator meets AAL3 requirements. Upon successful registration, the home agency's endpoint stores the subscriber's key and appropriate metadata for non-PKI-based PIV authentication. The PIV Card issuer enters information about the new derived PIV credential into the subscriber's PIV identity account. The employee is notified of the binding of the new derived PIV credential by email or postal notification to their address in the PIV identity account.

If the authenticator uses verifier name binding as described in [[SP800-63B]](references.md#ref-SP-800-63B) Sec. 3.2.5.2, the website used to register the authenticator has to share the same domain name as will be used by the home agency IdMS to authenticate the subscriber so that the same keys are used for registration and authentication.

## Example Binding of a Non-PKI-Based Derived PIV Credential at AAL2 {#s-c-4}

The binding of a non-PKI-based derived PIV credential at AAL2 is identical to that at AAL3, except that the authenticator needs only to meet the requirements of AAL2.

## Example Binding of PACS Credential

To enable a derived PIV credential to be used for physical access as described in [Appendix D](D_pacs.md#s-d), the applicant first authenticates using their PIV Card and the PKI-AUTH authentication method. Having authenticated the employee, the server verifies PIV credential eligibility in the applicant's PIV identity account. The issuer generates a new CHUID data object, derived card authentication key, and derived card authentication certificate. If the SM-AUTH authentication method is supported, a key pair is generated. The issuer creates a corresponding derived card verifiable certificate and secure messaging certificate signer object. The issuer transfers the created objects to the derived PIV credential module using a TLS or similar authenticated protected channel. Because the PACS credential is a single authentication factor, it is not necessary to establish an activation factor.

The PIV Card issuer enters information about the new derived PIV credential into the subscriber's PIV identity account. The cardholder is notified of the binding of the new derived PIV credential.
