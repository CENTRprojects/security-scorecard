# M.3.11: DANE Existence

## Summary

Checks whether the DNS zone for each receiving mail server (MX host) publishes a TLSA record to support DANE, enabling cryptographic authentication of the mail server certificate via DNS.

## Test Procedure

For each MX host resolved for the domain:

1. Verify that DNSSEC is enabled and valid for the MX host's domain (prerequisite: M.4.1 and M.4.2 must pass for the mail server domain). If DNSSEC is missing, this test fails.
2. Query the TLSA record at **`_25._tcp.<mx-hostname>`** using a validating resolver with DNSSEC enabled.
3. Check that the query returns a valid DNSSEC-authenticated response (**`AD`** flag set) with one or more TLSA records.
4. Verify that the TLSA records do not use PKIX-TA (Certificate Usage 0) or PKIX-EE (Certificate Usage 1) types, as these are not recommended for receiving mail servers.
5. Verify that there is a valid DNSSEC proof of "Denial of Existence" (authenticated NXDOMAIN or NSEC/NSEC3 denial) for any TLSA name that has no records — absence of TLSA records must itself be provable via DNSSEC.

Note: If a signed TLSA record exists but the DNS simultaneously returns an insecure NXDOMAIN for the same name (due to faulty signer software), the test fails. This failure scenario can cause DANE-validating sending mail servers to refuse delivery.

## Scoring

| Result | Score |
| --- | --- |
| DNSSEC valid on MX domain AND at least one DANE-EE (type 3) or DANE-TA (type 2) TLSA record found with DNSSEC authentication | Pass |
| DNSSEC missing on MX domain, no TLSA record, only PKIX-type TLSA records, or DNSSEC proof of denial absent | Fail |
| Null MX or no MX configured | Not Applicable |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Mail | Test 6.1 | Primary source |
| NCSC-NL TLS Guidelines 2025-05 | Chapter 2 | DANE |
| RFC 6698 | — | DANE specification |
| RFC 7671 | — | DANE implementation guidance |
