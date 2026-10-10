# W.2.3: Referrer-Policy Header

## Summary

Checks whether the web server provides a **`Referrer-Policy`** HTTP header with a policy value that adequately protects referrer data from being sent to third parties or over insecure connections.

## Test Procedure

1. Send an HTTPS GET request to the domain using the first available IPv4 and IPv6 address.
2. Inspect the HTTP response headers for a **`Referrer-Policy`** header.
3. Verify the header is present.
4. Identify the policy value and classify it:

### Good (no sensitive referrer data sent to third parties):

- **`no-referrer`**
- **`same-origin`**

### Warning (basic referrer data sent to third parties only over secure connections — acceptable if necessary):

- **`strict-origin`**
- **`strict-origin-when-cross-origin`** (browser default)

### Bad (referrer data sent to third parties, possibly over insecure connections — must not be used):

- **`no-referrer-when-downgrade`**
- **`origin-when-cross-origin`**
- **`origin`**
- **`unsafe-url`**

5. The test passes if the policy value is Good or Warning. Bad policy values fail the test.

Note: For performance reasons, only the first available IPv6 and IPv4 addresses are tested. Requirement level is Recommended. **`strict-origin-when-cross-origin`** is the browser default and is classified as Warning — it may be appropriate where necessary and permitted, but sensitive referrer data is sent to third parties over HTTPS.

## Scoring

| Result | Score |
| --- | --- |
| **`Referrer-Policy`** header present with a Good or Warning value (**`no-referrer`**, **`same-origin`**, **`strict-origin`**, or **`strict-origin-when-cross-origin`**) | Pass |
| Header absent, or present with a Bad policy value | Fail |
| HTTPS not available (W.1.1 failed) | Not Executed |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Web | Test 6.4 | Primary source |
| W3C Referrer Policy | — | Referrer Policy specification |
