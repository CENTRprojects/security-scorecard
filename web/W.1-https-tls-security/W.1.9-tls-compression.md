# W.1.9: TLS Compression

## Summary

Checks whether the web server has TLS-level compression disabled, preventing CRIME-type attacks that exploit compressed encrypted traffic.

## Test Procedure

1. During the TLS handshake with the web server, advertise support for TLS compression methods in the client hello.
2. Check whether the server selects a compression method other than **`null`** (i.e., no compression).

### Compression classification (NCSC-NL TLS Guidelines 2025-05, Section 3.4.1, table 10):

| Compression | Classification |
| --- | --- |
| No compression (**`null`**) | Good |
| Application-level compression (HTTP compression) | Sufficient |
| TLS compression (TLS-layer compression method selected) | Insufficient |

3. The test passes if the server does not select any TLS compression method (selects **`null`** only).

Note: Application-level (HTTP) compression is a separate layer and is not detected or evaluated by this test.

## Scoring

| Result | Score |
| --- | --- |
| TLS compression not selected (null compression only) | Pass |
| TLS compression selected | Fail |
| HTTPS not available (W.1.1 failed) | Not Executed |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Web | Test 4.6 | Primary source |
| NCSC-NL TLS Guidelines 2025-05 | Section 3.4.1, Table 10 | Compression classification |
