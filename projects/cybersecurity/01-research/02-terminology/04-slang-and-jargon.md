# Cybersecurity Slang and Jargon

A practical guide to the informal language, acronyms, and phrases commonly used in the cybersecurity community. Understanding this terminology is essential for effective communication in security operations.

## Table of Contents

1. [Common Acronyms in Daily Work](#common-acronyms-in-daily-work)
2. [Hacker Culture Terminology](#hacker-culture-terminology)
3. [Security Community Phrases](#security-community-phrases)
4. [Threat Intelligence Sharing Terms](#threat-intelligence-sharing-terms)
5. [Operations Slang](#operations-slang)

---

## Common Acronyms in Daily Work

### Detection and Response Acronyms

| Acronym | Full Form | Description |
|---------|-----------|-------------|
| **AV** | Antivirus | Traditional malware detection software |
| **EDR** | Endpoint Detection and Response | Advanced endpoint monitoring and response |
| **XDR** | Extended Detection and Response | Cross-layer detection and response |
| **NDR** | Network Detection and Response | Network traffic analysis and response |
| **MDR** | Managed Detection and Response | Outsourced security monitoring service |
| **SIEM** | Security Information and Event Management | Log aggregation and correlation platform |
| **SOAR** | Security Orchestration, Automation and Response | Automated security workflow platform |
| **DLP** | Data Loss Prevention | Controls to prevent data exfiltration |
| **IAM** | Identity and Access Management | User identity and permissions management |
| **PAM** | Privileged Access Management | Controls for administrative accounts |
| **MFA** | Multi-Factor Authentication | Authentication requiring multiple proofs |
| **SSO** | Single Sign-On | One login for multiple applications |
| **WAF** | Web Application Firewall | Protection for web applications |
| **CASB** | Cloud Access Security Broker | Cloud security controls |
| **ZTNA** | Zero Trust Network Access | Access based on continuous verification |

### Threat and Vulnerability Acronyms

| Acronym | Full Form | Description |
|---------|-----------|-------------|
| **APT** | Advanced Persistent Threat | Sophisticated, long-term threat actor |
| **CVE** | Common Vulnerabilities and Exposures | Unique vulnerability identifier |
| **CVSS** | Common Vulnerability Scoring System | Vulnerability severity rating |
| **IOC** | Indicator of Compromise | Evidence of breach |
| **IOA** | Indicator of Attack | Evidence of ongoing attack |
| **TTP** | Tactics, Techniques, and Procedures | Adversary behavioral patterns |
| **C2/C&C** | Command and Control | Attacker communication infrastructure |
| **RAT** | Remote Access Trojan | Malware enabling remote control |
| **RCE** | Remote Code Execution | Vulnerability allowing remote code execution |
| **LPE** | Local Privilege Escalation | Vulnerability allowing elevated permissions |
| **SQLi** | SQL Injection | Database attack via malicious SQL |
| **XSS** | Cross-Site Scripting | Web attack injecting malicious scripts |

### Operations and Process Acronyms

| Acronym | Full Form | Description |
|---------|-----------|-------------|
| **SOC** | Security Operations Center | Security monitoring team/facility |
| **NOC** | Network Operations Center | Network monitoring team/facility |
| **IR** | Incident Response | Handling security incidents |
| **DFIR** | Digital Forensics and Incident Response | Forensics combined with IR |
| **CTI** | Cyber Threat Intelligence | Information about threats |
| **OSINT** | Open Source Intelligence | Publicly available information |
| **HUMINT** | Human Intelligence | Intelligence from human sources |
| **SIGINT** | Signals Intelligence | Intelligence from communications |
| **TI** | Threat Intelligence | Threat information and analysis |
| **VA** | Vulnerability Assessment | Identifying vulnerabilities |
| **PT** | Penetration Testing | Authorized attack simulation |
| **RoE** | Rules of Engagement | Exercise boundaries and rules |

### Compliance and Governance Acronyms

| Acronym | Full Form | Description |
|---------|-----------|-------------|
| **GRC** | Governance, Risk, and Compliance | Combined governance approach |
| **DPO** | Data Protection Officer | Privacy compliance officer |
| **CISO** | Chief Information Security Officer | Security executive |
| **BCP** | Business Continuity Plan | Plan for maintaining operations |
| **DRP** | Disaster Recovery Plan | IT recovery plan |
| **RTO** | Recovery Time Objective | Maximum acceptable downtime |
| **RPO** | Recovery Point Objective | Maximum acceptable data loss |
| **DPIA** | Data Protection Impact Assessment | Privacy risk assessment |
| **SLA** | Service Level Agreement | Contracted performance standards |

---

## Hacker Culture Terminology

### Hat Colors (Hacker Types)

#### Black Hat
A hacker who breaks into systems for malicious purposes - theft, destruction, or other criminal activities.

**Characteristics**:
- Operates illegally
- Profit or destruction motivated
- May sell exploits on dark web
- No authorization for activities

**Use in context**: "The breach was attributed to black hat hackers selling stolen data on dark web forums."

#### White Hat (Ethical Hacker)
A security professional who hacks with permission to find vulnerabilities before malicious actors do.

**Characteristics**:
- Authorized testing only
- Follows rules of engagement
- Reports findings to organizations
- Helps improve security

**Use in context**: "Our white hat team found a critical vulnerability during the authorized pentest."

#### Gray Hat
A hacker who operates between white and black hat, sometimes breaking into systems without permission but without malicious intent, often to report vulnerabilities.

**Characteristics**:
- May operate without authorization
- No malicious intent
- Sometimes reports findings
- Legal ambiguity

**Use in context**: "A gray hat disclosed the vulnerability publicly after the vendor ignored their report."

#### Script Kiddie
A derogatory term for an unsophisticated attacker who uses existing tools and scripts without understanding how they work.

**Characteristics**:
- Uses others' tools
- Limited technical knowledge
- Often causes unintended damage
- Easy to detect

**Use in context**: "The attack pattern suggests script kiddies using automated tools rather than a sophisticated actor."

#### Hacktivist
A hacker motivated by political or social causes rather than financial gain.

**Examples**: Anonymous, various activist groups

**Use in context**: "Hacktivists defaced the website with political messages."

### Attack-Related Slang

#### Pwn (Owned)
To successfully compromise or take control of a system. Pronounced "own" - derived from a typo of "own."

**Use in context**: "The attacker completely pwned the domain controller."

#### Root
The highest level of access on Unix/Linux systems. "Getting root" means achieving full administrative access.

**Use in context**: "They exploited the vulnerability to get root on the database server."

#### Shell
Command-line access to a system. Getting a "shell" means establishing remote command execution.

**Types**:
- **Reverse shell**: Target connects back to attacker
- **Bind shell**: Attacker connects to target
- **Web shell**: Shell access through web interface

**Use in context**: "The exploit delivered a reverse shell to our C2 server."

#### Payload
The malicious code delivered and executed after exploiting a vulnerability.

**Use in context**: "The payload established persistence and began exfiltrating data."

#### Backdoor
A method of bypassing normal authentication to maintain unauthorized access.

**Use in context**: "The malware installed a backdoor for persistent access."

#### Drop
To place malware or tools on a compromised system.

**Use in context**: "After gaining access, the attacker dropped additional tools for lateral movement."

#### Exfil (Exfiltration)
The unauthorized removal of data from a network.

**Use in context**: "We detected exfil of customer data to an external IP."

#### Pivot
Using a compromised system as a launching point to attack other systems.

**Use in context**: "They pivoted through the web server to reach the internal database."

#### Pop (Pop a Box/Shell)
To successfully exploit and gain access to a system.

**Use in context**: "We popped the external web server within the first hour."

### Vulnerability and Exploit Terms

#### Zero-Day (0day)
A previously unknown vulnerability for which no patch exists.

**Use in context**: "The attacker used a zero-day in the email server."

#### N-Day
A known vulnerability that has been disclosed but may not be patched everywhere.

**Use in context**: "They exploited an n-day that had been patched months ago - the target just hadn't updated."

#### Weaponized
An exploit that has been refined for reliable use in attacks.

**Use in context**: "The proof-of-concept was weaponized within 48 hours of disclosure."

#### Burn
When a vulnerability, exploit, or technique becomes known and therefore less useful.

**Use in context**: "Once the security vendor published the IOCs, the C2 infrastructure was burned."

#### Spray and Pray
Attacking many targets indiscriminately hoping some succeed.

**Use in context**: "It was a spray and pray phishing campaign rather than targeted spear phishing."

### Social Engineering Terms

#### Phishing
Fraudulent attempts to obtain sensitive information by impersonating trustworthy entities via email.

#### Spear Phishing
Targeted phishing aimed at specific individuals or organizations.

#### Whaling
Phishing specifically targeting high-profile executives (the "big fish").

#### Vishing
Voice phishing - social engineering over phone calls.

#### Smishing
SMS phishing - social engineering via text messages.

#### Pretexting
Creating a fabricated scenario to manipulate targets into providing information.

**Use in context**: "The attacker used pretexting, claiming to be from IT support needing password verification."

---

## Security Community Phrases

### Common Expressions

#### "Defense in Depth"
A layered security approach where multiple controls protect assets, so if one fails, others remain.

**Use in context**: "Defense in depth means even if they bypass the firewall, they still face EDR, network segmentation, and encryption."

#### "Assume Breach"
A security mindset that assumes attackers have already compromised the network, driving proactive threat hunting and detection.

**Use in context**: "We operate with an assume breach mentality - hunting for threats rather than assuming we're secure."

#### "Trust but Verify"
Traditional approach of trusting users/systems within the network perimeter while verifying suspicious activity.

**Contrast**: Zero Trust ("Never trust, always verify")

#### "Zero Trust"
Security model that requires strict verification for everyone and everything, regardless of location or prior authentication.

**Principle**: "Never trust, always verify"

**Use in context**: "Our zero trust architecture requires re-authentication even for internal traffic."

#### "Crown Jewels"
The organization's most critical assets that require the highest protection.

**Examples**: Customer database, intellectual property, financial systems

**Use in context**: "The red team's objective was to reach the crown jewels - the customer PII database."

#### "Low-Hanging Fruit"
Easy-to-exploit vulnerabilities that attackers typically target first.

**Examples**: Default passwords, unpatched systems, open ports

**Use in context**: "We addressed the low-hanging fruit first - default credentials and missing patches."

#### "Attack Surface"
The sum of all possible entry points where an attacker could gain access.

**Use in context**: "Moving to cloud expanded our attack surface significantly."

#### "Blast Radius"
The extent of damage or impact if a system or account is compromised.

**Use in context**: "We limited the blast radius by segmenting the development environment."

#### "Kill Chain"
The sequence of steps in a cyberattack, from reconnaissance to objectives completion.

**Lockheed Martin Cyber Kill Chain**:
1. Reconnaissance
2. Weaponization
3. Delivery
4. Exploitation
5. Installation
6. Command and Control
7. Actions on Objectives

**Use in context**: "We broke the kill chain at the delivery stage by blocking the malicious email."

#### "Left of Boom"
Prevention activities that happen before an attack succeeds (the "boom").

**Use in context**: "Our threat hunting program focuses on left of boom - finding attackers before they cause damage."

#### "Right of Boom"
Response activities after an attack has occurred.

**Use in context**: "Incident response is right of boom - dealing with the aftermath."

### SOC and Operations Phrases

#### "Alert Fatigue"
The overwhelming of analysts with too many alerts, leading to missed real threats.

**Use in context**: "Alert fatigue caused them to miss the critical alert buried in noise."

#### "False Positive"
An alert that incorrectly indicates a threat when none exists.

**Use in context**: "After tuning, we reduced false positives by 80%."

#### "True Positive"
An alert that correctly identifies actual malicious activity.

#### "False Negative"
A missed detection - malicious activity that generated no alert.

**Use in context**: "The false negative allowed the attacker to remain undetected for months."

#### "Noise"
Irrelevant alerts or data that obscure actual threats.

**Use in context**: "We need to reduce the noise in our SIEM to focus on real threats."

#### "Signal"
Meaningful indicators of actual security events amid the noise.

**Use in context**: "The signal-to-noise ratio improved after we tuned our detection rules."

#### "Dwell Time"
How long an attacker remains undetected in the environment.

**Use in context**: "Industry average dwell time is still over 200 days."

#### "Mean Time to Detect" (MTTD)
Average time from attack initiation to detection.

#### "Mean Time to Respond" (MTTR)
Average time from detection to response initiation.

#### "Triage"
Initial assessment and prioritization of alerts or incidents.

**Use in context**: "Tier 1 handles triage - escalating confirmed incidents to Tier 2."

### Red Team/Pentest Phrases

#### "Get a Foothold"
Establish initial access to a target network.

**Use in context**: "We got a foothold through a vulnerable web application."

#### "Move Laterally"
Expand access from one system to others within the network.

**Use in context**: "After initial compromise, they moved laterally using stolen credentials."

#### "Escalate Privileges"
Gain higher-level permissions than currently held.

**Use in context**: "We escalated privileges from user to domain admin within two hours."

#### "Persist"
Establish mechanisms to maintain access after initial compromise.

**Use in context**: "They persisted using scheduled tasks and registry run keys."

#### "Land and Expand"
The strategy of gaining initial access (land) then expanding privileges and lateral movement (expand).

**Use in context**: "The APT used a land and expand approach over several months."

#### "Living off the Land" (LotL)
Using legitimate tools already present in the environment rather than custom malware.

**Examples**: PowerShell, WMI, PsExec, certutil

**Use in context**: "The attacker was living off the land, using only built-in Windows tools to avoid detection."

---

## Threat Intelligence Sharing Terms

### Threat Information Sharing

#### TLP (Traffic Light Protocol)
A system for classifying sensitive information and guiding its distribution.

| Color | Description | Sharing |
|-------|-------------|---------|
| **TLP:RED** | Personal risk | Named recipients only |
| **TLP:AMBER** | Limited disclosure | Organization only |
| **TLP:AMBER+STRICT** | More restrictive amber | Organization, need-to-know |
| **TLP:GREEN** | Community wide | Cybersecurity community |
| **TLP:CLEAR** | Public | No restrictions |

**Use in context**: "This threat report is TLP:AMBER - share only within our organization."

#### STIX (Structured Threat Information Expression)
A standardized language and format for sharing cyber threat intelligence.

**Use in context**: "We export our IOCs in STIX format for sharing with partners."

#### TAXII (Trusted Automated Exchange of Intelligence Information)
A protocol for exchanging threat intelligence in STIX format.

**Use in context**: "Our TI platform pulls threat feeds via TAXII."

#### MISP (Malware Information Sharing Platform)
An open-source threat intelligence platform for sharing, storing, and correlating IOCs.

**Use in context**: "We contribute our findings to our sector's MISP instance."

### Intelligence Types and Sources

#### OSINT (Open Source Intelligence)
Intelligence gathered from publicly available sources.

**Sources**: Social media, websites, news, public records, job postings

**Use in context**: "OSINT revealed the target company uses a specific VPN vendor."

#### HUMINT (Human Intelligence)
Intelligence gathered from human sources.

**Examples**: Insider information, informants, social engineering results

#### SIGINT (Signals Intelligence)
Intelligence gathered from electronic signals and communications.

#### Technical Intelligence
Intelligence derived from technical analysis of malware, infrastructure, and attack tools.

### Sharing Communities

#### ISAC (Information Sharing and Analysis Center)
Sector-specific organizations for sharing threat information.

**Examples**:
- FS-ISAC (Financial Services)
- H-ISAC (Healthcare)
- MS-ISAC (Multi-State)
- Auto-ISAC (Automotive)

**Use in context**: "The FS-ISAC alert warned of new banking trojans targeting our sector."

#### CERT/CSIRT
National or organizational computer emergency response teams.

**Examples**: US-CERT, SingCERT, JPCERT

### Attribution Terms

#### Attribution
Identifying the threat actor responsible for an attack.

**Challenges**: False flags, shared tools, proxy infrastructure

**Use in context**: "Attribution to a nation-state requires high-confidence intelligence."

#### False Flag
Techniques used by attackers to mislead attribution, making attacks appear to come from a different actor.

**Use in context**: "The malware contained Russian strings, but analysis suggests false flags."

#### APT Naming
Different security vendors use different naming conventions for threat groups.

**Examples** (same group, different names):
| Mandiant | CrowdStrike | Microsoft |
|----------|-------------|-----------|
| APT28 | Fancy Bear | STRONTIUM |
| APT29 | Cozy Bear | NOBELIUM |
| APT1 | Comment Panda | - |

**Use in context**: "APT29 - also known as Cozy Bear - was attributed to the supply chain attack."

---

## Operations Slang

### Analyst Slang

#### "In the Wild"
When malware or exploits are observed actively being used in real attacks.

**Use in context**: "The zero-day is now being exploited in the wild."

#### "Commodity Malware"
Widely available, easily obtained malware used by many different actors.

**Contrast**: Custom malware developed for specific campaigns

**Use in context**: "They used commodity malware - nothing sophisticated."

#### "Spray and Pray"
Attacking many targets indiscriminately, hoping some will be vulnerable.

**Use in context**: "The campaign was spray and pray - mass phishing to random addresses."

#### "Watering Hole"
Compromising websites frequented by the target group to infect them.

**Use in context**: "The watering hole attack targeted the industry association website."

#### "Drive-by Download"
Malware automatically downloaded when visiting a compromised website.

**Use in context**: "The compromised ad network delivered drive-by downloads to visitors."

#### "Island Hopping"
Attacking less-secure partners/suppliers to reach the primary target.

**Use in context**: "The attackers used island hopping through our managed service provider."

#### "Smash and Grab"
Quick attacks focused on immediate data theft rather than persistent access.

**Use in context**: "It was a smash and grab - they stole what they could and left."

### Infrastructure Terms

#### "Bulletproof Hosting"
Hosting providers that ignore abuse complaints and legal requests.

**Use in context**: "The C2 infrastructure was on bulletproof hosting in an uncooperative jurisdiction."

#### "Sinkholes"
Redirecting malicious traffic to controlled servers for analysis or disruption.

**Use in context**: "We sinkholed the botnet's C2 domain to disrupt operations."

#### "Fast Flux"
Rapidly changing DNS records to evade blocking and takedowns.

**Use in context**: "The C2 domain used fast flux with hundreds of IPs rotating every few minutes."

#### "Domain Fronting"
Using legitimate cloud services as proxies to hide C2 traffic.

**Use in context**: "The malware used domain fronting through a major CDN to evade detection."

### Data and Underground Terms

#### "Fullz"
Complete packages of stolen personal information (name, SSN, DOB, address, etc.) sold on dark web markets.

**Use in context**: "Fullz from the breach were selling for $50 each on dark web forums."

#### "Dumps"
Stolen credit card data from magnetic stripe.

**Use in context**: "The POS malware collected dumps from thousands of cards."

#### "Dark Web"
Hidden internet services accessible through special software (Tor), often hosting illegal marketplaces.

**Use in context**: "The stolen credentials appeared for sale on dark web forums."

#### "Underground Forums"
Online communities where cybercriminals share techniques, sell data, and coordinate activities.

#### "Crypter"
Software that encrypts malware to evade antivirus detection.

**Use in context**: "They used a FUD crypter to bypass AV detection." (FUD = Fully Undetectable)

### Response and Recovery Terms

#### "Nuke from Orbit"
Completely wiping and rebuilding compromised systems rather than attempting cleanup.

**Origin**: "It's the only way to be sure" (Aliens movie reference)

**Use in context**: "Given the rootkit, we decided to nuke from orbit rather than attempt remediation."

#### "Burn Down"
Systematically destroying and rebuilding compromised infrastructure.

**Use in context**: "We had to burn down the entire AD environment to ensure complete eradication."

#### "Rip and Replace"
Removing compromised systems/software and replacing with new.

**Use in context**: "The compromised firewalls were rip and replace."

#### "Scorched Earth"
Aggressive response that may impact operations to ensure threat elimination.

**Use in context**: "We went scorched earth - reset every password and rebuilt every domain controller."

---

## Pronunciation Guide

| Term | Pronunciation | Notes |
|------|---------------|-------|
| SIEM | "sim" | Not "seem" or "S-I-E-M" |
| SOAR | "sore" | Like the word "soar" |
| pwn | "own" | The 'p' is silent |
| GIF | Debated | Gift without 't' OR "jiff" |
| SQL | "sequel" or "S-Q-L" | Both acceptable |
| GUI | "gooey" | Graphical User Interface |
| CLI | "C-L-I" | Command Line Interface |
| IoC | "I-O-C" | Each letter pronounced |
| APT | "A-P-T" | Each letter pronounced |
| MITRE | "MY-ter" | Like "miter saw" |
| Nginx | "engine-x" | Not "N-ginx" |

---

## Summary

This document covers the informal language of cybersecurity:

1. **Acronyms**: Essential abbreviations for daily communication
2. **Hacker Culture**: Hat colors, attack slang, and underground terms
3. **Community Phrases**: Common expressions and concepts
4. **Intelligence Sharing**: TLP, STIX/TAXII, and attribution
5. **Operations Slang**: Analyst jargon and response terminology

Understanding this vocabulary helps new team members communicate effectively and integrate into security teams quickly.

---

## References

- [TrollEye Security - Top 100 Hacking Terms](https://www.trolleyesecurity.com/the-top-100-hacking-cybersecurity-terms/)
- [SANS Institute Glossary](https://www.sans.org/security-resources/glossary-of-terms)
- [CISA NICCS Glossary](https://niccs.cisa.gov/resources/glossary)
- [FIRST - Traffic Light Protocol (TLP)](https://www.first.org/tlp/)
- [MITRE ATT&CK](https://attack.mitre.org/)
- [Astra - Hacking Terminologies](https://www.getastra.com/blog/knowledge-base/hacking-terminologies/)
