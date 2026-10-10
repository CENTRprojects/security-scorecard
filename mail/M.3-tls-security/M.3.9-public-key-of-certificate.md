# M.3.9: Public Key of Certificate

## Summary

Checks whether each receiving mail server (MX host) presents a certificate whose public key uses secure cryptographic parameters (curve or key length).

## Test Procedure

After STARTTLS negotiation with each MX host (per M.3.1):

1. Retrieve the TLS certificate presented by the server during the handshake.
2. Determine the public key algorithm and parameters:

### ECDSA certificates — elliptic curve classification (NCSC-NL TLS Guidelines 2025-05, Section 3.3.2.1, table 3):

| Curve | Classification |
| --- | --- |
| Secp521r1, secp384r1, secp256r1, x448, x25519 | Sufficient |
| secp224r1 | Phase out |
| Other curves | Insufficient |

### RSA certificates — key length classification (NCSC-NL TLS Guidelines 2025-05, Section 3.3.2.1 , table 4):

| Key length | Classification |
| --- | --- |
| ≥ 3072 bits | Sufficient |
| 2048–3071 bit | Phase out |
| \< 2048 bit | Insufficient |

### EDSA certificates – Edwards curve classification

| Elliptic curve | Classification | Cryptographic strength |
| --- | --- | --- |
| Ed448 | Sufficient | 224 bits |
| Ed25519 | Sufficient | 128 bits |
| Other Edwards curves | Insufficient |  |

3. Multiple certificates may be presented (e.g., for ECDSA and RSA simultaneously). Evaluate all presented certificates.
4. The test passes if all presented certificates use Good or Sufficient parameters.

Note: Sending mail servers often ignore whether a mail server certificate is issued by a publicly trusted CA. Without DNSSEC and DANE, certificate-based authentication provides limited value for mail. RSA is considered Good for certificate purposes, though Phase out for key exchange.

## Scoring

| Result | Score |
| --- | --- |
| All presented certificates use Good or Sufficient public key parameters | Pass |
| Any certificate uses Phase out or Insufficient parameters | Fail |
| STARTTLS not available (M.3.1 failed or N/A) | Not Executed |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Mail | Test 5.2 | Primary source |
| NCSC-NL TLS Guidelines 2025-05 | Section 3.3.2.1 Table 3 (ECDSA), Table 4 (RSA) and Table 5 (EdDSA) | Secure parameters for authentication |
