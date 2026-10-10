# W.1.1: HTTPS Availability

## Summary

Checks whether the website is reachable via HTTPS with a valid TLS connection, confirming that encrypted access is possible.

## Test Procedure

1. Attempt an HTTPS connection (port 443) to the domain using the first available IPv4 address and, if available, the first available IPv6 address.
2. Complete the TLS handshake (an untrusted or self-signed certificate still allows the connection to be established for this test).
3. Send an HTTP GET request to the root path (**`/`**) and check that a response is received.
4. The test passes if a response is received over HTTPS on at least one address (IPv4 or IPv6).

Note: For performance reasons, only the first available IPv6 and IPv4 addresses are tested. HTTPS availability is a prerequisite for all subsequent TLS security tests (W.1.2–W.1.15).

## Scoring

| Result | Score |
| --- | --- |
| Website is reachable via HTTPS (TLS handshake completes and HTTP response received) | Pass |
| HTTPS not reachable on any tested address | Fail |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Web | Test 3.1 | Primary source |
| NCSC-NL TLS Guidelines 2025-05 | — | General TLS security baseline |
