# M.3.10: Signature of Certificate

## Summary

Checks whether each receiving mail server (MX host) presents a certificate whose fingerprint (signature) was created with a secure hashing algorithm.

## Test Procedure

After STARTTLS negotiation with each MX host (per M.3.1):

1. Retrieve the TLS certificate(s) presented by the server during the handshake.
2. For each certificate, identify the signature hash algorithm used to sign the certificate (the **`signatureAlgorithm`** field in the certificate).
3. Classify the algorithm:

### Hash function classification (NCSC-NL TLS Guidelines 2025-05, Section 3.3.5, table 9):

| Hash function | Classification |
| --- | --- |
| SHA-512, SHA-384, SHA-256 | Good |
| SHA-224 | Phase Out |
| SHA-1, MD5 | Insufficient |

4. The test passes if all presented certificates are signed with a Good hash algorithm.

## Scoring

| Result | Score |
| --- | --- |
| All certificates signed with SHA-256, SHA-384, or SHA-512 | Pass |
| Any certificate signed with SHA-224, SHA-1 or MD5 | Fail |
| STARTTLS not available (M.3.1 failed or N/A) | Not Executed |

### Note

the list of valid algorithms is not static and should be updated regularly to remain compliant with the latest standards (see, for example, NIST policy: https://csrc.nist.gov/Projects/HashFunctions/NIST-Policy-on-Hash-Functions).

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Mail | Test 5.3 | Primary source |
| NCSC-NL TLS Guidelines 2025-05 | Section 3.3.5, Table 9 | Hash functions for TLS |
