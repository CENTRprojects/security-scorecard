# W.1.5: Ciphers (Algorithm Selections)

## Summary

Checks whether the web server supports only secure cipher suites (classified as Good or Sufficient), with no Phase out or Insufficient algorithm selections.

## Test Procedure

5. Enumerate all cipher suites accepted by the web server by probing with cipher-specific client hellos.
6. Classify each accepted cipher suite according to the NCSC-NL TLS Guidelines v2.1 (guidelines B2-1 to B2-4, tables 2, 4, 6, and 7).

### Good algorithm selections (TLS 1.3)

- TLS_AES_256_GCM_SHA384
- TLS_CHACHA20_POLY1305_SHA256

### Sufficient algorithm selections:

TLS 1.3

- TLS_AES_128_CCM_SHA256
- TLS_AES_128_GCM_SHA256

TLS 1.2

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
- TLS_ECDHE_RSA_WITH_CAMELLIA_128_GCM_SHA256
- TLS_ECDHE_RSA_WITH_CAMELLIA_256_CBC_SHA384
- TLS_ECDHE_RSA_WITH_CAMELLIA_256_GCM_SHA384
- TLS_ECDHE_RSA_WITH_CAMELLIA_128_GCM_SHA256
- TLS_ECDHE_RSA_WITH_CAMELLIA_256_CBC_SHA384
- TLS_ECDHE_RSA_WITH_CAMELLIA_256_GCM_SHA384

Please note: the list above is copied from NCSC TLS Guidelines 2025-05 which explicitly states “this Appendix does not contain an exhaustive list of cipher suites that are Good, Sufficient and To be phased out. It is possible that your TLS library supports other cipher suites. In that case, please check the extent to which you can support these cipher suites based on the security level of the respective algorithms.”.

More algorithms can be tested. The test shall be diligent about appropriate categorisations of the additional tests.

7. Any cipher suite not in the above lists (considering the note above) is classified as Insufficient.
8. The test passes if no Phase out or Insufficient cipher suites are accepted.

Note: Cipher suites using PSK or SRP for key exchange cannot be detected due to a limitation of the testing method. The bracket notation (e.g. **`[1.2]`**) indicates the minimum TLS version required for that cipher suite. Naming follows the OpenSSL convention; for TLS 1.3, OpenSSL follows the IANA convention.

Implementation note: for Pass/Fail criteria it is enough to just test Phased Out algorithms.

## Scoring

| Result | Score |
| --- | --- |
| Only Good and/or Sufficient cipher suites accepted | Pass |
| Any Phase out or Insufficient cipher suite accepted | Fail |
| HTTPS not available (W.1.1 failed) | Not Executed |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Web | Test 4.2 | Primary source |
| NCSC-NL TLS Guidelines 2025-05 | Appendix B | List of cipher suites |
