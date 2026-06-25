# CyFun 2025 Compliance Audit, BeCode Corp. Secure Network Design

[![Framework](https://img.shields.io/badge/framework-CyFun%202025%20Important-1f6feb.svg)](https://ccb.belgium.be/en/cyberfundamentals-framework)
[![Regulation](https://img.shields.io/badge/regulation-NIS2%20%7C%20GDPR-orange.svg)](#frameworks-12)
[![Standards](https://img.shields.io/badge/standards-ISO%2027001%20%7C%20NIST%20800--53%20%7C%20CIS%20v8.1-red.svg)](#frameworks-12)
[![Maturity](https://img.shields.io/badge/CyFun%20maturity-1.13%20%2F%203-critical.svg)](#cyfun-maturity-result)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Johan--Emmanuel%20Hatchi-0A66C2?logo=linkedin&logoColor=white)](https://www.linkedin.com/in/johan-emmanuel-hatchi/)

Hybrid multi-framework cybersecurity compliance audit of an enterprise Cisco network design,
assessed against the CyberFundamentals Framework 2025 (Important level) issued by the
Centre for Cybersecurity Belgium (CCB).

The anonymized audit report is published in `report/`, and the board-level presentation of the audit
in `presentation/` (PDF). See the Confidentiality section for what is intentionally
redacted or not redistributed.

## Operational notice

Publication authorized by BeCode lab coach (Thomas B.) on 2026-05-17 for portfolio use. BeCode Corp. is a
fictitious organization and the audited network is a simulated Cisco Packet Tracer lab, so the
anonymized deliverables are shareable (TLP:CLEAR). See the Confidentiality and data minimisation
section for what is redacted or kept local.

## How to read this repository

| If you are a... | Start with | Time |
| --- | --- | --- |
| Recruiter or hiring manager | This README: Key result, CyFun maturity, Top 3 critical risks | 5 min |
| GRC or compliance reader | The anonymized report in `report/`, plus the Frameworks and Findings sections below | 25 min |
| Auditor or technical reviewer | The full report in `report/` and the board presentation in `presentation/` | 40 min |

## Overview

This audit evaluates the compliance and real security posture of a "Secure Network Design,
BeCode Corp." project. It is a hybrid audit: documentary analysis of the 44-page design
deliverable is combined with direct empirical verification on the associated Cisco Packet Tracer
file via CLI, so that documented claims are tested against the actual device configurations.

## Key result

Overall security posture assessed as Critical. 18 findings reported, distributed as
5 Critical, 10 High, 2 Medium, 1 Low (per executive summary).

The headline finding is organizational rather than technical: a systematic disconnect between
documented controls and their actual implementation. Four findings share this root cause
(F-10, F-14, F-17, F-18), which points to a missing final review process more severe than any
single technical gap.

## CyFun maturity result

Measured total maturity: 1.13 against a target of 3 for the Important assurance level, scored with
the official CCB CyFun 2025 toolbox (completion date 20 February 2026). The Govern, Respond and
Recover functions sit at the 1.0 floor, consistent with the absence of a governance framework,
incident response plan and recovery mechanism (F-04, F-06, F-07). Protect is the least weak function.

## Top 3 critical risks

- F-17: Inter-VLAN ACLs defined but never applied on the L3-SW SVIs, segmentation is theoretical
- F-10: ASA 5506-X firewall left in factory configuration, privileged mode without password
- F-04: No centralized logging and no NTP, no ability to detect or notify within NIS2 deadlines

## Scope and assurance level

- Audited deliverable: a Secure Network Design document (44 pages) and its Cisco Packet Tracer file
- Assurance level: CyFun Important, CIS references calibrated on Implementation Group 2 (IG2)
- Positioning: tertiary-sector SME or mid-sized organization (more than 50 employees)
- Out of scope: business processes, governance maturity, intrusive testing, endpoint and
  application audit, and services not simulated by Packet Tracer

## Frameworks (12)

Primary framework: CyFun 2025 (Important).

Secondary frameworks: NIS2 Belgian Act, GDPR, APD/GBA, ISO/IEC 27001:2022, ISO/IEC 27005:2022,
NIST SP 800-53 Rev. 5, SOC 2, Cyber Resilience Act, CIS Controls v8.1 (IG2),
CIS Cisco IOS Benchmark, MITRE ATT&CK.

Each finding cites 7 to 15 references on average, selected for legal traceability, audit defense,
technical actionability, and threat relevance.

## Methodology

1. Documentary analysis of the 44-page deliverable
2. CyFun scoring via the official CCB CyFun 2025 Toolbox across the 6 functions
   (Govern, Identify, Protect, Detect, Respond, Recover)
3. Direct empirical verification via CLI: show running-config, show interfaces trunk,
   show ip interface brief, show version, show nat, show access-lists, and related commands
4. Consolidation into 18 narrative findings with localized evidence (PDF page or CLI screenshot),
   risk analysis, multi-framework regulatory mapping, and MITRE ATT&CK technique mapping

## Findings

- F-01: Shared administrator secret across the entire scope
- F-02: No multi-factor authentication on privileged access
- F-03: No privilege segregation, single-level authentication model
- F-04: No centralization or correlation of security logs
- F-05: No detection capability (anti-malware, IDS/IPS, EDR)
- F-06: No backup or recovery mechanism
- F-07: No incident response plan
- F-08: No vulnerability management or patch management
- F-09: Undersized SSH cryptography (RSA 1024-bit keys)
- F-10: ASA 5506-X firewall in factory configuration, no authentication, no filtering
- F-11: Permissive trunk configuration on SW2, no VLAN restriction
- F-12: Printers not assigned to a dedicated VLAN, systemic flaw across SW1, SW2, SW3
- F-13: Native VLAN 1 not purged across trunks
- F-14: AAA protocol mismatch, TACACS+ clients vs RADIUS server
- F-15: AAA user base with trivial credentials (username equals password)
- F-16: Undocumented perimeter filtering and FTP in cleartext
- F-17: Inter-VLAN ACLs defined but not applied on L3-SW SVIs
- F-18: VTY lines 5 to 15 not hardened on SW1, SW2, SW3, Telnet access possible by default

## Remediation roadmap

- Quick wins (less than 1 week, low effort): around 25 configuration-level actions, immediately applicable
- Short term (1 to 3 months, medium effort): around 27 actions requiring standard tooling
  (syslog, antivirus, backup, incident response plan, corrected AAA)
- Long term (6 to 18 months, high effort): around 20 strategic actions
  (SIEM, PAM, MFA, BCP and DRP, vulnerability management program)

Indicative budget for short-term actions: 30,000 to 80,000 EUR depending on open source versus
commercial choices. Reaching CyFun Important level is realistic within 6 to 12 months.

## Repository layout

```
.
├── README.md
├── report/
│   └── CyFun-Audit-Report-public.pdf                     Anonymized audit report (public)
└── presentation/
    └── CyFun-Audit-Fictitious-Board-Presentation.pdf     Cleaned board presentation (public)
```

Kept local only (under a gitignored `_private/`, available on request): the source audit report
with real names, the editable board presentation (PPTX), the scored CyFun toolbox, and the audited
team's network design and Cisco Packet Tracer file.

## Confidentiality and data minimisation

The report published in `report/` is an anonymized version. Personal names that appeared as test
credentials inside the simulation have been removed from the text and redacted in the evidence
screenshots. The audited team's source files (the network design document and the Packet Tracer
simulation) and the scored CyFun workbook are not redistributed here. They are available on request. The board presentation in `presentation/` is the cleaned, publicly shareable version (educational marking, corrected severity tally, no third-party personal data).

## Team and attribution

Audit team: Zoltàn F., Johan-Emmanuel Hatchi, André P. Personal contribution: report writing and regulatory mapping.
The audited network design was produced by a separate BeCode student team and is referenced here
solely as the system under audit.

BeCode coach: Thomas B.

## Disclaimer

This is an educational project produced during the BeCode Brussels Blue and Red Team bootcamp.
BeCode Corp. is a fictitious organization and the audited network is a simulated Cisco Packet
Tracer lab. The report is written in the format of a real compliance audit for training and
portfolio purposes only. No real organization, system, or personal data is involved, which is why
it is published publicly (TLP:CLEAR).

## About

Johan-Emmanuel Hatchi, junior cybersecurity analyst (BeCode Brussels, Blue and Red Team).

- LinkedIn: https://www.linkedin.com/in/johan-emmanuel-hatchi/
- GitHub: https://github.com/Jhatchi
