# Domain Security Scorecard

CENTR Task Force Document

Authors:

- Lavie Ben-Baruch – ISOC-IL
- Maarten Bosteels - DNS Belgium
- Alejandro Cañas Nieto - RED.es
- Sebastian Castro - .ie
- Simon Cox – Nominet
- Marco Davids – SIDN
- Mats Dufberg – Internetstiftelsen
- Ronald Geens – DNS Belgium
- Thomas Green – Afnic
- Michiel Henneke - SIDN
- Jordi Iparraguirre – Eurid
- Pawel Kowalik – DENIC
- Alexander Mayrhofer – NIC.at
- Ricardo Pires - .pt
- Jing Qiao – Internet.nz
- Dominic Rivett – Nominet
- Tomas Simonaitis - Domreg.lt
- Oleksandr Sobko – EURID
- Jaromir Talir – NIC.cz
- Ulrich Wisser - ICANN
- Namrata Gilada – CENTR

Version 1.0 (Final Authors’ Recommendation)  
Sep 22, 2026

## Abstract

This document defines the Domain Security Scorecard - a structured set of tests for assessing the security configuration of a domain name across three categories: Domain (e.g. security.txt, DNSSEC), Mail (e.g. SPF, DKIM, DMARC, TLS, DANE), and Web (e.g. HTTPS/TLS configuration, security headers, CAA records). By providing a common, reproducible set of test definitions, the methodology enables consistent measurement and comparison of domain security posture across different TLD zones.

## Table of Contents

- Domain
  - Tests
    - RFC 9116 / security.txt
      - [D.1.1: security.txt File](domain/D.1-security.txt/D.1.1-security.txt.md)
    - DNSSEC
      - [D.2.1: DNSSEC Existence](domain/D.2-dnssec/D.2.1-dnssec-existence.md)
      - [D.2.2: DNSSEC Validity](domain/D.2-dnssec/D.2.2-dnssec-validity.md)
- Mail
  - Tests
    - Email Authentication
      - [M.1.1: DMARC Existence](mail/M.1-email-authentication/M.1.1-dmarc-existence.md)
      - [M.1.2: DMARC Policy](mail/M.1-email-authentication/M.1.2-dmarc-policy.md)
      - [M.1.3: DKIM Existence](mail/M.1-email-authentication/M.1.3-dkim-existence.md)
      - [M.1.4: SPF Existence](mail/M.1-email-authentication/M.1.4-spf-existence.md)
      - [M.1.5: SPF Policy](mail/M.1-email-authentication/M.1.5-spf-policy.md)
    - Advanced Mail Security
      - [M.2.1: MTA-STS](mail/M.2-advanced-mail-security/M.2.1-mta-sts.md)
      - [M.2.2: TLS-RPT](mail/M.2-advanced-mail-security/M.2.2-tls-rpt.md)
      - [M.2.3: BIMI](mail/M.2-advanced-mail-security/M.2.3-bimi.md)
    - TLS Security
      - [M.3.1: STARTTLS Available](mail/M.3-tls-security/M.3.1-starttls-available.md)
      - [M.3.2: TLS Version](mail/M.3-tls-security/M.3.2-tls-version.md)
      - [M.3.3: Ciphers (Algorithm Selections)](mail/M.3-tls-security/M.3.3-ciphers.md)
      - [M.3.4: Cipher Order](mail/M.3-tls-security/M.3.4-cipher-order.md)
      - [M.3.5: Key Exchange Parameters](mail/M.3-tls-security/M.3.5-key-exchange-parameters.md)
      - [M.3.6: Hash Function for Key Exchange](mail/M.3-tls-security/M.3.6-hash-function-for-key-exchange.md)
      - [M.3.7: TLS Compression](mail/M.3-tls-security/M.3.7-tls-compression.md)
      - [M.3.8: Secure Renegotiation](mail/M.3-tls-security/M.3.8-secure-renegotiation.md)
      - [M.3.9: Public Key of Certificate](mail/M.3-tls-security/M.3.9-public-key-of-certificate.md)
      - [M.3.10: Signature of Certificate](mail/M.3-tls-security/M.3.10-signature-of-certificate.md)
      - [M.3.11: DANE Existence](mail/M.3-tls-security/M.3.11-dane-existence.md)
      - [M.3.12: DANE-Validity](mail/M.3-tls-security/M.3.12-dane-validity.md)
    - DNSSEC
      - [M.4.1: DNSSEC Existence (Mail Server Domain)](mail/M.4-dnssec/M.4.1-dnssec-existence.md)
      - [M.4.2: DNSSEC Validity (Mail Server Domain)](mail/M.4-dnssec/M.4.2-dnssec-validity.md)
- Web
  - Tests
    - HTTPS / TLS Security
      - [W.1.1: HTTPS Availability](web/W.1-https-tls-security/W.1.1-https-availability.md)
      - [W.1.2: HTTPS Redirect](web/W.1-https-tls-security/W.1.2-https-redirect.md)
      - [W.1.3: HSTS (HTTP Strict Transport Security)](web/W.1-https-tls-security/W.1.3-hsts.md)
      - [W.1.4: TLS Version Support](web/W.1-https-tls-security/W.1.4-tls-version-support.md)
      - [W.1.5: Ciphers (Algorithm Selections)](web/W.1-https-tls-security/W.1.5-ciphers.md)
      - [W.1.6: Cipher Order](web/W.1-https-tls-security/W.1.6-cipher-order.md)
      - [W.1.7: Key Exchange Parameters](web/W.1-https-tls-security/W.1.7-key-exchange-parameters.md)
      - [W.1.8: Hash Function for Key Exchange](web/W.1-https-tls-security/W.1.8-hash-function-for-key-exchange.md)
      - [W.1.9: TLS Compression](web/W.1-https-tls-security/W.1.9-tls-compression.md)
      - [W.1.10: Secure Renegotiation](web/W.1-https-tls-security/W.1.10-secure-renegotiation.md)
      - [W.1.11: 0-RTT (Zero Round Trip Time)](web/W.1-https-tls-security/W.1.11-0-rtt.md)
      - [W.1.12: Trust Chain of Certificate](web/W.1-https-tls-security/W.1.12-trust-chain-of-certificate.md)
      - [W.1.13: Public Key of Certificate](web/W.1-https-tls-security/W.1.13-public-key-of-certificate.md)
      - [W.1.14: Signature of Certificate](web/W.1-https-tls-security/W.1.14-signature-of-certificate.md)
      - [W.1.15: Domain Name on Certificate](web/W.1-https-tls-security/W.1.15-domain-name-on-certificate.md)
    - Security Headers
      - [W.2.1: X-Content-Type-Options Header](web/W.2-security-headers/W.2.1-x-content-type-options-header.md)
      - [W.2.2: Content-Security-Policy (CSP)](web/W.2-security-headers/W.2.2-content-security-policy.md)
      - [W.2.3: Referrer-Policy Header](web/W.2-security-headers/W.2.3-referrer-policy-header.md)
    - CAA Records
      - [W.3.1: CAA Records](web/W.3-caa-records/W.3.1-caa-records.md)
