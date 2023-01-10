---
layout: default
title: Digital Signature and Key Management Keys
navOrder: 5
navTitle: Keys
permalink: /keys/
anchor: s-a
section: A
---
# Digital Signature and Key Management Keys {#s-a}

*This appendix is informative.*

In addition to the PIV authentication keys, [[FIPS201]](references.md#ref-FIPS201) also requires each PIV Card to have a digital signature key and a key management key unless the cardholder does not have a government-issued email account at the time of credential issuance. A subscriber who has been issued a derived PIV credential may also need a digital signature and key management key.

For most subscribers, it will be necessary to store a copy of the PIV Card's key management private key and certificate in the keystore that hosts the derived PIV credential. Similarly, copies of some or all of the PIV Card's retired key management private keys and certificates should be stored in the derived PIV credential keystore. Neither [[FIPS201]](references.md#ref-FIPS201) nor [[COMMON]](references.md#ref-COMMON) precludes a key management private key from being used on more than one device (e.g., the PIV Card and a derived PIV credential keystore) as long as all of the requirements of the policy under which the key management certificate was issued are satisfied. This means that in order to use a copy of a key management private key in a [[FIPS140]](references.md#ref-FIPS140) Level 1 software cryptographic module, the corresponding certificate would have to be issued under a certificate policy, such as `id-fpki-common-policy`, that does not require the use of a [[FIPS140]](references.md#ref-FIPS140) Level 2 hardware cryptographic module. This should be taken into account at the time that the key management certificate that will be placed on the PIV Card is issued. Key recovery mechanisms are encouraged for key management keys that will be used on derived PIV credential keystores.

As the digital signature key on a PIV Card cannot be copied, a new digital signature private key will need to be generated and a corresponding certificate will need to be issued for the derived PIV credential keystore. The issuance of this private key and certificate is independent of the issuance of the PIV Card. As the certificate policies associated with digital signature certificates in [[COMMON]](references.md#ref-COMMON) (`id-fpki-common-policy`, `id-fpki-common-hardware`, and `id-fpki-common-High`) are not limited to use with PIV Cards, a digital signature certificate for a derived PIV credential keystore may be issued under one of these policies as long as all of the policy requirements are satisfied.
