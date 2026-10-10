# W.2.1: X-Content-Type-Options Header

## Summary

Checks whether the web server provides an **`X-Content-Type-Options`** HTTP header with the value **`nosniff`**, preventing browsers from performing MIME type sniffing that could be exploited in MIME confusion attacks.

## Test Procedure

1. Send an HTTPS GET request to the domain using the first available IPv4 and IPv6 address.
2. Inspect the HTTP response headers for an **`X-Content-Type-Options`** header.
3. Verify the header is present.
4. Verify the header value is exactly **`nosniff`** (the only valid value for this header).

Note: For performance reasons, only the first available IPv6 and IPv4 addresses are tested. Requirement level is Recommended.

Note: For execution of this test http redirects shall be followed and the final site evaluated

## Scoring

| Result | Score |
| --- | --- |
| **`X-Content-Type-Options: nosniff`** header present | Pass |
| Header absent, or present with a value other than **`nosniff`** | Fail |
| HTTPS not available (W.1.1 failed) | Not Executed |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Web | Test 6.2 | Primary source |
