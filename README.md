check_dane
==========

Nagios/Icinga plugin for checking DANE/TLSA records.

It compares the DANE/TLSA record against the TLS certificate provided by a service.

Usage
=====

    -h, --help            show this help message and exit
    --host HOST, -H HOST  Hostname to check.
    --port PORT, -p PORT  Connect to TCP port.
    --ip IP, -I IP        Connect to this IP instead of resolving the host.
    --starttls {smtp,imap,xmpp}
                          Send the protocol-specific messages to enable TLS.
    --check-pkix          Additionally perform traditional checks on the
                          certificate (ca trust path, hostname, expiry).
    --min-days-valid MIN_DAYS_VALID
                          Minimum number of days a certificate has to be valid.
                          Format: INTEGER[,INTEGER]. 1st is #days for warning,
                          2nd is critical.
    --no-dnssec           Continue even when DNS replies aren't DNSSEC
                          authenticated.
    --nameserver NAMESERVER
                          Use a custom nameserver.
    --timeout TIMEOUT     Network timeone in sec. Default: 10
    --version             show program's version number and exit

Supported TLSA records
======================

   * Certificate Usage: Only "Domain-issued certificate" (3) is supported.
   * Selector: "Full certificate" (0) and SubjectPublicKeyInfo (1)
   * Matching Type: "Exact match" (0), SHA-256 hash (1) and SHA-512 hash (2)

Requirements
============

   * Python >= 3.4
   * [dnspython](http://www.dnspython.org/)
   * openssl binary
   * DNSSEC capable resolver (or use --no-dnssec but be aware of the security implications)

Examples
========

   * check_dane -H mx.example.com -p 25 --starttls smtp
   * check_dane -H example.com -p 443 --check-pkix
