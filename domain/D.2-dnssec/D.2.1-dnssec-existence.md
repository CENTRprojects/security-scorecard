# D.2.1: DNSSEC Existence

## Summary

Checks whether the domain's SOA record is covered by a DNSSEC signature, confirming that the zone has been signed and delegated securely.

## Test Procedure

1. Query the SOA record for the domain to check whether it is DNSSEC signed.
2. If the domain redirects to another domain via CNAME, also check whether the CNAME target domain is signed (conformant with the DNSSEC standard). If the CNAME target is not signed, the test fails.
3. If the SOA record (and any CNAME target) is DNSSEC signed, the test passes.

Note: The validity of the signature is not part of this test; that is evaluated in D.2.2.

## Scoring

| Result | Score |
| --- | --- |
| SOA record is DNSSEC signed (and CNAME target is signed, if applicable) | Pass |
| SOA record is not DNSSEC signed, or CNAME target is not signed | Fail |
| Test cannot be completed (e.g. resolver error) | Not Executed |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Web | Test 2.1 | Primary source |
