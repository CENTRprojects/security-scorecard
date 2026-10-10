# M.3.4: Cipher Order

## Summary

Checks whether each receiving mail server (MX host) enforces its own cipher preference and offers cipher suites in the prescribed security order (Good before Sufficient before Phase out).

## Test Procedure

After STARTTLS negotiation with each MX host (per M.3.1):

### Part I — Server-enforced cipher preference:

1. Connect with two different client hellos advertising the same cipher suites in opposite order.
2. If the server selects the same cipher suite regardless of client ordering, it enforces its own preference. If it follows the client's order, it does not enforce preference.

### Part II — Prescribed ordering:

1. Offer all supported cipher suites in a single client hello.
2. Check that the server selects a Good cipher if any Good cipher is available, then Sufficient, then Phase out.
3. If the server selects a lower-ranked cipher when a higher-ranked cipher was offered, it is out of prescribed order.

Not Applicable: If the server supports only Good cipher suites, cipher ordering has no security benefit and this test is not applicable.

## Scoring

| Result | Score |
| --- | --- |
| Server enforces its own cipher preference AND offers ciphers in prescribed order (Good > Sufficient > Phase out) | Pass |
| Server does not enforce preference, or serves ciphers out of prescribed order | Fail |
| Server supports only Good ciphers | Not Applicable |
| STARTTLS not available (M.3.1 failed or N/A) | Not Executed |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Mail | Test 4.4 | Primary source |
| NCSC-NL TLS Guidelines v2.1 | B2-5 | Cipher categorisation |
