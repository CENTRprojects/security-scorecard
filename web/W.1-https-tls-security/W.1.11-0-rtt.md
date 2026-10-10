# W.1.11: 0-RTT (Zero Round Trip Time)

## Summary

Checks whether the web server has the TLS 1.3 Zero Round Trip Time Resumption (0-RTT) feature disabled, preventing potential replay attacks on early data.

## Test Procedure

1. Fetch the index page of the website using a TLS 1.3 connection.
2. Check the server's response for the **`max_early_data_size`** extension in the session ticket. If the value is greater than zero, the server accepts 0-RTT early data.
3. If early data is indicated as accepted, establish a second TLS connection that re-uses the session details from the first connection and sends the HTTP request as early data (0-RTT).
4. Check whether the server accepts and processes the early data.

Not Applicable: If the web server does not support TLS 1.3, this test is not applicable.

### Classification (NCSC-NL TLS Guidelines 2025-05, Section 3.4.4, table 13):

| 0-RTT | Classification |
| --- | --- |
| Off (or N/A — TLS 1.3 not supported) | Good |
| On | Insufficient |

## Scoring

| Result | Score |
| --- | --- |
| 0-RTT is disabled (server does not accept early data) | Pass |
| 0-RTT is enabled (server accepts early data) | Fail |
| Server does not support TLS 1.3 | Not Applicable |
| HTTPS not available (W.1.1 failed) | Not Executed |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Web | Test 4.9 | Primary source |
| NCSC-NL TLS Guidelines 2025-05 | Section 3.4.4 | 0-RTT classification |
| RFC 8446 | — | TLS 1.3, including 0-RTT specification |
