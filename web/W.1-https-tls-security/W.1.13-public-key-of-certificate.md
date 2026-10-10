# W.1.13: Public Key of Certificate

## Summary

Checks whether the website's TLS certificate uses secure public key parameters (ECDSA curve or RSA key length), ensuring the cryptographic strength of the certificate's digital signature.

## Test Procedure

1. Retrieve the TLS certificate presented by the web server during the HTTPS handshake.
2. Determine the public key algorithm and parameters:

### ECDSA certificates — elliptic curve classification (NCSC-NL TLS Guidelines 2025-05, Section 3.3.2 , table 3):

| Curve | Classification |
| --- | --- |
| secp521r1, secp384r1, secp256r1, x448, x25519 | Sufficient |
| secp224r1 | Phase out |
| Other curves | Insufficient |

### EDSA certificates – Edwards curve classification (NCSC-NL TLS Guidelines 2025-05, Section 3.3.2, table 5):

| Elliptic curve | Classification | Cryptographic strength |
| --- | --- | --- |
| Ed448 | Sufficient | 224 bits |
| Ed25519 | Sufficient | 128 bits |
| Other Edwards curves | Insufficient |  |

### RSA certificates — key length classification (NCSC-NL TLS Guidelines 2025-05, Section 3.3.2 , table 4):

| Key length | Classification |
| --- | --- |
| ≥ 3072 bit | Sufficient |
| 2048–3071 bit | Phase out |
| \< 2048 bit | Insufficient |

3. Multiple certificates may be configured (e.g., one ECDSA and one RSA certificate). Evaluate all presented certificates.
4. The test passes if all presented certificates use Good or Sufficient parameters.

## Scoring

| Result | Score |
| --- | --- |
| All presented certificates use Good or Sufficient public key parameters | Pass |
| Any certificate uses Phase out or Insufficient parameters | Fail |
| HTTPS not available (W.1.1 failed) | Not Executed |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Web | Test 5.2 | Primary source |
| NCSC-NL TLS Guidelines 2025-05 |  | Key parameter classification |
