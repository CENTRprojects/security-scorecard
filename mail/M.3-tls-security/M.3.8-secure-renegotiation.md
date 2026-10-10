# M.3.8: Secure Renegotiation

## Summary

Checks whether each receiving mail server (MX host) has insecure TLS renegotiation disabled, ensuring only the secure renegotiation mechanism (RFC 5746) or TLS 1.3 (which eliminates legacy renegotiation) is used.

## Test Procedure

After STARTTLS negotiation with each MX host (per M.3.1):

1. During or after the TLS handshake, attempt to initiate renegotiation using the legacy (insecure) renegotiation mechanism without the **`renegotiation_info`** extension.
2. Check whether the server accepts the insecure renegotiation request.

### Classification (NCSC-NL TLS Guidelines 2025-05, Section 3.4.2 , table 11):

| Insecure renegotiation | Classification |
| --- | --- |
| Off (or N/A for TLS 1.3) | Good |
| On | Insufficient |

3. The test passes if insecure renegotiation is rejected (or not applicable because only TLS 1.3 is used).

## Scoring

| Result | Score |
| --- | --- |
| Insecure renegotiation is disabled (or server only supports TLS 1.3) | Pass |
| Insecure renegotiation is accepted | Fail |
| STARTTLS not available (M.3.1 failed or N/A) | Not Executed |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Mail | Test 4.8 | Primary source |
| NCSC-NL TLS Guidelines 2025-05 | Section 3.4.2, Table 11 | Renegotiation classification |
| RFC 5746 | — | TLS Renegotiation Indication Extension |
