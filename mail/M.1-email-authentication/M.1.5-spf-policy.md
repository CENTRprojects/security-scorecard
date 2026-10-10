# M.1.5: SPF Policy

## Summary

Checks whether the domain's SPF record contains a sufficiently strict policy (**`~all`** or **`-all`**) to prevent abuse by phishers and spammers.

## Test Procedure

1. Retrieve the SPF record as per M.1.4 (record must exist and be syntactically valid).
2. Follow all **`include:`** and **`redirect=`** mechanisms recursively to evaluate the full effective SPF record.
3. Count the total number of DNS-lookup mechanisms encountered (**`redirect`**, **`include`**, **`a`**, **`mx`**, **`ptr`**, **`exists`**). Verify the count does not exceed 10 (the RFC 7208 limit). **`all`**, **`ip4`**, **`ip6`**, and **`exp`** do not count.
4. Inspect the **`all`** mechanism qualifier at the end of the resolved SPF record:
   - **`-all`** (fail) — most strict.
   - **`~all`** (softfail) — sufficient.
   - **`?all`** (neutral) — insufficient.
   - **`+all`** (pass) — insufficient (allows all senders).
   - Absent **`all`** with no **`redirect`** — treated as **`?all`** by default.

Note: Macros in **`include:`** or **`redirect=`** values are not expanded, so their DNS lookups are not counted and their outcomes are not evaluated.

## Scoring

| Result | Score |
| --- | --- |
| Policy ends with **`-all`** or **`~all`** AND DNS lookup count does not exceed 10 | Pass |
| Policy ends with **`?all`**, **`+all`**, no qualifying **`all`** mechanism, DNS lookup count exceeds 10, no SPF record, or invalid syntax | Fail |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Mail | Test 3.5 | Primary source |
| RFC 7208 | — | SPF specification, including 10-lookup limit |
