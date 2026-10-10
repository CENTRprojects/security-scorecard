# M.3.7: TLS Compression

## Summary

Checks whether each receiving mail server (MX host) has TLS-level compression disabled, preventing CRIME-type attacks that exploit compressed encrypted traffic.

## Test Procedure

After STARTTLS negotiation with each MX host (per M.3.1):

1. During the TLS handshake, advertise support for TLS compression methods in the client hello.
2. Check whether the server selects a compression method other than **`null`** (i.e., no compression).

### Compression classification (NCSC-NL TLS Guidelines 2025-05, table 10):

| Compression | Classification |
| --- | --- |
| No compression (**`null`**) | Good |
| Application-level compression (e.g., SMTP-level) | Sufficient |
| TLS compression (TLS-layer compression method selected) | Insufficient |

3. The test passes if the server does not select any TLS compression method (selects **`null`** only).

## Scoring

| Result | Score |
| --- | --- |
| TLS compression not selected (null compression only) | Pass |
| TLS compression selected | Fail |
| STARTTLS not available (M.3.1 failed or N/A) | Not Executed |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Mail | Test 4.7 | Primary source |
| NCSC-NL TLS Guidelines 2025-05 | Section 3.4.1, Table 10 | Options for TLS compression and their security level. |
