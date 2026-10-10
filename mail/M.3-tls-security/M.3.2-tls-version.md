# M.3.2: TLS Version

## Summary

Checks whether each receiving mail server (MX host) supports only secure TLS versions, rejecting deprecated SSL/TLS versions that expose connections to known attacks.

## Test Procedure

After STARTTLS negotiation with each MX host (per M.3.1):

1. Probe the MX host for support of each TLS/SSL version by attempting handshakes with version-specific client hellos:
   - TLS 1.3
   - TLS 1.2
   - TLS 1.1
   - TLS 1.0
   - SSL 3.0, 2.0, 1.0
2. Record which versions the server accepts.
3. Classify each supported version:

### Version classification (NCSC-NL TLS Guidelines 2025-05, Section 3.3.1, table 1):

| Version | Classification |
| --- | --- |
| TLS 1.3 | Good |
| TLS 1.2 | Sufficient |
| TLS 1.1, TLS 1.0 | Insufficient |
| SSL 3.0, SSL 2.0, SSL 1.0 | Insufficient |

4. The test passes if no Phase out or Insufficient versions are accepted.

Note: Many mail servers still support older TLS versions for interoperability. If both the sending and receiving server support no common version, mail transport falls back to unencrypted. An informed decision based on log data is recommended before disabling Phase out versions.

## Scoring

| Result | Score |
| --- | --- |
| Only TLS 1.2 and/or TLS 1.3 accepted (no Phase out or Insufficient versions) | Pass |
| Any Phase out or Insufficient (SSL) version accepted | Fail |
| STARTTLS not available (M.3.1 failed or N/A) | Not Executed |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Mail | Test 4.2 | Primary source |
| NCSC TLS-Security guidelines 2025-05 | Section 3.3.1, Table 1 (page 16) | Table 1: TLS versions and their security status |
