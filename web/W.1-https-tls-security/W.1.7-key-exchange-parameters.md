# W.1.7: Key Exchange Parameters

## Summary

Checks whether the web server uses secure Diffie-Hellman key exchange parameters (sufficiently large ECDHE curves or approved DHE finite field groups).

## Test Procedure

During TLS handshake with the web server:

### ECDHE (Elliptic Curve Diffie-Hellman Ephemeral):

1. Record the elliptic curve offered by the server for ECDHE key exchange.
2. Classify the curve:

| Curve | Classification |
| --- | --- |
| secp384r1, secp256r1, x448, x25519 | Sufficient |
| secp224r1 | Phase out |
| Other curves | Insufficient |

### DHE (Diffie-Hellman Ephemeral):

1. Record the DHE finite field group offered by the server.
2. Verify the group matches one of the predefined finite field groups from RFC 7919 by comparing its sha256 checksum:

| Group | Classification | sha256 checksum |
| --- | --- | --- |
| ffdhe4096 (RFC 7919) | Phase Out | **`64852d6890ff9e62eecd1ee89c72af9af244dfef5b853bcedea3dfd7aade22b3`** |
| ffdhe3072 (RFC 7919) | Phase out | **`c410cc9c4fd85d2c109f7ebe5930ca5304a52927c0ebcb1a11c5cf6b2386bbab`** |
| ffdhe8192, ffdhe6144 (RFC 7919) | Phase out | — |
| ffdhe2048 (RFC 7919) | Insufficient | **`9ba6429597aeed2d8617a7705b56e96d044f64b07971659382e426675105654b`** |
| Self-generated or other groups | Insufficient | — |

1. Self-generated DHE groups that do not match RFC 7919 are classified as Insufficient.

Note: RSA key exchange is Phase out; its public key parameters are tested separately in W.1.13 (Public Key of Certificate). IANA naming is used above; **`prime256v1`** (ANSI) and **`NIST P-256`** are alternative names for **`secp256r1`**. Currently, ECDHE curve names cannot always be retrieved — only the bit-length is checked (minimum 224 bits for Phase out detection).

## Scoring

| Result | Score |
| --- | --- |
| All key exchange parameters are Good or Sufficient | Pass |
| Any Insufficient parameter used | Fail |
| HTTPS not available (W.1.1 failed) | Not Executed |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Web | Test 4.4 | Primary source |
| NCSC-NL TLS Guidelines 2025-05 | Section 3.3.3, Table 7 and Section 3.3.2 Table 3 | Parameter classification |
| RFC 7919 | — | Predefined finite field groups for DHE |
