# W.3.1: CAA Records

## Summary

Checks whether the domain's DNS zone contains one or more syntactically valid CAA records with at least one **`issue`** tag, authorising specific certificate authorities to issue TLS certificates for the domain.

## Test Procedure

1. Query DNS for CAA records at **`<domain>`**. If no CAA records are found, walk up the DNS hierarchy (e.g., from **`sub.example.nl`** to **`example.nl`**) until CAA records are found or the root is reached.
2. Verify that at least one CAA record is present.
3. Verify that all found CAA records have correct syntax (valid **`flags`**, **`tag`**, and **`value`** fields per RFC 8659).
4. Verify that at least one CAA record has the **`issue`** tag (authorising a named CA to issue certificates, or using **`;`** to deny all issuance).
5. The test passes if one or more syntactically valid CAA records are found with at least one **`issue`** tag.

It is not checked whether the CA currently used for the domain's TLS certificate is listed in the CAA records.

### Recommended additions (not required for pass):

- **`issuewild`**, **`issuemail`**, and **`issuevmc`** with an empty **`;`** if wildcard, S/MIME, or BIMI certificates are not used.
- **`iodef`** with an HTTPS URL for reporting CAA violations.
- ACME parameters **`validationmethods`** and **`accounturi`** to further restrict issuance.

Note: CAA records do not enforce DNSSEC usage, but DNSSEC is strongly recommended to prevent CAA record suppression or spoofing. URLs in **`iodef`** must use the **`https://`** scheme.

## Scoring

| Result | Score |
| --- | --- |
| One or more CAA records present with valid syntax and at least one **`issue`** tag | Pass |
| No CAA records found, invalid syntax in any record, or no **`issue`** tag present | Fail |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Mail / Web | — | Description derived from Internet.nl implementation |
| RFC 8659 | — | DNS Certification Authority Authorization (CAA) Resource Record |
