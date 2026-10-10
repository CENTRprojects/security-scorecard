# M.2.2: TLS-RPT

## Summary

Checks whether the domain publishes a valid SMTP TLS Reporting (TLS-RPT) DNS record, enabling receiving mail servers to send TLS failure reports to the domain owner.

## Test Procedure

1. Query the DNS TXT record at **`_smtp._tls.<domain>`**.
2. Verify the record starts with **`v=TLSRPTv1`**.
3. Verify the record contains at least one **`rua=`** field with a valid reporting URI. Accepted URI schemes:
   - **`mailto:<email-address>`** — report delivered by email.
   - **`https://<url>`** — report delivered via HTTPS POST.
4. Verify the syntax of each URI is valid.

## Scoring

| Result | Score |
| --- | --- |
| Valid TLS-RPT DNS record present with at least one valid **`rua=`** URI | Pass |
| No TLS-RPT record, invalid syntax, or no valid **`rua=`** URI | Fail |

## References

| Source | ID | Notes |
| --- | --- | --- |
| RFC 8460 | — | SMTP TLS Reporting specification |
