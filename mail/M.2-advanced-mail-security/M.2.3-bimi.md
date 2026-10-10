# M.2.3: BIMI

## Summary

Checks whether the domain publishes a valid BIMI DNS record, optionally accompanied by a Verified Mark Certificate (VMC), allowing email clients to display a verified brand logo alongside authenticated messages.

## Test Procedure

1. Query the DNS TXT record at **`default._bimi.<domain>`**.
2. Verify the record starts with **`v=BIMI1`**.
3. Verify the record contains an **`l=`** field with an HTTPS URL pointing to an SVG logo file.
4. Optionally check for an **`a=`** field with an HTTPS URL pointing to a Verified Mark Certificate (VMC) issued by an accredited certificate authority.
5. Determine the result:
   - BIMI record present with valid **`l=`** URL and valid **`a=`** VMC URL — full verified brand identity.
   - BIMI record present with valid **`l=`** URL but no **`a=`** VMC — logo present, unverified.
   - No BIMI record or invalid syntax — no BIMI.

Note: Without a VMC, some email clients may not display the logo even if the BIMI record is present. BIMI requires DMARC **`p=quarantine`** or **`p=reject`** to be effective.

## Scoring

| Result | Score |
| --- | --- |
| Valid BIMI record present with both **`l=`** logo URL and **`a=`** VMC URL | Pass |
| No BIMI record, invalid record syntax, or missing **`l=`** URL | Fail |

## References

| Source | ID | Notes |
| --- | --- | --- |
| BIMI Specification | — | Brand Indicators for Message Identification |
