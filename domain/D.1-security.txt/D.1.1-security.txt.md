# D.1.1: security.txt File

## Summary

Checks whether the domain publishes a syntactically valid **`security.txt`** file at **`/.well-known/security.txt`**, enabling security researchers to report vulnerabilities through a standardised contact channel.

## Test Procedure

1. Send an HTTPS GET request to **`https://<domain>/.well-known/security.txt`** using the first available IPv4 and IPv6 address of the web server.
2. If the response status code is not 200, retry at **`https://<domain>/security.txt`** (legacy path).
3. If any redirect is followed, record the final URL and the host it resolves to.
4. Evaluate the HTTP response:
   - Verify the response status is 200.
   - Verify the **`Content-Type`** header is present and its media type is **`text/plain`** with charset **`utf-8`**.
   - If the file was found at the legacy **`/security.txt`** path instead of **`/.well-known/security.txt`**, record a location error.
5. Read up to the first 100 kB of the response body.
6. Parse the file content using the **`security.txt`** specification (RFC 9116):
   - Check that all required fields are present (e.g., **`Contact`**, **`Expires`**).
   - Check that the **`Expires`** date is valid and has not passed.
   - If one or more **`Canonical`** fields are present, verify the URL used to retrieve the file is listed in a **`Canonical`** field.
   - Check for PGP signature (recorded as a recommendation if absent, not an error).
7. Collect all parser errors. The file passes if and only if no errors are found (neither retrieval errors nor parse errors).

Note: For performance reasons, only the first available IPv6 and IPv4 address are tested. Cross-domain redirects are permitted; in large domain portfolios it is common to redirect to a central **`security.txt`** file.

## Scoring

| Result | Score |
| --- | --- |
| File found at **`/.well-known/security.txt`**, **`Content-Type: text/plain; charset=utf-8`**, and no parse errors | Pass |
| File not found (404 or other non-200 status), missing **`Content-Type`**, wrong media type, wrong charset, wrong location, or any RFC 9116 parse error | Fail |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Web | Test 6.5 | Primary source |
| RFC 9116 | — | Defines the **`security.txt`** format and required fields |
