# M.1.3: DKIM Existence

## Summary

Checks whether the domain supports DKIM by verifying that the **`_domainkey.<domain>`** DNS node exists, allowing receiving servers to validate email signatures from this domain.

## Test Procedure

1. Query DNS for any record at **`_domainkey.<domain>`**.
2. Check that the name server returns **`NOERROR`** (not **`NXDOMAIN`**) for this query. A **`NOERROR`** response — even with an empty answer section (empty non-terminal) — confirms that the domain has DKIM infrastructure.
3. A **`NXDOMAIN`** response indicates no DKIM support.

Note: Because the DKIM selector is embedded in outbound email headers (not discoverable via DNS alone), it is not possible to retrieve and validate the actual DKIM public key without a selector. This test uses strict alignment (the tested domain must be identical to the DKIM **`d=`** domain and the SPF **`MAIL FROM`** domain), conformant with DMARC requirements.

Note: Some name servers that are not conformant with RFC 2308 incorrectly respond with **`NXDOMAIN`** when **`_domainkey.<domain>`** is an empty non-terminal. This produces a false negative.

## Scoring

| Result | Score |
| --- | --- |
| DNS query for **`_domainkey.<domain>`** returns **`NOERROR`** | Pass |
| DNS query returns **`NXDOMAIN`** | Fail |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Mail | Test 3.3 | Primary source |
| RFC 6376 | — | DKIM specification |
| RFC 2308 | — | DNS negative caching (correct NOERROR for empty non-terminals) |
