# M.3.12: DANE-Validity

## Summary

Checks whether the TLSA records published by each receiving mail server's (MX host's) domain correctly match the certificate presented during STARTTLS, confirming that DANE authentication is functionally valid.

## Test Procedure

After STARTTLS negotiation with each MX host (per M.3.1) and with TLSA records confirmed present (per M.3.11):

1. Retrieve the TLSA records from DNS (DNSSEC-authenticated) at **`_25._tcp.<mx-hostname>`**.
2. Retrieve the certificate (or certificate chain) presented by the MX host during the TLS handshake.
3. For each TLSA record, perform the matching procedure as defined in RFC 6698:
   - Certificate Usage: DANE-TA (2) matches against the trust anchor; DANE-EE (3) matches against the end-entity certificate directly.
   - Selector: Full certificate (0) or SubjectPublicKeyInfo (1).
   - Matching type: Exact match (0), SHA-256 hash (1), SHA-512 hash (2).
4. Compute the expected fingerprint of the certificate or public key (as specified by the selector and matching type) and compare against the TLSA record data.
5. The test passes if at least one TLSA record successfully matches the presented certificate or trust anchor.

Note: DANE allows sending mail servers to authenticate the receiving server's certificate through DNS, independent of the CA system. A DANE-validated sending mail server that encounters a valid TLSA record will only connect via STARTTLS, preventing downgrade attacks.

## Scoring

| Result | Score |
| --- | --- |
| At least one TLSA record matches the certificate presented during STARTTLS | Pass |
| No TLSA record matches the certificate, or TLSA records are present but the certificate is invalid or mismatched | Fail |
| TLSA records not present (M.3.11 failed or N/A) | Not Executed |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Mail | Test 6.2 | Primary source |
| RFC 6698 | — | DANE specification and matching procedure |
| RFC 7671 | — | DANE implementation guidance |
