# M.1.2: DMARC Policy

## Summary

Checks whether the domain's DMARC policy is sufficiently strict (**`p=quarantine`** or **`p=reject`**) to protect against phishing and spoofing abuse.

## Test Procedure

1. Retrieve the DMARC record as per M.1.1 (record must exist and be syntactically valid).
2. Inspect the **`p=`** tag value:
   - **`p=reject`** — most strict; unauthenticated mail is rejected.
   - **`p=quarantine`** — strict; unauthenticated mail is quarantined.
   - **`p=none`** — monitoring only; no enforcement action.
3. If **`rua=`** or **`ruf=`** fields are present, verify the listed mail addresses are syntactically valid. If any address belongs to an external domain, check that the external domain publishes a DMARC authorisation record containing at least **`v=DMARC1;`** at **`<domain>._report._dmarc.<external-domain>`**.
4. Verify the total number of DNS lookups performed does not indicate misconfiguration.

Note: The experimental **`np`** tag (RFC 9091) is permitted and does not affect the result.

## Scoring

| Result | Score |
| --- | --- |
| **`p=quarantine`** or **`p=reject`** | Pass |
| **`p=none`**, no DMARC record, or invalid DMARC record | Fail |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Mail | Test 3.2 | Primary source |
| RFC 7489 | — | DMARC specification |
| RFC 9091 | — | Experimental **`np`** tag |
