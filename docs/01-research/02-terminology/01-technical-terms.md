# Technical Cybersecurity Terminology

Comprehensive reference for technical terms used in government cybersecurity operations. This document covers network security, cryptography, vulnerability management, and malware analysis terminology.

## Table of Contents

1. [Network Security Terms](#network-security-terms)
2. [Cryptography Terms](#cryptography-terms)
3. [Vulnerability Terms](#vulnerability-terms)
4. [Malware Analysis Terms](#malware-analysis-terms)

---

## Network Security Terms

### Infrastructure Components

#### DMZ (Demilitarized Zone)
A network segment that sits between an organization's internal network and the external internet, providing an additional layer of security for hosting public-facing services. The DMZ acts as a buffer zone where external-facing servers (web servers, email servers) are placed, preventing direct access to internal systems.

**Use in context**: "We host our public web servers in the DMZ to isolate them from our internal network."

#### Firewall
A network security device that monitors and controls incoming and outgoing network traffic based on predetermined security rules. Firewalls establish a barrier between trusted internal networks and untrusted external networks.

**Types**:
- **Packet-filtering firewall**: Examines packets in isolation
- **Stateful inspection firewall**: Tracks connection states
- **Application-layer firewall**: Inspects application data
- **Next-generation firewall (NGFW)**: Combines traditional firewall with additional features like IPS

**Use in context**: "The firewall blocked outbound connections to suspicious IP addresses."

#### IDS (Intrusion Detection System)
A passive monitoring system that scans network traffic and raises alerts when it detects suspicious activity or known attack signatures. IDS sits out-of-band (not directly in the network path) and relies on a TAP or SPAN port to copy network traffic in real time.

**Types**:
- **NIDS (Network Intrusion Detection System)**: Monitors network traffic at strategic points
- **HIDS (Host Intrusion Detection System)**: Monitors individual host systems

**Key characteristic**: Detection only - does not block traffic

**Use in context**: "The IDS flagged unusual SSH traffic patterns that we need to investigate."

#### IPS (Intrusion Prevention System)
An active network security technology that not only detects but also prevents identified threats in real-time. IPS sits inline with network traffic and can block malicious packets before they reach their destination.

**Key characteristic**: Detection AND prevention - actively blocks threats

**Use in context**: "The IPS automatically blocked the SQL injection attempt."

#### IDS vs IPS Comparison

| Aspect | IDS | IPS |
|--------|-----|-----|
| Position | Out-of-band (passive) | Inline (active) |
| Action | Alert only | Alert and block |
| Latency impact | None | Minimal |
| False positive risk | Alert noise | Blocked legitimate traffic |

### Security Operations Infrastructure

#### SIEM (Security Information and Event Management)
*Pronounced "sim" (not "seem")*

A platform that collects, aggregates, and analyzes security event data from across an organization's IT infrastructure. SIEM provides centralized visibility, correlation of events, and real-time monitoring capabilities.

**Core functions**:
- Log collection and management
- Event correlation and analysis
- Real-time alerting
- Compliance reporting
- Forensic investigation support

**Common SIEM platforms**: Splunk, IBM QRadar, Microsoft Sentinel, Elastic Security

**Use in context**: "The SIEM correlated multiple failed login attempts across different systems, indicating a possible brute force attack."

#### SOC (Security Operations Center)
A dedicated team and facility responsible for monitoring, detecting, analyzing, and responding to cybersecurity incidents 24/7. The SOC serves as the organization's security nerve center.

**Key roles in a SOC**:
- **Tier 1 Analyst**: Initial triage and alert handling
- **Tier 2 Analyst**: Deep investigation and analysis
- **Tier 3 Analyst**: Advanced threat hunting and incident response
- **SOC Manager**: Team leadership and escalation point

**Use in context**: "The SOC detected the breach within 15 minutes of initial compromise."

#### NOC (Network Operations Center)
A centralized facility focused on maintaining network performance, availability, and uptime. While similar to a SOC in structure, the NOC focuses on operational health rather than security.

**SOC vs NOC**:
| SOC | NOC |
|-----|-----|
| Security-focused | Operations-focused |
| Threat detection | Performance monitoring |
| Incident response | Availability management |

### Detection and Response Platforms

#### EDR (Endpoint Detection and Response)
A cybersecurity solution focused on monitoring and responding to threats on endpoints (laptops, desktops, servers, mobile devices). EDR continuously collects and analyzes endpoint data to detect suspicious activities.

**Key capabilities**:
- Continuous endpoint monitoring
- Behavioral analysis (not just signature-based)
- Threat investigation tools
- Automated response actions
- Historical data for forensics

**Use in context**: "EDR detected the malware executing in memory despite no file being written to disk."

#### XDR (Extended Detection and Response)
An evolution of EDR that extends detection and response capabilities across multiple security layers including endpoints, networks, email, and cloud environments. XDR provides a unified view across the entire security stack.

**XDR vs EDR**:
- EDR: Endpoint-focused
- XDR: Cross-layer visibility and correlation

**Use in context**: "XDR correlated the phishing email with the subsequent endpoint compromise and lateral movement."

#### NDR (Network Detection and Response)
Network monitoring solution that uses AI and machine learning to establish baseline network behavior and identify anomalies that may indicate cyberattacks or unauthorized access.

**Key capabilities**:
- Network traffic analysis
- Behavioral baseline modeling
- Anomaly detection
- Threat hunting support

**Use in context**: "NDR detected unusual data exfiltration patterns in encrypted traffic."

#### MDR (Managed Detection and Response)
A service model where external security experts provide 24/7 monitoring, threat hunting, and incident response capabilities. MDR addresses the challenge of limited in-house security expertise.

**Use in context**: "We use MDR to augment our small security team with 24/7 coverage."

#### SOAR (Security Orchestration, Automation, and Response)
A platform that integrates security tools, automates repetitive tasks, and orchestrates incident response workflows. SOAR reduces manual effort and standardizes response procedures.

**Key capabilities**:
- Playbook automation
- Tool integration/orchestration
- Case management
- Metrics and reporting

**Use in context**: "The SOAR playbook automatically isolated the compromised endpoint and initiated a malware scan."

### Network Protocols and Concepts

#### TCP/IP (Transmission Control Protocol/Internet Protocol)
The fundamental communication protocols of the internet. TCP ensures reliable data transmission, while IP handles addressing and routing.

#### DNS (Domain Name System)
The system that translates human-readable domain names into IP addresses. A common attack vector for DNS hijacking, tunneling, and amplification attacks.

#### VPN (Virtual Private Network)
Technology that creates an encrypted tunnel for secure communication over public networks.

#### TLS/SSL (Transport Layer Security/Secure Sockets Layer)
Cryptographic protocols that provide secure communication over networks. TLS is the modern successor to SSL.

---

## Cryptography Terms

### Encryption Fundamentals

#### Encryption
The process of converting plaintext data into ciphertext using an algorithm and a key, making it unreadable to unauthorized parties.

**Types**:
- **At-rest encryption**: Protects stored data
- **In-transit encryption**: Protects data during transmission
- **End-to-end encryption (E2EE)**: Data encrypted from sender to recipient

#### Symmetric Encryption
Encryption method where the same key is used for both encryption and decryption. Fast but requires secure key distribution.

**Common algorithms**: AES, 3DES, ChaCha20

**Use in context**: "We use AES-256 symmetric encryption for data at rest."

#### Asymmetric Encryption (Public Key Cryptography)
Encryption method using a pair of mathematically related keys: a public key for encryption and a private key for decryption.

**Common algorithms**: RSA, ECC, Ed25519

**Key principle**: Public keys can be freely shared; private keys must be protected.

**Use in context**: "The message was encrypted with the recipient's public key, so only they can decrypt it."

### Hashing

#### Hash Function
A one-way mathematical function that takes data of any size and produces a fixed-size output (hash value or digest). Hashing cannot be reversed to reveal the original data.

**Properties of cryptographic hash functions**:
- **Deterministic**: Same input always produces same output
- **Fast computation**: Quick to calculate
- **Pre-image resistance**: Cannot derive input from output
- **Collision resistance**: Extremely difficult to find two inputs with same output

**Common algorithms**: SHA-256, SHA-3, MD5 (deprecated), SHA-1 (deprecated)

**Use in context**: "We verified the file integrity by comparing SHA-256 hashes."

#### Salt
Random data added to a password before hashing to prevent rainbow table attacks and ensure identical passwords produce different hashes.

**Use in context**: "All passwords are salted before hashing to prevent rainbow table attacks."

### Public Key Infrastructure (PKI)

#### PKI (Public Key Infrastructure)
A framework of policies, procedures, hardware, software, and roles for creating, managing, distributing, using, storing, and revoking digital certificates.

**Core components**:
- Certificate Authority (CA)
- Registration Authority (RA)
- Digital certificates
- Certificate Revocation Lists (CRL)
- Key management systems

#### Certificate Authority (CA)
A trusted entity that issues digital certificates, verifying the identity of certificate holders and the authenticity of their public keys.

**Types**:
- **Root CA**: Top of the trust hierarchy
- **Intermediate CA**: Signed by Root CA, issues end-entity certificates
- **Internal CA**: Organization's private certificate authority

**Use in context**: "Our internal CA issues certificates for employee authentication."

#### Digital Certificate (X.509 Certificate)
An electronic document that binds a public key to an identity. Contains the public key, identity information, validity period, and CA signature.

**Certificate contents**:
- Subject (identity)
- Public key
- Issuer (CA)
- Validity period
- Digital signature
- Serial number

**Use in context**: "The web server's SSL certificate expired, causing browser warnings."

#### Certificate Revocation
The process of invalidating a certificate before its expiration date, typically due to compromise of the private key or change in certificate holder status.

**Methods**:
- **CRL (Certificate Revocation List)**: Periodic list of revoked certificates
- **OCSP (Online Certificate Status Protocol)**: Real-time certificate validation

### Key Management

#### Key Pair
A mathematically related public key and private key used in asymmetric cryptography.

#### Key Escrow
The practice of storing copies of encryption keys with a trusted third party for recovery purposes.

#### Ephemeral Keys
Keys generated for a single session or transaction and discarded after use. Provides forward secrecy - compromised long-term keys don't expose past communications.

**Use in context**: "We use ephemeral keys in TLS to ensure forward secrecy."

---

## Vulnerability Terms

### Vulnerability Identification

#### CVE (Common Vulnerabilities and Exposures)
A unique identifier assigned to publicly known cybersecurity vulnerabilities. Maintained by MITRE Corporation on behalf of CISA.

**Format**: CVE-{YEAR}-{ID}
**Example**: CVE-2021-44228 (Log4Shell)

**Use in context**: "We need to patch CVE-2024-1234 on all affected systems immediately."

#### NVD (National Vulnerability Database)
A US government repository of vulnerability management data that enhances CVE entries with additional analysis, including CVSS scores.

**Source**: [nvd.nist.gov](https://nvd.nist.gov)

### Vulnerability Scoring

#### CVSS (Common Vulnerability Scoring System)
An open framework for rating the severity of security vulnerabilities on a scale of 0 to 10.

**Severity ratings**:
| Score | Rating |
|-------|--------|
| 0.0 | None |
| 0.1 - 3.9 | Low |
| 4.0 - 6.9 | Medium |
| 7.0 - 8.9 | High |
| 9.0 - 10.0 | Critical |

**Metric groups** (CVSS v4.0):
- **Base**: Intrinsic vulnerability characteristics
- **Threat**: Factors like exploit availability
- **Environmental**: Organization-specific factors
- **Supplemental**: Additional contextual information

**Use in context**: "This vulnerability has a CVSS score of 9.8 - critical severity requiring immediate patching."

#### EPSS (Exploit Prediction Scoring System)
A model that estimates the probability a vulnerability will be exploited in the wild within the next 30 days. Complements CVSS by predicting real-world exploitation likelihood.

**Use in context**: "Despite the moderate CVSS, EPSS shows 87% exploitation probability - prioritize this patch."

#### KEV (Known Exploited Vulnerabilities)
CISA's catalog of vulnerabilities confirmed to be actively exploited in the wild. Provides actionable intelligence on which vulnerabilities attackers are actually using.

**Source**: [cisa.gov/known-exploited-vulnerabilities-catalog](https://www.cisa.gov/known-exploited-vulnerabilities-catalog)

### Vulnerability Types

#### Zero-Day (0day)
A vulnerability unknown to the software vendor or for which no patch exists. Called "zero-day" because developers have had zero days to fix it before exploitation.

**Timeline**:
1. Vulnerability discovered (by researcher or attacker)
2. If discovered by attacker: exploitation begins (0day in the wild)
3. Vendor notified
4. Patch developed and released (no longer 0day)

**Use in context**: "We detected exploitation of a zero-day vulnerability in our email server."

#### Exploit
Code or technique that takes advantage of a vulnerability to cause unintended behavior in a system.

**Types**:
- **Local exploit**: Requires prior access to the system
- **Remote exploit**: Can be triggered over a network
- **Proof of Concept (PoC)**: Demonstrates vulnerability exists
- **Weaponized exploit**: Ready for malicious use

#### Payload
The component of an exploit that performs the malicious action after the vulnerability is exploited. The exploit delivers the payload.

**Common payloads**:
- Reverse shell
- Keylogger
- Ransomware dropper
- Data exfiltration script

**Use in context**: "The exploit delivered a reverse shell payload to establish persistence."

### Vulnerability Assessment

#### Vulnerability Assessment
The process of identifying, quantifying, and prioritizing vulnerabilities in systems, networks, and applications.

#### Vulnerability Scanner
Automated tools that scan systems for known vulnerabilities.

**Common tools**: Nessus, Qualys, Rapid7 Nexpose, OpenVAS

#### Patch Management
The process of identifying, acquiring, testing, and installing software patches to address vulnerabilities.

---

## Malware Analysis Terms

### Threat Intelligence Indicators

#### IOC (Indicator of Compromise)
Forensic evidence suggesting a system or network has been breached. IOCs are reactive - they indicate a compromise has already occurred.

**Types of IOCs**:
- **File hashes**: MD5, SHA-1, SHA-256 of malicious files
- **IP addresses**: Known malicious infrastructure
- **Domain names**: C2 servers, malware distribution sites
- **URLs**: Specific malicious URLs
- **Registry keys**: Persistence mechanisms
- **File paths**: Known malware locations
- **Email indicators**: Malicious sender addresses, subjects

**Use in context**: "We searched our logs for IOCs from the threat intelligence feed."

#### IOA (Indicator of Attack)
Behavioral patterns that indicate an attack is in progress. IOAs are proactive and focus on attacker actions regardless of specific tools used.

**IOC vs IOA comparison**:
| Aspect | IOC | IOA |
|--------|-----|-----|
| Timing | After compromise | During attack |
| Nature | Static artifacts | Behavioral patterns |
| Focus | Evidence | Intent and actions |
| Detection | Signature matching | Behavioral analysis |

**Use in context**: "The IOA - multiple failed logins followed by successful authentication from a new location - triggered our alert."

### Analysis Methods

#### Sandbox
An isolated environment for safely executing and analyzing suspicious code without risk to production systems. Sandboxes monitor malware behavior in a controlled setting.

**Sandbox analysis captures**:
- File system changes
- Registry modifications
- Network connections
- Process creation
- API calls

**Common sandboxes**: Any.run, Hybrid Analysis, Joe Sandbox, Cuckoo

**Use in context**: "We detonated the suspicious attachment in our sandbox to observe its behavior."

#### Static Analysis
Examining malware without executing it. Involves analyzing code structure, strings, imports, and metadata.

**Techniques**:
- File header analysis
- String extraction
- Disassembly
- Decompilation
- Signature detection

**Advantages**: Safe, no risk of execution
**Limitations**: May miss runtime behavior, obfuscation can defeat analysis

**Use in context**: "Static analysis revealed hardcoded C2 server addresses in the binary."

#### Dynamic Analysis
Executing malware in a controlled environment to observe its behavior.

**Observations include**:
- Files created/modified/deleted
- Network communications
- Process behavior
- System changes

**Advantages**: Reveals actual behavior
**Limitations**: Malware may detect sandbox environment

**Use in context**: "Dynamic analysis showed the malware beaconing to multiple C2 servers every 30 minutes."

#### Reverse Engineering
The process of deconstructing malware to understand its functionality, purpose, and capabilities at the code level.

**Tools**: IDA Pro, Ghidra, x64dbg, OllyDbg

### Threat Intelligence

#### TTP (Tactics, Techniques, and Procedures)
The behavioral patterns that describe how threat actors operate.

**Components**:
- **Tactics**: High-level goals (e.g., initial access, persistence)
- **Techniques**: Methods to achieve tactics (e.g., phishing, registry run keys)
- **Procedures**: Specific implementations of techniques

**Use in context**: "We mapped the adversary's TTPs to the MITRE ATT&CK framework."

#### MITRE ATT&CK
A globally-accessible knowledge base of adversary tactics and techniques based on real-world observations. Provides a common language for describing attacker behavior.

**Structure**:
- **Tactics** (14 categories): What attackers want to achieve
- **Techniques**: How attackers achieve their goals
- **Sub-techniques**: More specific variations
- **Procedures**: Real-world examples

**Matrices available**: Enterprise, Mobile, ICS

**Source**: [attack.mitre.org](https://attack.mitre.org)

#### Threat Feed
A stream of data about current threats, including IOCs, attacker infrastructure, and malware samples. Organizations subscribe to feeds for timely threat intelligence.

**Sources**:
- Commercial feeds (CrowdStrike, Recorded Future)
- Government feeds (US-CERT, CISA)
- Open-source feeds (AlienVault OTX, MISP)

### Malware Types

#### Malware (Malicious Software)
Software intentionally designed to cause damage, gain unauthorized access, or disrupt systems.

**Common types**:
| Type | Description |
|------|-------------|
| **Virus** | Self-replicating code that attaches to programs |
| **Worm** | Self-replicating code that spreads via networks |
| **Trojan** | Malware disguised as legitimate software |
| **Ransomware** | Encrypts files and demands payment |
| **Spyware** | Secretly collects user information |
| **Adware** | Displays unwanted advertisements |
| **Rootkit** | Hides presence while maintaining access |
| **Keylogger** | Records keystrokes |
| **RAT** | Remote Access Trojan - provides remote control |

#### C2/C&C (Command and Control)
Infrastructure used by attackers to communicate with and control compromised systems.

**C2 channels**: HTTP/HTTPS, DNS, social media, cloud services

**Use in context**: "The malware established a C2 channel using encrypted DNS queries."

#### Botnet
A network of compromised computers (bots/zombies) controlled by an attacker for malicious purposes.

**Uses**: DDoS attacks, spam distribution, cryptomining, credential theft

---

## Summary

This document covers the essential technical terminology for cybersecurity professionals. Key areas include:

1. **Network Security**: Understanding defensive infrastructure (firewalls, IDS/IPS, SIEM) and operations centers (SOC/NOC)
2. **Cryptography**: Encryption methods, hashing, PKI, and certificate management
3. **Vulnerabilities**: Identification (CVE), scoring (CVSS), and assessment processes
4. **Malware Analysis**: Indicators (IOC/IOA), analysis methods, and threat intelligence

For practical application of these concepts, see [02-operations-terms.md](./02-operations-terms.md).

---

## References

- [NIST Computer Security Resource Center Glossary](https://csrc.nist.gov/glossary)
- [SANS Institute Glossary of Security Terms](https://www.sans.org/security-resources/glossary-of-terms)
- [MITRE ATT&CK Framework](https://attack.mitre.org/)
- [NVD - Vulnerability Metrics](https://nvd.nist.gov/vuln-metrics/cvss)
- [FIRST.org CVSS Documentation](https://www.first.org/cvss/)
- [Palo Alto Networks Cyberpedia](https://www.paloaltonetworks.com/cyberpedia/glossary)
