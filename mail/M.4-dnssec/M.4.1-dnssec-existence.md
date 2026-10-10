# M.4.1: DNSSEC Existence (Mail Server Domain)

## Summary

Checks whether the DNS zone of each receiving mail server (MX host) is DNSSEC-signed, confirming that the MX host's domain has a secure delegation.

## Test Procedure

1. Retrieve the MX records for the domain. If no MX records are present, stop — the test does not fall back to A/AAAA records.
2. For each MX hostname, query the SOA record for the MX host's domain to check whether it is DNSSEC signed.
3. If the MX host's domain redirects to another domain via CNAME, also check whether the CNAME target domain is signed (conformant with the DNSSEC standard). If the CNAME target is not signed, the test fails.
4. If the SOA record (and any CNAME target) is DNSSEC signed for all MX hosts, the test passes.

Note: The validity of the signature is not part of this test; that is evaluated in M.4.2.

## Scoring

| Result | Score |
| --- | --- |
| SOA record is DNSSEC signed (and CNAME target is signed, if applicable) | Pass |
| SOA record is not DNSSEC signed, or CNAME target is not signed | Fail |
| No MX records configured | Not Applicable |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Mail | Test 2.3 | Primary source |
