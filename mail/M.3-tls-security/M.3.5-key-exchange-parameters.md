# M.3.5: Key Exchange Parameters

## Summary

Checks whether the public parameters used in Diffie-Hellman key exchange by each receiving mail server (MX host) are secure (sufficiently large key sizes or approved named groups).

## Test Procedure

After STARTTLS negotiation with each MX host (per M.3.1):

### ECDHE (Elliptic Curve Diffie-Hellman Ephemeral):

1. During TLS handshake, record the elliptic curve offered by the server for ECDHE key exchange.
2. Classify the curve:

| Curve | Classification |
| --- | --- |
| secp384r1, secp256r1, x448, x25519 | Good |
| secp224r1 | Phase out |
| Other curves | Insufficient |

### DHE (Diffie-Hellman Ephemeral):

1. During TLS handshake, record the DHE finite field group offered by the server.
2. Verify the group matches one of the predefined finite field groups from RFC 7919 by comparing its sha256 checksum:

| Group | Classification | sha256 checksum |
| --- | --- | --- |
| ffdhe4096 (RFC 7919) | Phase out | **`64852d6890ff9e62eecd1ee89c72af9af244dfef5b853bcedea3dfd7aade22b3`** |
| ffdhe3072 (RFC 7919) | Phase out | **`c410cc9c4fd85d2c109f7ebe5930ca5304a52927c0ebcb1a11c5cf6b2386bbab`** |
| ffdhe8192, ffdhe6144 (RFC 7919) | Phase out | — |
| ffdhe2048 (RFC 7919) | Insufficient | **`9ba6429597aeed2d8617a7705b56e96d044f64b07971659382e426675105654b`** |
| Self-generated or other groups | Insufficient | — |

1. Self-generated DHE groups that do not match RFC 7919 are classified as Insufficient.

Note: RSA key exchange is classified as Phase out; its public parameters are tested under M.3.9 (Public Key of Certificate). The IANA curve names are used above; alternative names include **`prime256v1`** (ANSI) and **`NIST P-256`** for **`secp256r1`**. Currently ECDHE curve names cannot always be retrieved — only the bit-length is checked (minimum 224 bits for Phase out detection).

## Scoring

| Result | Score |
| --- | --- |
| All key exchange parameters are Good or Sufficient | Pass |
| Any Insufficient or Phased out parameter used (e.g., self-generated DHE group, curve shorter than 224 bits) | Fail |
| STARTTLS not available (M.3.1 failed or N/A) | Not Executed |

## References

| Source | ID | Notes |
| --- | --- | --- |
| Internet.nl Mail | Test 4.5 | Primary source |
| NCSC-NL TLS Guidelines 2025-05 | Section 3.3.2.1, Table 3 & Table 7 |  |
| RFC 7919 | — | Predefined finite field groups for DHE |
