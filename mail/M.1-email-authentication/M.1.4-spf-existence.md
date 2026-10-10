# M.1.4: SPF Existence

## Summary

Checks whether the domain publishes exactly one syntactically valid SPF record, enabling receiving mail servers to authenticate the sending IP address for messages using this domain as sender.

## Test Procedure

1. Query the DNS TXT records at **`<domain>`**.
2. Identify all TXT records that start with **`v=spf1`**.
3. Check that exactly one such record is present. If more than one is found, the test fails (invalid SPF configuration).
4. Verify the SPF record has valid syntax (correctly formed mechanism and modifier list).

Note: The SPF policy strictness is evaluated separately in M.1.5.

## Scoring

| Result | Score |
| --- | --- |
| Exactly one TXT record starting with **`v=spf1`** with valid syntax | Pass |
| No SPF record, more than one SPF record, or invalid syntax | Fail |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Mail | Test 3.4 | Primary source |
| RFC 7208 | — | SPF specification |
