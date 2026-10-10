# W.1.3: HSTS (HTTP Strict Transport Security)

## Summary

Checks whether the web server provides an HSTS header with a sufficiently long **`max-age`** directive, instructing browsers to always use HTTPS when revisiting the domain.

## Test Procedure

1. Send an HTTPS request to the domain (before following any redirect).
2. Inspect the HTTP response headers for a **`Strict-Transport-Security`** header.
3. Verify the header is present in the response from the first contacted host (before any redirect), so the browser can record the HSTS policy immediately.
4. Verify the **`max-age`** directive is present and its value is at least 31,536,000 seconds (1 year).
5. The **`includeSubDomains`** and **`preload`** directives are optional and are not required for this test to pass.

Note: HSTS policies are remembered per subdomain. Failing to include an HSTS header on each domain in a redirect chain may leave users vulnerable to MITM attacks before the final HTTPS destination is reached. The test does not check whether the domain is included in browser HSTS preload lists.

## Scoring

| Result | Score |
| --- | --- |
| **`Strict-Transport-Security`** header present with **`max-age`** ≥ 31,536,000 seconds | Pass |
| Header absent, **`max-age`** missing, or **`max-age`** \< 31,536,000 seconds | Fail |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Web | Test 3.4 | Primary source |
| RFC 6797 | — | HTTP Strict Transport Security specification |
