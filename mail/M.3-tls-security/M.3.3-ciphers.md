# M.3.3: Ciphers (Algorithm Selections)

## Summary

Checks whether each receiving mail server (MX host) supports only secure cipher suites (classified as Good or Sufficient), with no Phase out or Insufficient algorithm selections.

## Test Procedure

After STARTTLS negotiation with each MX host (per M.3.1):

1. Enumerate all cipher suites accepted by the server by probing with cipher-specific client hellos.
2. Classify each accepted cipher suite according to the NCSC-NL TLS Guidelines 2025-05.

### Good algorithm selections (TLS 1.3):

- TLS_AES_256_GCM_SHA384
- TLS_CHACHA20_POLY1305_SHA256

### Sufficient algorithm selections (TLS 1.3):

- TLS_AES_128_CCM_SHA256
- TLS_AES_128_GCM_SHA256

### Sufficient algorithm selections (TLS 1.2):

- TLS_ECDHE_ECDSA_WITH_AES_128_CCM
- TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CCM
- TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_ECDSA_WITH_CHACHA20_POLY1305_SHA256
- TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305_SHA256

### Phase out algorithm selections:

- TLS_DHE_RSA_WITH_AES_128_CBC_SHA256
- TLS_DHE_RSA_WITH_AES_128_CCM
- TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_DHE_RSA_WITH_AES_256_CBC_SHA256
- TLS_DHE_RSA_WITH_AES_256_CCM
- TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_DHE_RSA_WITH_ARIA_128_CBC_SHA256
- TLS_DHE_RSA_WITH_ARIA_128_GCM_SHA256
- TLS_DHE_RSA_WITH_ARIA_256_CBC_SHA384
- TLS_DHE_RSA_WITH_ARIA_256_GCM_SHA384
- TLS_DHE_RSA_WITH_CAMELLIA_128_CBC_SHA256
- TLS_DHE_RSA_WITH_CAMELLIA_128_GCM_SHA256
- TLS_DHE_RSA_WITH_CAMELLIA_256_CBC_SHA256
- TLS_DHE_RSA_WITH_CAMELLIA_256_GCM_SHA384
- TLS_DHE_RSA_WITH_CHACHA20_POLY1305_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_ECDSA_WITH_ARIA_128_CBC_SHA256
- TLS_ECDHE_ECDSA_WITH_ARIA_128_GCM_SHA256
- TLS_ECDHE_ECDSA_WITH_ARIA_256_CBC_SHA384
- TLS_ECDHE_ECDSA_WITH_ARIA_256_GCM_SHA384
- TLS_ECDHE_ECDSA_WITH_CAMELLIA_128_CBC_SHA256
- TLS_ECDHE_ECDSA_WITH_CAMELLIA_128_GCM_SHA256
- TLS_ECDHE_ECDSA_WITH_CAMELLIA_256_CBC_SHA384
- TLS_ECDHE_ECDSA_WITH_CAMELLIA_256_GCM_SHA384
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_RSA_WITH_ARIA_128_CBC_SHA256
- TLS_ECDHE_RSA_WITH_ARIA_128_GCM_SHA256
- TLS_ECDHE_RSA_WITH_ARIA_256_CBC_SHA384
- TLS_ECDHE_RSA_WITH_ARIA_256_GCM_SHA384
- TLS_ECDHE_RSA_WITH_CAMELLIA_128_CBC_SHA256
- TLS_ECDHE_RSA_WITH_CAMELLIA_128_GCM_SHA256
- TLS_ECDHE_RSA_WITH_CAMELLIA_256_CBC_SHA384
- TLS_ECDHE_RSA_WITH_CAMELLIA_256_GCM_SHA384

3. Any cipher suite not in the above lists is classified as Insufficient.
4. The test passes if no Phase out or Insufficient cipher suites are accepted.

Note: Cipher suites using PSK or SRP for key exchange cannot be detected due to a limitation of the testing method. Naming follows the OpenSSL convention; for TLS 1.3, OpenSSL follows the IANA convention. The bracket notation (e.g. **`[1.2]`**) indicates the minimum TLS version required for that cipher suite.

## Scoring

| Result | Score |
| --- | --- |
| Only Good and/or Sufficient cipher suites accepted | Pass |
| Any Phase out or Insufficient cipher suite accepted | Fail |
| STARTTLS not available (M.3.1 failed or N/A) | Not Executed |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Mail | Test 4.3 | Primary source |
| NCSC-NL TLS Guidelines 2025-05 | Appendix B | List of cipher suites |
