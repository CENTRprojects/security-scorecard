# M.2.1: MTA-STS

## Summary

Checks whether the domain publishes an MTA-STS DNS record and a valid policy file, enforcing TLS for inbound SMTP connections and protecting against downgrade attacks.

## Test Procedure

1. Query the DNS TXT record at **`_mta-sts.<domain>`**.
2. Verify the record starts with **`v=STSv1`** and contains an **`id=`** field.
3. Fetch the MTA-STS policy file via HTTPS at **`https://mta-sts.<domain>/.well-known/mta-sts.txt`**.
4. Verify the HTTPS fetch succeeds (HTTP 200) with a valid TLS certificate.
5. Parse the policy file and check:
   - **`version: STSv1`** is present.
   - **`mode:`** field is present with value **`enforce`**, **`testing`**, or **`none`**.
   - At least one **`mx:`** field is present listing allowed MX hostnames (wildcards permitted).
   - **`max_age:`** field is present with a positive integer value.
6. Determine the effective mode:
   - **`mode: enforce`** — full TLS enforcement.
   - **`mode: testing`** — monitoring only; no enforcement.
   - **`mode: none`** — policy disabled.

## Scoring

| Result | Score |
| --- | --- |
| Valid DNS record and policy file with **`mode: enforce`** | Pass |
| DNS record or policy file absent, invalid, unreachable, or **`mode: testing`** / **`mode: none`** | Fail |

## References

| Source | ID | Notes |
| --- | --- | --- |
| RFC 8461 | — | MTA-STS specification |
