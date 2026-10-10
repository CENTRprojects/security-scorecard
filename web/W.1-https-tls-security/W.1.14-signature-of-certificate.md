# W.1.14: Signature of Certificate

## Summary

Checks whether the website's TLS certificate was signed with a secure hashing algorithm, ensuring the certificate's fingerprint cannot be forged using weak cryptography.

## Test Procedure

1. Retrieve the TLS certificate presented by the web server during the HTTPS handshake.
2. Identify the signature hash algorithm used to sign the certificate (the **`signatureAlgorithm`** field in the certificate).
3. Classify the algorithm:

### Hash function classification (NCSC-NL TLS Guidelines v2.1, guideline B3-2, table 3):

| Hash function | Classification |
| --- | --- |
| SHA-512, SHA-384, SHA-256 | Good |
| SHA-224 | Phase out |
| SHA-1, MD5 | Insufficient |

4. The test passes if all presented certificates are signed with a Good hash algorithm.

## Scoring

| Result | Score |
| --- | --- |
| All certificates signed with SHA-256, SHA-384, or SHA-512 | Pass |
| Any certificate signed with SHA-1, SHA-224 or MD5 | Fail |
| HTTPS not available (W.1.1 failed) | Not Executed |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Web | Test 5.3 | Primary source |
| NCSC-NL TLS Guidelines 2025-05 | Section 3.3.5, Table 9 | Hash functions for TLS |
