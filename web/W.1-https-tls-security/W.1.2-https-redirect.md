# W.1.2: HTTPS Redirect

## Summary

Checks whether the web server automatically redirects HTTP connections to HTTPS on the same domain, ensuring visitors are always upgraded to a secure connection.

## Test Procedure

1. Send an HTTP request (port 80) to the domain (both apex and www subdomain if applicable).
2. Check whether the server responds with a 3xx redirect status code (e.g., 301, 302).
3. Verify that the redirect target URL uses the HTTPS scheme (**`https://`**) and the same domain (not a different domain).
4. Example of a correct redirect sequence:
   - **`http://example.nl`** → **`https://www.example.nl`** → (optional further redirect to **`https://example.nl`**)
   - **`http://www.example.nl`** → **`https://www.example.nl`**
5. The test passes if the HTTP request is redirected to the HTTPS version of the same domain before any cross-domain redirect.

Note: An alternative pass condition is that the server only listens on HTTPS (port 80 not reachable), effectively supporting only HTTPS. This test only checks the HTTP-to-HTTPS redirect on the tested domain; redirects to other domains are not evaluated here.

## Scoring

| Result | Score |
| --- | --- |
| HTTP request redirected to HTTPS on the same domain (or HTTP port not accessible) | Pass |
| HTTP request not redirected, or redirected to another domain before self-redirect to HTTPS | Fail |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Web | Test 3.2 | Primary source |
