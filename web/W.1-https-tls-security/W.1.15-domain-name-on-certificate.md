# W.1.15: Domain Name on Certificate

## Summary

Checks whether the domain name of the website matches a Subject Alternative Name (SAN) or Common Name on the presented TLS certificate.

## Test Procedure

1. Establish an HTTPS connection to the web server and retrieve the TLS certificate.
2. Extract the Subject Alternative Names (SAN) from the certificate's **`subjectAltName`** extension.
3. Check whether the domain being tested (e.g., **`example.nl`** or **`www.example.nl`**) matches one of the SANs, using standard wildcard matching rules (e.g., **`*.example.nl`** matches **`www.example.nl`**).
4. The test passes if the tested domain matches a SAN in the certificate.

Note: It could be useful to include more than one domain (e.g. the domain with and without www) as Subject Alternative Name on the certificate.

## Scoring

| Result | Score |
| --- | --- |
| Domain name matches a SAN in the certificate | Pass |
| Domain name does not match any SAN in the certificate | Fail |
| HTTPS not available (W.1.1 failed) | Not Executed |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Web | Test 5.4 | Primary source |
| RFC 5280 | — | X.509 certificate profile (SAN extension) |
