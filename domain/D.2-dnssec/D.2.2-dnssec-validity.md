# D.2.2: DNSSEC Validity

## Summary

Checks whether the domain's DNSSEC signature is cryptographically valid, making the domain resolution "secure" from a DNSSEC perspective.

## Test Procedure

1. Query the SOA record for the domain using a validating resolver.
2. Check whether the SOA record is signed with a valid DNSSEC signature (i.e., the domain is resolved as "secure").
3. If the domain redirects to another domain via CNAME, also check whether the signature of the CNAME target domain is valid (conformant with the DNSSEC standard). If the signature of the CNAME target is not valid, the test fails.

Note: Only the first responding name server is tested. Inconsistent configurations across name servers may produce varying results between test runs.

## Scoring

| Result | Score |
| --- | --- |
| SOA record is signed with a valid DNSSEC signature | Pass |
| Signature is invalid ("bogus") | Fail |
| CNAME target signature is invalid | Fail |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Web | Test 2.2 | Primary source |
