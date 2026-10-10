# W.2.2: Content-Security-Policy (CSP)

## Summary

Checks whether the web server provides a **`Content-Security-Policy`** HTTP header with a secure configuration that mitigates content injection attacks including cross-site scripting (XSS).

## Test Procedure

1. Send an HTTPS GET request to the domain using the first available IPv4 and IPv6 address.
2. Inspect the HTTP response headers for a **`Content-Security-Policy`** header.
3. Verify the header is present.
4. Evaluate the CSP configuration against the following rules:

### Required directives and values:

- **`default-src`** must be defined with a value of **`'none'`**, or **`'self'`** and/or URLs of the domain itself (including subdomains/superdomain). The value **`'report-sample'`** may also be present.
- **`base-uri`** must be defined with a value of **`'none'`**, or **`'self'`** and/or URLs of the domain itself.
- **`frame-src`** must be used (directly or via fallback to **`child-src`** then **`default-src`**) with a value of **`'none'`**, or **`'self'`** and/or specific URLs.
- **`frame-ancestors`** must be defined with a value of **`'none'`**, or **`'self'`** and/or specific URLs.
- **`form-action`** must be defined with a value of **`'none'`**, or **`'self'`** and/or specific URLs.

### Prohibited values (in any directive):

- **`unsafe-eval`**, **`unsafe-inline`**, **`unsafe-hashes`** — enable XSS attacks.
- **`data:`** scheme in **`default-src`**, **`script-src`**, or **`object-src`** — enables XSS.
- **`http://`** scheme or scheme-less domains — allows insecure loading.
- Wildcard (**`*`**) for the full host part of a URL in any directive (including bare **`https:`**).
- **`127.0.0.1`** in any directive.

1. The test passes only if the header is present and all required directives are correctly defined with no prohibited values.

Note: For performance reasons, only the first available IPv6 and IPv4 addresses are tested. Requirement level is Recommended. The test does not exhaustively verify CSP effectiveness.

Note: For execution of this test http redirects shall be followed and the final site evaluated

## Scoring

| Result | Score |
| --- | --- |
| CSP header present with all required directives and no prohibited values | Pass |
| CSP header absent, required directive missing or incorrect, or prohibited value present | Fail |
| HTTPS not available (W.1.1 failed) | Not Executed |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Web | Test 6.3 | Primary source |
| W3C CSP Level 3 | — | Content Security Policy specification |
