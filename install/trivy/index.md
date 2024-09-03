# Install Trivy

<!-- TOC -->

- [Install Trivy](#install-trivy)
  - [Overview](#overview)
    - [What is Trivy?](#what-is-trivy)
  - [Installation](#installation)
    - [Mac OS](#mac-os)
  - [Apply](#apply)

<!-- /TOC -->


## Overview

### What is Trivy?
https://trivy.dev/

Trivy is the most popular open source security scanner, reliable, fast, and easy to use. Use Trivy to find vulnerabilities & IaC misconfigurations, SBOM discovery, Cloud scanning, Kubernetes security risks, and more.

## Installation

### Mac OS
```bash
brew install trivy
```

## Apply

```bash
trivy image --no-progress --severity HIGH,CRITICAL ajktown/api
trivy image --no-progress --severity HIGH,CRITICAL ajktown/wordnote
trivy image --no-progress --severity HIGH,CRITICAL ajktown/consistency
```

Sample Result:
```bash
aj % trivy image --no-progress --severity HIGH,CRITICAL ajktown/wordnote
2024-09-03T09:01:33+09:00	INFO	[vuln] Vulnerability scanning is enabled
2024-09-03T09:01:33+09:00	INFO	[secret] Secret scanning is enabled
2024-09-03T09:01:33+09:00	INFO	[secret] If your scanning is slow, please try '--scanners vuln' to disable secret scanning
2024-09-03T09:01:33+09:00	INFO	[secret] Please see also https://aquasecurity.github.io/trivy/v0.54/docs/scanner/secret#recommendation for faster secret detection
2024-09-03T09:01:33+09:00	INFO	Detected OS	family="debian" version="12.5"
2024-09-03T09:01:33+09:00	INFO	[debian] Detecting vulnerabilities...	os_version="12" pkg_num=413
2024-09-03T09:01:33+09:00	INFO	Number of language-specific files	num=1
2024-09-03T09:01:33+09:00	INFO	[node-pkg] Detecting vulnerabilities...
2024-09-03T09:01:33+09:00	WARN	Using severities from other vendors for some vulnerabilities. Read https://aquasecurity.github.io/trivy/v0.54/docs/scanner/vulnerability#severity-selection for details.

ajktown/wordnote (debian 12.5)

Total: 203 (HIGH: 183, CRITICAL: 20)

┌─────────────────────────┬────────────────┬──────────┬──────────────┬─────────────────────────┬────────────────────────┬──────────────────────────────────────────────────────────────┐
│         Library         │ Vulnerability  │ Severity │    Status    │    Installed Version    │     Fixed Version      │                            Title                             │
├─────────────────────────┼────────────────┼──────────┼──────────────┼─────────────────────────┼────────────────────────┼──────────────────────────────────────────────────────────────┤
│ curl                    │ CVE-2024-2398  │ HIGH     │ fixed        │ 7.88.1-10+deb12u5       │ 7.88.1-10+deb12u6      │ curl: HTTP/2 push headers memory-leak                        │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-2398                    │
├─────────────────────────┼────────────────┤          │              ├─────────────────────────┼────────────────────────┼──────────────────────────────────────────────────────────────┤
│ gir1.2-gdkpixbuf-2.0    │ CVE-2022-48622 │          │              │ 2.42.10+dfsg-1+b1       │ 2.42.10+dfsg-1+deb12u1 │ gnome: heap memory corruption on gdk-pixbuf                  │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2022-48622                   │
├─────────────────────────┼────────────────┼──────────┼──────────────┼─────────────────────────┼────────────────────────┼──────────────────────────────────────────────────────────────┤
│ git                     │ CVE-2024-32002 │ CRITICAL │ affected     │ 1:2.39.2-1.1            │                        │ git: Recursive clones RCE                                    │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-32002                   │
│                         ├────────────────┼──────────┤              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2023-25652 │ HIGH     │              │                         │                        │ git: by feeding specially crafted input to `git apply        │
│                         │                │          │              │                         │                        │ --reject`, a path...                                         │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-25652                   │
│                         ├────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2023-29007 │          │              │                         │                        │ git: arbitrary configuration injection when renaming or      │
│                         │                │          │              │                         │                        │ deleting a section from a...                                 │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-29007                   │
│                         ├────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-32004 │          │              │                         │                        │ git: RCE while cloning local repos                           │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-32004                   │
│                         ├────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-32465 │          │              │                         │                        │ git: additional local RCE                                    │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-32465                   │
├─────────────────────────┼────────────────┼──────────┤              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│ git-man                 │ CVE-2024-32002 │ CRITICAL │              │                         │                        │ git: Recursive clones RCE                                    │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-32002                   │
│                         ├────────────────┼──────────┤              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2023-25652 │ HIGH     │              │                         │                        │ git: by feeding specially crafted input to `git apply        │
│                         │                │          │              │                         │                        │ --reject`, a path...                                         │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-25652                   │
│                         ├────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2023-29007 │          │              │                         │                        │ git: arbitrary configuration injection when renaming or      │
│                         │                │          │              │                         │                        │ deleting a section from a...                                 │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-29007                   │
│                         ├────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-32004 │          │              │                         │                        │ git: RCE while cloning local repos                           │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-32004                   │
│                         ├────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-32465 │          │              │                         │                        │ git: additional local RCE                                    │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-32465                   │
├─────────────────────────┼────────────────┼──────────┼──────────────┼─────────────────────────┼────────────────────────┼──────────────────────────────────────────────────────────────┤
│ krb5-multidev           │ CVE-2024-37371 │ CRITICAL │ fixed        │ 1.20.1-2+deb12u1        │ 1.20.1-2+deb12u2       │ krb5: GSS message token handling                             │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-37371                   │
│                         ├────────────────┼──────────┼──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-26462 │ HIGH     │ affected     │                         │                        │ krb5: Memory leak at /krb5/src/kdc/ndr.c                     │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-26462                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-37370 │          │ fixed        │                         │ 1.20.1-2+deb12u2       │ krb5: GSS message token handling                             │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-37370                   │
├─────────────────────────┼────────────────┼──────────┼──────────────┼─────────────────────────┼────────────────────────┼──────────────────────────────────────────────────────────────┤
│ libaom3                 │ CVE-2023-6879  │ CRITICAL │ affected     │ 3.6.0-1                 │                        │ aom: heap-buffer-overflow on frame size change               │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-6879                    │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-5171  │          │ fixed        │                         │ 3.6.0-1+deb12u1        │ libaom: Integer overflow in internal                         │
│                         │                │          │              │                         │                        │ function img_alloc_helper                                    │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-5171                    │
│                         ├────────────────┼──────────┼──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2023-39616 │ HIGH     │ affected     │                         │                        │ AOMedia v3.0.0 to v3.5.0 was discovered to contain an        │
│                         │                │          │              │                         │                        │ invalid read mem...                                          │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-39616                   │
├─────────────────────────┼────────────────┤          ├──────────────┼─────────────────────────┼────────────────────────┼──────────────────────────────────────────────────────────────┤
│ libcurl3-gnutls         │ CVE-2024-2398  │          │ fixed        │ 7.88.1-10+deb12u5       │ 7.88.1-10+deb12u6      │ curl: HTTP/2 push headers memory-leak                        │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-2398                    │
├─────────────────────────┤                │          │              │                         │                        │                                                              │
│ libcurl4                │                │          │              │                         │                        │                                                              │
│                         │                │          │              │                         │                        │                                                              │
├─────────────────────────┤                │          │              │                         │                        │                                                              │
│ libcurl4-openssl-dev    │                │          │              │                         │                        │                                                              │
│                         │                │          │              │                         │                        │                                                              │
├─────────────────────────┼────────────────┤          ├──────────────┼─────────────────────────┼────────────────────────┼──────────────────────────────────────────────────────────────┤
│ libexpat1               │ CVE-2023-52425 │          │ affected     │ 2.5.0-1                 │                        │ expat: parsing large tokens can trigger a denial of service  │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-52425                   │
├─────────────────────────┤                │          │              │                         ├────────────────────────┤                                                              │
│ libexpat1-dev           │                │          │              │                         │                        │                                                              │
│                         │                │          │              │                         │                        │                                                              │
├─────────────────────────┼────────────────┤          ├──────────────┼─────────────────────────┼────────────────────────┼──────────────────────────────────────────────────────────────┤
│ libgdk-pixbuf-2.0-0     │ CVE-2022-48622 │          │ fixed        │ 2.42.10+dfsg-1+b1       │ 2.42.10+dfsg-1+deb12u1 │ gnome: heap memory corruption on gdk-pixbuf                  │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2022-48622                   │
├─────────────────────────┤                │          │              │                         │                        │                                                              │
│ libgdk-pixbuf-2.0-dev   │                │          │              │                         │                        │                                                              │
│                         │                │          │              │                         │                        │                                                              │
├─────────────────────────┤                │          │              │                         │                        │                                                              │
│ libgdk-pixbuf2.0-bin    │                │          │              │                         │                        │                                                              │
│                         │                │          │              │                         │                        │                                                              │
├─────────────────────────┤                │          │              ├─────────────────────────┤                        │                                                              │
│ libgdk-pixbuf2.0-common │                │          │              │ 2.42.10+dfsg-1          │                        │                                                              │
│                         │                │          │              │                         │                        │                                                              │
├─────────────────────────┼────────────────┼──────────┤              ├─────────────────────────┼────────────────────────┼──────────────────────────────────────────────────────────────┤
│ libgssapi-krb5-2        │ CVE-2024-37371 │ CRITICAL │              │ 1.20.1-2+deb12u1        │ 1.20.1-2+deb12u2       │ krb5: GSS message token handling                             │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-37371                   │
│                         ├────────────────┼──────────┼──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-26462 │ HIGH     │ affected     │                         │                        │ krb5: Memory leak at /krb5/src/kdc/ndr.c                     │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-26462                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-37370 │          │ fixed        │                         │ 1.20.1-2+deb12u2       │ krb5: GSS message token handling                             │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-37370                   │
├─────────────────────────┼────────────────┼──────────┤              │                         │                        ├──────────────────────────────────────────────────────────────┤
│ libgssrpc4              │ CVE-2024-37371 │ CRITICAL │              │                         │                        │ krb5: GSS message token handling                             │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-37371                   │
│                         ├────────────────┼──────────┼──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-26462 │ HIGH     │ affected     │                         │                        │ krb5: Memory leak at /krb5/src/kdc/ndr.c                     │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-26462                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-37370 │          │ fixed        │                         │ 1.20.1-2+deb12u2       │ krb5: GSS message token handling                             │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-37370                   │
├─────────────────────────┼────────────────┤          ├──────────────┼─────────────────────────┼────────────────────────┼──────────────────────────────────────────────────────────────┤
│ libharfbuzz0b           │ CVE-2023-25193 │          │ affected     │ 6.0.0+dfsg-3            │                        │ harfbuzz: allows attackers to trigger O(n^2) growth via      │
│                         │                │          │              │                         │                        │ consecutive marks                                            │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-25193                   │
├─────────────────────────┼────────────────┤          │              ├─────────────────────────┼────────────────────────┼──────────────────────────────────────────────────────────────┤
│ libheif1                │ CVE-2023-49460 │          │              │ 1.15.1-1                │                        │ libheif v1.17.5 was discovered to contain a segmentation     │
│                         │                │          │              │                         │                        │ violation via ...                                            │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-49460                   │
│                         ├────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2023-49462 │          │              │                         │                        │ libheif v1.17.5 was discovered to contain a segmentation     │
│                         │                │          │              │                         │                        │ violation via ...                                            │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-49462                   │
│                         ├────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2023-49463 │          │              │                         │                        │ libheif v1.17.5 was discovered to contain a segmentation     │
│                         │                │          │              │                         │                        │ violation via ...                                            │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-49463                   │
│                         ├────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2023-49464 │          │              │                         │                        │ libheif v1.17.5 was discovered to contain a segmentation     │
│                         │                │          │              │                         │                        │ violation via ...                                            │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-49464                   │
├─────────────────────────┼────────────────┼──────────┼──────────────┼─────────────────────────┼────────────────────────┼──────────────────────────────────────────────────────────────┤
│ libk5crypto3            │ CVE-2024-37371 │ CRITICAL │ fixed        │ 1.20.1-2+deb12u1        │ 1.20.1-2+deb12u2       │ krb5: GSS message token handling                             │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-37371                   │
│                         ├────────────────┼──────────┼──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-26462 │ HIGH     │ affected     │                         │                        │ krb5: Memory leak at /krb5/src/kdc/ndr.c                     │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-26462                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-37370 │          │ fixed        │                         │ 1.20.1-2+deb12u2       │ krb5: GSS message token handling                             │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-37370                   │
├─────────────────────────┼────────────────┼──────────┤              │                         │                        ├──────────────────────────────────────────────────────────────┤
│ libkadm5clnt-mit12      │ CVE-2024-37371 │ CRITICAL │              │                         │                        │ krb5: GSS message token handling                             │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-37371                   │
│                         ├────────────────┼──────────┼──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-26462 │ HIGH     │ affected     │                         │                        │ krb5: Memory leak at /krb5/src/kdc/ndr.c                     │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-26462                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-37370 │          │ fixed        │                         │ 1.20.1-2+deb12u2       │ krb5: GSS message token handling                             │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-37370                   │
├─────────────────────────┼────────────────┼──────────┤              │                         │                        ├──────────────────────────────────────────────────────────────┤
│ libkadm5srv-mit12       │ CVE-2024-37371 │ CRITICAL │              │                         │                        │ krb5: GSS message token handling                             │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-37371                   │
│                         ├────────────────┼──────────┼──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-26462 │ HIGH     │ affected     │                         │                        │ krb5: Memory leak at /krb5/src/kdc/ndr.c                     │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-26462                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-37370 │          │ fixed        │                         │ 1.20.1-2+deb12u2       │ krb5: GSS message token handling                             │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-37370                   │
├─────────────────────────┼────────────────┼──────────┤              │                         │                        ├──────────────────────────────────────────────────────────────┤
│ libkdb5-10              │ CVE-2024-37371 │ CRITICAL │              │                         │                        │ krb5: GSS message token handling                             │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-37371                   │
│                         ├────────────────┼──────────┼──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-26462 │ HIGH     │ affected     │                         │                        │ krb5: Memory leak at /krb5/src/kdc/ndr.c                     │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-26462                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-37370 │          │ fixed        │                         │ 1.20.1-2+deb12u2       │ krb5: GSS message token handling                             │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-37370                   │
├─────────────────────────┼────────────────┼──────────┤              │                         │                        ├──────────────────────────────────────────────────────────────┤
│ libkrb5-3               │ CVE-2024-37371 │ CRITICAL │              │                         │                        │ krb5: GSS message token handling                             │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-37371                   │
│                         ├────────────────┼──────────┼──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-26462 │ HIGH     │ affected     │                         │                        │ krb5: Memory leak at /krb5/src/kdc/ndr.c                     │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-26462                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-37370 │          │ fixed        │                         │ 1.20.1-2+deb12u2       │ krb5: GSS message token handling                             │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-37370                   │
├─────────────────────────┼────────────────┼──────────┤              │                         │                        ├──────────────────────────────────────────────────────────────┤
│ libkrb5-dev             │ CVE-2024-37371 │ CRITICAL │              │                         │                        │ krb5: GSS message token handling                             │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-37371                   │
│                         ├────────────────┼──────────┼──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-26462 │ HIGH     │ affected     │                         │                        │ krb5: Memory leak at /krb5/src/kdc/ndr.c                     │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-26462                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-37370 │          │ fixed        │                         │ 1.20.1-2+deb12u2       │ krb5: GSS message token handling                             │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-37370                   │
├─────────────────────────┼────────────────┼──────────┤              │                         │                        ├──────────────────────────────────────────────────────────────┤
│ libkrb5support0         │ CVE-2024-37371 │ CRITICAL │              │                         │                        │ krb5: GSS message token handling                             │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-37371                   │
│                         ├────────────────┼──────────┼──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-26462 │ HIGH     │ affected     │                         │                        │ krb5: Memory leak at /krb5/src/kdc/ndr.c                     │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-26462                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-37370 │          │ fixed        │                         │ 1.20.1-2+deb12u2       │ krb5: GSS message token handling                             │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-37370                   │
├─────────────────────────┼────────────────┤          ├──────────────┼─────────────────────────┼────────────────────────┼──────────────────────────────────────────────────────────────┤
│ libldap-2.5-0           │ CVE-2023-2953  │          │ affected     │ 2.5.13+dfsg-5           │                        │ openldap: null pointer dereference in ber_memalloc_x         │
│                         │                │          │              │                         │                        │ function                                                     │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-2953                    │
├─────────────────────────┼────────────────┼──────────┤              ├─────────────────────────┼────────────────────────┼──────────────────────────────────────────────────────────────┤
│ libopenexr-3-1-30       │ CVE-2023-5841  │ CRITICAL │              │ 3.1.5-5                 │                        │ OpenEXR: Heap Overflow in Scanline Deep Data Parsing         │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-5841                    │
├─────────────────────────┤                │          │              │                         ├────────────────────────┤                                                              │
│ libopenexr-dev          │                │          │              │                         │                        │                                                              │
│                         │                │          │              │                         │                        │                                                              │
├─────────────────────────┼────────────────┼──────────┤              ├─────────────────────────┼────────────────────────┼──────────────────────────────────────────────────────────────┤
│ libopenjp2-7            │ CVE-2021-3575  │ HIGH     │              │ 2.5.0-2                 │                        │ openjpeg: heap-buffer-overflow in color.c may lead to DoS or │
│                         │                │          │              │                         │                        │ arbitrary code execution...                                  │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2021-3575                    │
├─────────────────────────┤                │          │              │                         ├────────────────────────┤                                                              │
│ libopenjp2-7-dev        │                │          │              │                         │                        │                                                              │
│                         │                │          │              │                         │                        │                                                              │
│                         │                │          │              │                         │                        │                                                              │
├─────────────────────────┼────────────────┤          │              ├─────────────────────────┼────────────────────────┼──────────────────────────────────────────────────────────────┤
│ libperl5.36             │ CVE-2023-31484 │          │              │ 5.36.0-7+deb12u1        │                        │ perl: CPAN.pm does not verify TLS certificates when          │
│                         │                │          │              │                         │                        │ downloading distributions over HTTPS...                      │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-31484                   │
├─────────────────────────┼────────────────┤          ├──────────────┼─────────────────────────┼────────────────────────┼──────────────────────────────────────────────────────────────┤
│ libpq-dev               │ CVE-2024-7348  │          │ fixed        │ 15.6-0+deb12u1          │ 15.8-0+deb12u1         │ postgresql: PostgreSQL relation replacement during pg_dump   │
│                         │                │          │              │                         │                        │ executes arbitrary SQL                                       │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-7348                    │
├─────────────────────────┤                │          │              │                         │                        │                                                              │
│ libpq5                  │                │          │              │                         │                        │                                                              │
│                         │                │          │              │                         │                        │                                                              │
│                         │                │          │              │                         │                        │                                                              │
├─────────────────────────┼────────────────┤          │              ├─────────────────────────┼────────────────────────┼──────────────────────────────────────────────────────────────┤
│ libpython3.11-minimal   │ CVE-2023-24329 │          │              │ 3.11.2-6                │ 3.11.2-6+deb12u2       │ python: urllib.parse url blocklisting bypass                 │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-24329                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2023-41105 │          │              │                         │                        │ python: file path truncation at \0 characters                │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-41105                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2023-6597  │          │              │                         │                        │ python: Path traversal on tempfile.TemporaryDirectory        │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-6597                    │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-7592  │          │ fix_deferred │                         │                        │ cpython: python: Uncontrolled CPU resource consumption when  │
│                         │                │          │              │                         │                        │ in http.cookies module                                       │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-7592                    │
├─────────────────────────┼────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│ libpython3.11-stdlib    │ CVE-2023-24329 │          │ fixed        │                         │ 3.11.2-6+deb12u2       │ python: urllib.parse url blocklisting bypass                 │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-24329                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2023-41105 │          │              │                         │                        │ python: file path truncation at \0 characters                │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-41105                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2023-6597  │          │              │                         │                        │ python: Path traversal on tempfile.TemporaryDirectory        │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-6597                    │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-7592  │          │ fix_deferred │                         │                        │ cpython: python: Uncontrolled CPU resource consumption when  │
│                         │                │          │              │                         │                        │ in http.cookies module                                       │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-7592                    │
├─────────────────────────┼────────────────┤          ├──────────────┼─────────────────────────┼────────────────────────┼──────────────────────────────────────────────────────────────┤
│ libsqlite3-0            │ CVE-2023-7104  │          │ affected     │ 3.40.1-2                │                        │ sqlite: heap-buffer-overflow at sessionfuzz                  │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-7104                    │
├─────────────────────────┤                │          │              │                         ├────────────────────────┤                                                              │
│ libsqlite3-dev          │                │          │              │                         │                        │                                                              │
│                         │                │          │              │                         │                        │                                                              │
├─────────────────────────┼────────────────┤          ├──────────────┼─────────────────────────┼────────────────────────┼──────────────────────────────────────────────────────────────┤
│ libsystemd0             │ CVE-2023-50387 │          │ fixed        │ 252.22-1~deb12u1        │ 252.23-1~deb12u1       │ bind9: KeyTrap - Extreme CPU consumption in DNSSEC validator │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-50387                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2023-50868 │          │              │                         │                        │ bind9: Preparing an NSEC3 closest encloser proof can exhaust │
│                         │                │          │              │                         │                        │ CPU resources                                                │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-50868                   │
├─────────────────────────┼────────────────┤          ├──────────────┼─────────────────────────┼────────────────────────┼──────────────────────────────────────────────────────────────┤
│ libtiff-dev             │ CVE-2023-52355 │          │ affected     │ 4.5.0-6+deb12u1         │                        │ libtiff: TIFFRasterScanlineSize64 produce too-big size and   │
│                         │                │          │              │                         │                        │ could cause OOM                                              │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-52355                   │
│                         ├────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2023-52356 │          │              │                         │                        │ libtiff: Segment fault in libtiff in TIFFReadRGBATileExt()   │
│                         │                │          │              │                         │                        │ leading to denial of...                                      │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-52356                   │
│                         ├────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-7006  │          │              │                         │                        │ libtiff: NULL pointer dereference in tif_dirinfo.c           │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-7006                    │
├─────────────────────────┼────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│ libtiff6                │ CVE-2023-52355 │          │              │                         │                        │ libtiff: TIFFRasterScanlineSize64 produce too-big size and   │
│                         │                │          │              │                         │                        │ could cause OOM                                              │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-52355                   │
│                         ├────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2023-52356 │          │              │                         │                        │ libtiff: Segment fault in libtiff in TIFFReadRGBATileExt()   │
│                         │                │          │              │                         │                        │ leading to denial of...                                      │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-52356                   │
│                         ├────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-7006  │          │              │                         │                        │ libtiff: NULL pointer dereference in tif_dirinfo.c           │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-7006                    │
├─────────────────────────┼────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│ libtiffxx6              │ CVE-2023-52355 │          │              │                         │                        │ libtiff: TIFFRasterScanlineSize64 produce too-big size and   │
│                         │                │          │              │                         │                        │ could cause OOM                                              │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-52355                   │
│                         ├────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2023-52356 │          │              │                         │                        │ libtiff: Segment fault in libtiff in TIFFReadRGBATileExt()   │
│                         │                │          │              │                         │                        │ leading to denial of...                                      │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-52356                   │
│                         ├────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-7006  │          │              │                         │                        │ libtiff: NULL pointer dereference in tif_dirinfo.c           │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-7006                    │
├─────────────────────────┼────────────────┤          ├──────────────┼─────────────────────────┼────────────────────────┼──────────────────────────────────────────────────────────────┤
│ libudev1                │ CVE-2023-50387 │          │ fixed        │ 252.22-1~deb12u1        │ 252.23-1~deb12u1       │ bind9: KeyTrap - Extreme CPU consumption in DNSSEC validator │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-50387                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2023-50868 │          │              │                         │                        │ bind9: Preparing an NSEC3 closest encloser proof can exhaust │
│                         │                │          │              │                         │                        │ CPU resources                                                │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-50868                   │
├─────────────────────────┼────────────────┤          ├──────────────┼─────────────────────────┼────────────────────────┼──────────────────────────────────────────────────────────────┤
│ libxml2                 │ CVE-2024-25062 │          │ affected     │ 2.9.14+dfsg-1.3~deb12u1 │                        │ libxml2: use-after-free in XMLReader                         │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-25062                   │
├─────────────────────────┤                │          │              │                         ├────────────────────────┤                                                              │
│ libxml2-dev             │                │          │              │                         │                        │                                                              │
│                         │                │          │              │                         │                        │                                                              │
├─────────────────────────┼────────────────┼──────────┼──────────────┼─────────────────────────┼────────────────────────┼──────────────────────────────────────────────────────────────┤
│ linux-libc-dev          │ CVE-2024-42154 │ CRITICAL │ fixed        │ 6.1.90-1                │ 6.1.98-1               │ kernel: tcp_metrics: validate source addr length             │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-42154                   │
│                         ├────────────────┼──────────┼──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2013-7445  │ HIGH     │ will_not_fix │                         │                        │ kernel: memory exhaustion via crafted Graphics Execution     │
│                         │                │          │              │                         │                        │ Manager (GEM) objects                                        │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2013-7445                    │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2019-19449 │          │ fix_deferred │                         │                        │ kernel: mounting a crafted f2fs filesystem image can lead to │
│                         │                │          │              │                         │                        │ slab-out-of-bounds read...                                   │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2019-19449                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2019-19814 │          │ affected     │                         │                        │ kernel: out-of-bounds write in __remove_dirty_segment in     │
│                         │                │          │              │                         │                        │ fs/f2fs/segment.c                                            │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2019-19814                   │
│                         ├────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2021-3847  │          │              │                         │                        │ kernel: low-privileged user privileges escalation            │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2021-3847                    │
│                         ├────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2021-3864  │          │              │                         │                        │ kernel: descendant's dumpable setting with certain SUID      │
│                         │                │          │              │                         │                        │ binaries                                                     │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2021-3864                    │
│                         ├────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2023-52452 │          │              │                         │                        │ kernel: bpf: Fix accesses to uninit stack slots              │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-52452                   │
│                         ├────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2023-52590 │          │              │                         │                        │ kernel: ocfs2: Avoid touching renamed directory if parent    │
│                         │                │          │              │                         │                        │ does not change                                              │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-52590                   │
│                         ├────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2023-52591 │          │              │                         │                        │ kernel: reiserfs: Avoid touching renamed directory if parent │
│                         │                │          │              │                         │                        │ does not change                                              │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-52591                   │
│                         ├────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2023-52596 │          │              │                         │                        │ kernel: sysctl: Fix out of bounds access for empty sysctl    │
│                         │                │          │              │                         │                        │ registers                                                    │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-52596                   │
│                         ├────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2023-52751 │          │              │                         │                        │ kernel: smb: client: fix use-after-free in                   │
│                         │                │          │              │                         │                        │ smb2_query_info_compound()                                   │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-52751                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2023-52760 │          │ fixed        │                         │ 6.1.99-1               │ kernel: gfs2: Fix slab-use-after-free in gfs2_qd_dealloc     │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-52760                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2023-52827 │          │ affected     │                         │                        │ kernel: wifi: ath12k: fix possible out-of-bound read in      │
│                         │                │          │              │                         │                        │ ath12k_htt_pull_ppdu_stats()                                 │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-52827                   │
│                         ├────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-21803 │          │              │                         │                        │ kernel: bluetooth: use-after-free vulnerability in           │
│                         │                │          │              │                         │                        │ af_bluetooth.c                                               │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-21803                   │
│                         ├────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-25742 │          │              │                         │                        │ hw: amd: Instruction raise #VC exception at exit             │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-25742                   │
│                         ├────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-25743 │          │              │                         │                        │ hw: amd: Instruction raise #VC exception at exit             │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-25743                   │
│                         ├────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-26669 │          │              │                         │                        │ kernel: net/sched: flower: Fix chain template offload        │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-26669                   │
│                         ├────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-26913 │          │              │                         │                        │ kernel: drm/amd/display: Fix dcn35 8k30 Underflow/Corruption │
│                         │                │          │              │                         │                        │ Issue                                                        │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-26913                   │
│                         ├────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-26930 │          │              │                         │                        │ kernel: scsi: qla2xxx: Fix double free of the ha-&gt;vp_map  │
│                         │                │          │              │                         │                        │ pointer                                                      │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-26930                   │
│                         ├────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-26952 │          │              │                         │                        │ kernel: ksmbd: fix potencial out-of-bounds when buffer       │
│                         │                │          │              │                         │                        │ offset is invalid                                            │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-26952                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-27397 │          │ fixed        │                         │ 6.1.99-1               │ kernel: netfilter: nf_tables: use timestamp to check for set │
│                         │                │          │              │                         │                        │ element timeout                                              │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-27397                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-36013 │          │ affected     │                         │                        │ kernel: Bluetooth: L2CAP: Fix slab-use-after-free in         │
│                         │                │          │              │                         │                        │ l2cap_connect()                                              │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-36013                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-36883 │          │ fixed        │                         │ 6.1.94-1               │ kernel: net: fix out-of-bounds access in ops_init            │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-36883                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-36886 │          │              │                         │                        │ kernel: TIPC message reassembly use-after-free remote code   │
│                         │                │          │              │                         │                        │ execution vulnerability                                      │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-36886                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-36904 │          │              │                         │                        │ kernel: tcp: Use refcount_inc_not_zero() in                  │
│                         │                │          │              │                         │                        │ tcp_twsk_unique().                                           │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-36904                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-36946 │          │              │                         │                        │ kernel: phonet: fix rtm_phonet_notify() skb allocation       │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-36946                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-36960 │          │              │                         │                        │ kernel: drm/vmwgfx: Fix invalid reads in fence signaled      │
│                         │                │          │              │                         │                        │ events                                                       │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-36960                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-36971 │          │              │                         │                        │ kernel: net: kernel: UAF in network route management         │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-36971                   │
│                         ├────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-36978 │          │              │                         │ 6.1.99-1               │ kernel: net: sched: sch_multiq: fix possible OOB write in    │
│                         │                │          │              │                         │                        │ multiq_tune()                                                │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-36978                   │
│                         ├────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-36979 │          │              │                         │ 6.1.94-1               │ kernel: net: bridge: mst: fix vlan use-after-free            │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-36979                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-38538 │          │              │                         │                        │ kernel: net: bridge: xmit: make sure we have at least eth    │
│                         │                │          │              │                         │                        │ header...                                                    │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-38538                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-38545 │          │              │                         │                        │ kernel: RDMA/hns: Fix UAF for cq async event                 │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-38545                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-38552 │          │              │                         │                        │ kernel: drm/amd/display: Fix potential index out of bounds   │
│                         │                │          │              │                         │                        │ in color transformation function...                          │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-38552                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-38555 │          │              │                         │                        │ kernel: net/mlx5: Discard command completions in internal    │
│                         │                │          │              │                         │                        │ error                                                        │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-38555                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-38561 │          │              │                         │                        │ kernel: kunit: Fix kthread reference                         │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-38561                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-38570 │          │ affected     │                         │                        │ kernel: gfs2: Fix potential glock use-after-free on unmount  │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-38570                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-38577 │          │ fixed        │                         │ 6.1.94-1               │ kernel: rcu-tasks: Fix show_rcu_tasks_trace_gp_kthread       │
│                         │                │          │              │                         │                        │ buffer overflow                                              │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-38577                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-38581 │          │              │                         │                        │ kernel: drm/amdgpu/mes: fix use-after-free issue             │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-38581                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-38583 │          │              │                         │                        │ kernel: nilfs2: fix use-after-free of timer for log writer   │
│                         │                │          │              │                         │                        │ thread                                                       │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-38583                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-38667 │          │              │                         │                        │ kernel: riscv: prevent pt_regs corruption for secondary idle │
│                         │                │          │              │                         │                        │ threads                                                      │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-38667                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-39277 │          │              │                         │                        │ kernel: dma-mapping: benchmark: handle NUMA_NO_NODE          │
│                         │                │          │              │                         │                        │ correctly                                                    │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-39277                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-39463 │          │              │                         │                        │ kernel: 9p: add missing locking around taking dentry fid     │
│                         │                │          │              │                         │                        │ list                                                         │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-39463                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-39479 │          │ affected     │                         │                        │ kernel: drm/i915/hwmon: Get rid of devm                      │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-39479                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-39480 │          │ fixed        │                         │ 6.1.94-1               │ kernel: kdb: Fix buffer overflow during tab-complete         │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-39480                   │
│                         ├────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-39487 │          │              │                         │ 6.1.99-1               │ kernel: bonding: Fix out-of-bounds read in                   │
│                         │                │          │              │                         │                        │ bond_option_arp_ip_targets_set()                             │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-39487                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-39494 │          │              │                         │                        │ kernel: ima: Fix use-after-free on a dentry's dname.name     │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-39494                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-39495 │          │              │                         │                        │ kernel: greybus: Fix use-after-free bug in                   │
│                         │                │          │              │                         │                        │ gb_interface_release due to race condition                   │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-39495                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-39496 │          │              │                         │                        │ kernel: btrfs: zoned: fix use-after-free due to race with    │
│                         │                │          │              │                         │                        │ dev replace                                                  │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-39496                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-39508 │          │ affected     │                         │                        │ kernel: io_uring/io-wq: Use set_bit() and test_bit() at      │
│                         │                │          │              │                         │                        │ worker->flags                                                │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-39508                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-39510 │          │ fixed        │                         │ 6.1.99-1               │ kernel: cachefiles: fix slab-use-after-free in               │
│                         │                │          │              │                         │                        │ cachefiles_ondemand_daemon_read()                            │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-39510                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-40899 │          │              │                         │                        │ kernel: cachefiles: fix slab-use-after-free in               │
│                         │                │          │              │                         │                        │ cachefiles_ondemand_get_fd()                                 │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-40899                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-40902 │          │              │                         │                        │ kernel: jfs: xattr: fix buffer overflow for invalid xattr    │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-40902                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-40903 │          │              │                         │                        │ kernel: usb: typec: tcpm: fix use-after-free case in         │
│                         │                │          │              │                         │                        │ tcpm_register_source_caps                                    │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-40903                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-40906 │          │              │                         │                        │ kernel: net/mlx5: Always stop health timer during driver     │
│                         │                │          │              │                         │                        │ removal                                                      │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-40906                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-40954 │          │              │                         │                        │ kernel: net: do not leave a dangling sk pointer, when socket │
│                         │                │          │              │                         │                        │ creation...                                                  │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-40954                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-40956 │          │              │                         │                        │ kernel: dmaengine: idxd: Fix possible Use-After-Free in      │
│                         │                │          │              │                         │                        │ irq_process_work_list                                        │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-40956                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-40958 │          │              │                         │                        │ kernel: netns: Make get_net_ns() handle zero refcount net    │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-40958                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-40994 │          │              │                         │                        │ kernel: ptp: fix integer overflow in max_vclocks_store       │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-40994                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-40996 │          │              │                         │                        │ kernel: bpf: Avoid splat in pskb_pull_reason                 │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-40996                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-41000 │          │              │                         │                        │ kernel: block/ioctl: prefer different overflow check         │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-41000                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-41013 │          │ affected     │                         │                        │ kernel: xfs: don&#39;t walk off the end of a directory data  │
│                         │                │          │              │                         │                        │ block...                                                     │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-41013                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-41030 │          │ fixed        │                         │ 6.1.106-1              │ kernel: ksmbd: discard write access to the directory open    │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-41030                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-41046 │          │              │                         │                        │ kernel: net: ethernet: lantiq_etop: fix double free in       │
│                         │                │          │              │                         │                        │ detach                                                       │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-41046                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-41049 │          │              │                         │                        │ kernel: filelock: fix potential use-after-free in            │
│                         │                │          │              │                         │                        │ posix_lock_inode                                             │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-41049                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-41057 │          │              │                         │                        │ kernel: cachefiles: fix slab-use-after-free in               │
│                         │                │          │              │                         │                        │ cachefiles_withdraw_cookie()                                 │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-41057                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-41058 │          │              │                         │                        │ kernel: cachefiles: fix slab-use-after-free in               │
│                         │                │          │              │                         │                        │ fscache_withdraw_volume()                                    │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-41058                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-41061 │          │ affected     │                         │                        │ kernel: drm/amd/display: Fix array-index-out-of-bounds in    │
│                         │                │          │              │                         │                        │ dml2/FCLKChangeSupport                                       │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-41061                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-41070 │          │ fixed        │                         │ 6.1.106-1              │ kernel: KVM: PPC: Book3S HV: Prevent UAF in                  │
│                         │                │          │              │                         │                        │ kvm_spapr_tce_attach_iommu_group()                           │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-41070                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-41071 │          │ affected     │                         │                        │ kernel: wifi: mac80211: Avoid address calculations via out   │
│                         │                │          │              │                         │                        │ of bounds array indexing...                                  │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-41071                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-41073 │          │ fixed        │                         │ 6.1.106-1              │ In the Linux kernel, the following vulnerability has been    │
│                         │                │          │              │                         │                        │ resolved: n...                                               │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-41073                   │
│                         ├────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-41087 │          │              │                         │ 6.1.98-1               │ kernel: ata: libata-core: Fix double free on error           │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-41087                   │
│                         ├────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-41090 │          │              │                         │ 6.1.106-1              │ kernel: virtio-net: tap: mlx5_core short frame denial of     │
│                         │                │          │              │                         │                        │ service                                                      │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-41090                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-41091 │          │              │                         │                        │ kernel: virtio-net: tun: mlx5_core short frame denial of     │
│                         │                │          │              │                         │                        │ service                                                      │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-41091                   │
│                         ├────────────────┤          │              │                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-41092 │          │              │                         │ 6.1.98-1               │ kernel: drm/i915/gt: Fix potential UAF by revoke of fence    │
│                         │                │          │              │                         │                        │ registers                                                    │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-41092                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-41096 │          │ affected     │                         │                        │ kernel: PCI/MSI: Fix UAF in msi_capability_init              │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-41096                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-42093 │          │ fixed        │                         │ 6.1.98-1               │ kernel: net/dpaa2: Avoid explicit cpumask var allocation on  │
│                         │                │          │              │                         │                        │ stack                                                        │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-42093                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-42094 │          │              │                         │                        │ kernel: net/iucv: Avoid explicit cpumask var allocation on   │
│                         │                │          │              │                         │                        │ stack                                                        │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-42094                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-42104 │          │              │                         │                        │ kernel: nilfs2: add missing check for inode numbers on       │
│                         │                │          │              │                         │                        │ directory entries                                            │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-42104                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-42159 │          │              │                         │                        │ kernel: scsi: mpi3mr: Sanitise num_phys                      │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-42159                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-42160 │          │              │                         │                        │ kernel: f2fs: check validation of fault attrs in             │
│                         │                │          │              │                         │                        │ f2fs_build_fault_attr()                                      │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-42160                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-42161 │          │              │                         │                        │ kernel: bpf: Avoid uninitialized value in                    │
│                         │                │          │              │                         │                        │ BPF_CORE_READ_BITFIELD                                       │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-42161                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-42162 │          │ affected     │                         │                        │ kernel: gve: Account for stopped queues when reading NIC     │
│                         │                │          │              │                         │                        │ stats                                                        │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-42162                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-42224 │          │ fixed        │                         │ 6.1.98-1               │ kernel: net: dsa: mv88e6xxx: Correct check for empty list    │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-42224                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-42225 │          │              │                         │                        │ kernel: wifi: mt76: replace skb_put with skb_put_zero        │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-42225                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-42228 │          │ affected     │                         │                        │ kernel: drm/amdgpu: Using uninitialized value *size when     │
│                         │                │          │              │                         │                        │ calling amdgpu_vce_cs_reloc                                  │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-42228                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-42271 │          │ fixed        │                         │ 6.1.106-1              │ kernel: net/iucv: fix use after free in iucv_sock_close()    │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-42271                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-42284 │          │              │                         │                        │ kernel: tipc: Return non-zero value from tipc_udp_addr2str() │
│                         │                │          │              │                         │                        │ on error                                                     │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-42284                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-42285 │          │              │                         │                        │ kernel: RDMA/iwcm: Fix a use-after-free related to           │
│                         │                │          │              │                         │                        │ destroying CM IDs                                            │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-42285                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-42301 │          │              │                         │                        │ kernel: dev/parport: fix the array out-of-bounds risk        │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-42301                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-42302 │          │              │                         │                        │ kernel: PCI/DPC: Fix use-after-free on concurrent DPC and    │
│                         │                │          │              │                         │                        │ hot-removal                                                  │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-42302                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-42313 │          │              │                         │                        │ kernel: media: venus: fix use after free in vdec_close       │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-42313                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-42314 │          │ affected     │                         │                        │ kernel: btrfs: fix extent map use-after-free when adding     │
│                         │                │          │              │                         │                        │ pages to compressed bio...                                   │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-42314                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-43858 │          │ fixed        │                         │ 6.1.106-1              │ kernel: jfs: Fix array-index-out-of-bounds in diFree         │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-43858                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-43900 │          │              │                         │                        │ kernel: media: xc2028: avoid use-after-free in               │
│                         │                │          │              │                         │                        │ load_firmware_cb()                                           │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-43900                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-44934 │          │              │                         │                        │ kernel: net: bridge: mcast: wait for previous gc cycles when │
│                         │                │          │              │                         │                        │ removing port...                                             │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-44934                   │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-44942 │          │ affected     │                         │                        │ kernel: f2fs: fix to do sanity check on F2FS_INLINE_DATA     │
│                         │                │          │              │                         │                        │ flag in inode...                                             │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-44942                   │
├─────────────────────────┼────────────────┤          ├──────────────┼─────────────────────────┼────────────────────────┼──────────────────────────────────────────────────────────────┤
│ openssh-client          │ CVE-2024-6387  │          │ fixed        │ 1:9.2p1-2+deb12u2       │ 1:9.2p1-2+deb12u3      │ openssh: regreSSHion - race condition in SSH allows RCE/DoS  │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-6387                    │
├─────────────────────────┼────────────────┤          ├──────────────┼─────────────────────────┼────────────────────────┼──────────────────────────────────────────────────────────────┤
│ perl                    │ CVE-2023-31484 │          │ affected     │ 5.36.0-7+deb12u1        │                        │ perl: CPAN.pm does not verify TLS certificates when          │
│                         │                │          │              │                         │                        │ downloading distributions over HTTPS...                      │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-31484                   │
├─────────────────────────┤                │          │              │                         ├────────────────────────┤                                                              │
│ perl-base               │                │          │              │                         │                        │                                                              │
│                         │                │          │              │                         │                        │                                                              │
│                         │                │          │              │                         │                        │                                                              │
├─────────────────────────┤                │          │              │                         ├────────────────────────┤                                                              │
│ perl-modules-5.36       │                │          │              │                         │                        │                                                              │
│                         │                │          │              │                         │                        │                                                              │
│                         │                │          │              │                         │                        │                                                              │
├─────────────────────────┼────────────────┤          ├──────────────┼─────────────────────────┼────────────────────────┼──────────────────────────────────────────────────────────────┤
│ python3.11              │ CVE-2023-24329 │          │ fixed        │ 3.11.2-6                │ 3.11.2-6+deb12u2       │ python: urllib.parse url blocklisting bypass                 │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-24329                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2023-41105 │          │              │                         │                        │ python: file path truncation at \0 characters                │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-41105                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2023-6597  │          │              │                         │                        │ python: Path traversal on tempfile.TemporaryDirectory        │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-6597                    │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-7592  │          │ fix_deferred │                         │                        │ cpython: python: Uncontrolled CPU resource consumption when  │
│                         │                │          │              │                         │                        │ in http.cookies module                                       │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-7592                    │
├─────────────────────────┼────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│ python3.11-minimal      │ CVE-2023-24329 │          │ fixed        │                         │ 3.11.2-6+deb12u2       │ python: urllib.parse url blocklisting bypass                 │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-24329                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2023-41105 │          │              │                         │                        │ python: file path truncation at \0 characters                │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-41105                   │
│                         ├────────────────┤          │              │                         │                        ├──────────────────────────────────────────────────────────────┤
│                         │ CVE-2023-6597  │          │              │                         │                        │ python: Path traversal on tempfile.TemporaryDirectory        │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-6597                    │
│                         ├────────────────┤          ├──────────────┤                         ├────────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2024-7592  │          │ fix_deferred │                         │                        │ cpython: python: Uncontrolled CPU resource consumption when  │
│                         │                │          │              │                         │                        │ in http.cookies module                                       │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-7592                    │
├─────────────────────────┼────────────────┼──────────┼──────────────┼─────────────────────────┼────────────────────────┼──────────────────────────────────────────────────────────────┤
│ wget                    │ CVE-2024-38428 │ CRITICAL │ affected     │ 1.21.3-1+b1             │                        │ wget: Misinterpretation of input may lead to improper        │
│                         │                │          │              │                         │                        │ behavior                                                     │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2024-38428                   │
├─────────────────────────┼────────────────┤          ├──────────────┼─────────────────────────┼────────────────────────┼──────────────────────────────────────────────────────────────┤
│ zlib1g                  │ CVE-2023-45853 │          │ will_not_fix │ 1:1.2.13.dfsg-1         │                        │ zlib: integer overflow and resultant heap-based buffer       │
│                         │                │          │              │                         │                        │ overflow in zipOpenNewFileInZip4_6                           │
│                         │                │          │              │                         │                        │ https://avd.aquasec.com/nvd/cve-2023-45853                   │
├─────────────────────────┤                │          │              │                         ├────────────────────────┤                                                              │
│ zlib1g-dev              │                │          │              │                         │                        │                                                              │
│                         │                │          │              │                         │                        │                                                              │
│                         │                │          │              │                         │                        │                                                              │
└─────────────────────────┴────────────────┴──────────┴──────────────┴─────────────────────────┴────────────────────────┴──────────────────────────────────────────────────────────────┘
2024-09-03T09:01:33+09:00	INFO	Table result includes only package filenames. Use '--format json' option to get the full path to the package file.

Node.js (node-pkg)

Total: 3 (HIGH: 3, CRITICAL: 0)

┌───────────────────────────┬────────────────┬──────────┬────────┬───────────────────┬───────────────┬────────────────────────────────────────────────────────┐
│          Library          │ Vulnerability  │ Severity │ Status │ Installed Version │ Fixed Version │                         Title                          │
├───────────────────────────┼────────────────┼──────────┼────────┼───────────────────┼───────────────┼────────────────────────────────────────────────────────┤
│ axios (package.json)      │ CVE-2024-39338 │ HIGH     │ fixed  │ 1.7.0             │ 1.7.4         │ axios: axios: Server-Side Request Forgery              │
│                           │                │          │        │                   │               │ https://avd.aquasec.com/nvd/cve-2024-39338             │
├───────────────────────────┼────────────────┤          │        ├───────────────────┼───────────────┼────────────────────────────────────────────────────────┤
│ braces (package.json)     │ CVE-2024-4068  │          │        │ 3.0.2             │ 3.0.3         │ braces: fails to limit the number of characters it can │
│                           │                │          │        │                   │               │ handle                                                 │
│                           │                │          │        │                   │               │ https://avd.aquasec.com/nvd/cve-2024-4068              │
├───────────────────────────┼────────────────┤          │        ├───────────────────┼───────────────┼────────────────────────────────────────────────────────┤
│ fast-loops (package.json) │ CVE-2024-39008 │          │        │ 1.1.3             │ 1.1.4         │ fast-loops: prototype pollution via objectMergeDeep    │
│                           │                │          │        │                   │               │ https://avd.aquasec.com/nvd/cve-2024-39008             │
```