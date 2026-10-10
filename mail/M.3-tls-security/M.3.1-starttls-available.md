# M.3.1: STARTTLS Available

## Summary

Checks whether each receiving mail server (MX host) supports STARTTLS, enabling encrypted SMTP transport for inbound email.

## Test Procedure

1. Resolve the MX records for the domain. If no MX records exist (no MX or Null MX per RFC 7505), all STARTTLS and TLS subtests are not applicable.
2. For up to 10 MX hosts (tested over IPv4 or IPv6), connect to port 25 (SMTP).
3. Send **`EHLO`** and inspect the response for **`STARTTLS`** in the list of advertised capabilities.
4. Attempt to initiate STARTTLS by sending the **`STARTTLS`** command and completing the TLS handshake.
5. The test passes if STARTTLS is successfully negotiated on all reachable MX hosts.

Note: If the domain uses a Null MX record (RFC 7505) or has no MX records and no A/AAAA records, this test and all dependent TLS subtests (M.3.2–M.3.12) are not applicable. The email test does not fall back to A/AAAA records in the absence of an MX record.

## Scoring

| Result | Score |
| --- | --- |
| STARTTLS successfully negotiated on all tested MX hosts | Pass |
| Any MX host does not advertise or fails to negotiate STARTTLS | Fail |
| Null MX or no MX configured | Not Applicable |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Mail | Test 4.1 | Primary source |
| RFC 3207 | — | SMTP STARTTLS extension |
| RFC 7505 | — | Null MX record |
