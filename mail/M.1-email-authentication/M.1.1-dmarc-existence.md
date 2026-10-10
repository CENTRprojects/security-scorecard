# M.1.1: DMARC Existence

## Summary

Checks whether the domain publishes a syntactically valid DMARC record at **`_dmarc.<domain>`**, enabling receiving mail servers to apply a policy to unauthenticated messages using the domain as sender.

## Test Procedure

1. Query the DNS TXT record at **`_dmarc.<domain>`**.
2. Check that exactly one TXT record is returned that starts with **`v=DMARC1`**. If more than one such record is found, the test fails (invalid DMARC configuration).
3. Verify the record has valid syntax: it must be a semicolon-separated list of **`key=value`** pairs, containing at least the **`v=DMARC1`** and **`p=`** tags (each appearing exactly once).
4. Verify the **`p=`** value is one of: **`none`**, **`quarantine`**, or **`reject`**.

Note: DMARC requires the SPF domain (envelope sender in **`MAIL FROM`**) and the DKIM domain (**`d=`**) to align with the mail body **`From:`** domain. The policy strength is evaluated separately in M.1.2.

## Scoring

| Result | Score |
| --- | --- |
| Exactly one valid DMARC record present with correct syntax and a recognised **`p=`** value | Pass |
| No DMARC record, more than one DMARC record, invalid syntax, or missing/invalid **`p=`** value | Fail |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Mail | Test 3.1 | Primary source |
| RFC 7489 | — | DMARC specification |
| RFC 9091 | — | Experimental **`np`** tag permitted |
