# M.3.6: Hash Function for Key Exchange

## Summary

Checks whether each receiving mail server (MX host) supports secure hash functions (SHA-256, SHA-384, or SHA-512) for creating the digital signature during the TLS key exchange.

## Test Procedure

After STARTTLS negotiation with each MX host (per M.3.1):

1. During the TLS handshake, record the signature algorithms advertised and/or selected by the server for the key exchange digital signature.
2. Check whether any of SHA-256, SHA-384, or SHA-512 is supported.

### Hash function classification (NCSC-NL TLS Guidelines 2025-05, Section 3.3.5, Table 5):

| Hash function | Classification |
| --- | --- |
| SHA-256, SHA-384, SHA-512 | Good |
| SHA-224 | Phase out |
| SHA-1, MD5, or older | Insufficient |

3. The test passes if at least one Good hash function is supported.

Note: Requirement level is Recommended.

## Scoring

| Result | Score |
| --- | --- |
| At least SHA-256, SHA-384, or SHA-512 supported for key exchange signatures | Pass |
| Only Phase out or insufficient hash functions supported | Fail |
| STARTTLS not available (M.3.1 failed or N/A) | Not Executed |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Mail | Test 4.6 | Primary source |
| NCSC-NL TLS Guidelines 2025-05 | Section 3.3.5, Table 5 | Algorithms for hash functions, their security level and cryptographic strength, based on collision resistance |
