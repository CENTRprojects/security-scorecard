# M.4.2: DNSSEC Validity (Mail Server Domain)

## Summary

Checks whether the DNSSEC signature for each receiving mail server's (MX host's) domain is cryptographically valid, making the domain resolution "secure".

## Test Procedure

1. Retrieve the MX records for the domain. If no MX records are present, stop — the test does not fall back to A/AAAA records.
2. For each MX hostname, query the SOA record for the MX host's domain using a validating resolver.
3. Check whether the SOA record is signed with a valid DNSSEC signature (i.e., the domain is resolved as "secure").
4. If the MX host's domain redirects to another domain via CNAME, also check whether the signature of the CNAME target domain is valid (conformant with the DNSSEC standard). If the signature of the CNAME target is not valid, the test fails.

Note: Only the first responding name server is tested. Inconsistent configurations across name servers may produce varying results between test runs.

## Scoring

| Result | Score |
| --- | --- |
| SOA record is signed with a valid DNSSEC signature (and CNAME target, if applicable) | Pass |
| Signature is invalid ("bogus") | Fail |
| CNAME target signature is invalid | Fail |
| No MX records configured | Not Applicable |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Mail | Test 2.4 | Primary source |
