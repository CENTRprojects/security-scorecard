# W.1.8: Hash Function for Key Exchange

## Summary

Checks whether the web server supports secure hash functions (SHA-256, SHA-384, or SHA-512) for creating the digital signature during the TLS key exchange.

## Test Procedure

During the TLS handshake with the web server:

1. Record the signature algorithms advertised and/or selected by the server for the key exchange digital signature.
2. Check whether any of SHA-256, SHA-384, or SHA-512 is supported.

### Hash function classification (NCSC-NL TLS Guidelines 2025-05, Table 9):

| Hash function | Classification |
| --- | --- |
| SHA-512, SHA-384, SHA-256, , | Good |
| SHA-224 | Phase out |
| SHA-1, MD5, or older | Insufficient |

3. The test passes if at least one Good hash function is supported.

Note: Requirement level is Recommended.

## Scoring

| Result | Score |
| --- | --- |
| At least one good hash function supported for key exchange signatures | Pass |
| Only Phase out or insufficient hash functions supported | Fail |
| HTTPS not available (W.1.1 failed) | Not Executed |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Web | Test 4.5 | Primary source |
| NCSC-NL TLS Guidelines 2025-05 | Table 9 | Hash functions for TLS |
