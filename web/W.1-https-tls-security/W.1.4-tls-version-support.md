# W.1.4: TLS Version Support

## Summary

Checks whether the web server supports only secure TLS versions, rejecting deprecated SSL/TLS versions that expose connections to known attacks.

## Test Procedure

1. Probe the web server for support of each TLS/SSL version by attempting handshakes with version-specific client hellos:
   - TLS 1.3
   - TLS 1.2
   - TLS 1.1
   - TLS 1.0
   - SSL 3.0, 2.0, 1.0
2. Record which versions the server accepts.
3. Classify each supported version:

### Note

Due to growing difficulty in testing of SSL 1.0, where support for it has been removed from many common libraries, the implementations may skip this test but shall be explicit about doing so.

### Version classification (NCSC-NL TLS Guidelines 2025-05, Table 1, page 16):

| Version | Classification |
| --- | --- |
| TLS 1.3 | Good |
| TLS 1.2 | Sufficient |
| TLS 1.1, TLS 1.0 | Insufficient |
| SSL 3.0, SSL 2.0, SSL 1.0 | Insufficient |

4. The test passes if no Phase out or Insufficient versions are accepted.

Note: Browser makers have announced cessation of support for TLS 1.1 and 1.0. Websites that do not support TLS 1.2 or 1.3 will become unreachable in modern browsers.

## Scoring

| Result | Score |
| --- | --- |
| Only TLS 1.2 and/or TLS 1.3 accepted (no Phase out or Insufficient versions) | Pass |
| Any Phase out (TLS 1.1, TLS 1.0) or Insufficient (SSL) version accepted | Fail |
| HTTPS not available (W.1.1 failed) | Not Executed |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Web | Test 4.1 | Primary source |
| NCSC-NL TLS Guidelines v2.1 | B1-1, Table 1 | Version classification |
| NCSC-NL TLS Guidelines 2025-05 | Table 1, page 16 | TLS versions and their security status |
| BCP195 | https://datatracker.ietf.org/doc/bcp195/ |  |

**`https://datatracker.ietf.org/doc/bcp195/`**
