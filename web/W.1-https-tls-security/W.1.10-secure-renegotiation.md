# W.1.10: Secure Renegotiation

## Summary

Checks whether the web server has insecure TLS renegotiation disabled, ensuring only the secure renegotiation mechanism (RFC 5746) or TLS 1.3 (which eliminates legacy renegotiation) is used.

## Test Procedure

1. Connect to the web server and complete an initial TLS handshake.
2. Attempt to initiate renegotiation using the legacy (insecure) renegotiation mechanism without the **`renegotiation_info`** extension.
3. Check whether the server accepts the insecure renegotiation request.

### Classification (NCSC-NL TLS Guidelines 2025-05, Section 3.4.2, table 11):

| Insecure renegotiation | Classification |
| --- | --- |
| Off (or N/A for TLS 1.3 only servers) | Good |
| On | Insufficient |

| TLS version | Client-initiated renegotiation option | Classification |
| --- | --- | --- |
| 1.3 | n/a | Good |
| 1.2 | No renegotiation | Good |
|  | Limited secure renegotiation | Sufficient |
|  | Unlimited secure renegotiation | Phase out |
|  | Insecure renegotiation | Insufficient |

4. The test passes if insecure renegotiation is rejected (or not applicable because only TLS 1.3 is used).

## Scoring

| Result | Score |
| --- | --- |
| Insecure renegotiation is disabled (or server only supports TLS 1.3) | Pass |
| Insecure renegotiation is accepted | Fail |
| HTTPS not available (W.1.1 failed) | Not Executed |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Web | Test 4.7 | Primary source |
| NCSC-NL TLS Guidelines 2025-05 | Section 3.4.2, Table 11 | Renegotiation classification |
| RFC 5746 | — | TLS Renegotiation Indication Extension |
