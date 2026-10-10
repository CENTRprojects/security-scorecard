# W.1.12: Trust Chain of Certificate

## Summary

Checks whether a complete and valid chain of trust can be built for the website's TLS certificate, from the end-entity certificate up to a publicly trusted root CA.

## Test Procedure

1. Establish an HTTPS connection to the web server and collect all certificates presented during the TLS handshake (end-entity certificate and any intermediate certificates).
2. Attempt to build a chain of trust by:
   - Verifying the end-entity certificate is signed by an intermediate CA certificate presented by the server (or directly by a root CA).
   - Verifying each intermediate certificate in the chain is signed by the next certificate up the chain.
   - Verifying the top-most certificate in the chain is signed by a publicly trusted root CA (present in the operating system or browser trust store).
3. The test passes if a complete and valid chain of trust can be built to a trusted root CA.

Note: All necessary intermediate certificates must be served by the web server itself; clients should not be required to fetch intermediates via AIA (Authority Information Access) URLs, though this is technically allowed.

## Scoring

| Result | Score |
| --- | --- |
| Valid chain of trust built to a publicly trusted root CA | Pass |
| Chain incomplete (missing intermediates), certificate not issued by trusted CA, or chain validation fails | Fail |
| HTTPS not available (W.1.1 failed) | Not Executed |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Web | Test 5.1 | Primary source |
| NCSC-NL TLS Guidelines 2025-05 | Section 1.2.2.1 | Certificate chain validation |
