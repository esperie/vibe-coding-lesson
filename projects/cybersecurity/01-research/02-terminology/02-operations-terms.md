# Cybersecurity Operations Terminology

Comprehensive reference for operational cybersecurity terminology covering security teams, penetration testing, threat hunting, incident response, and digital forensics.

## Table of Contents

1. [Security Team Colors](#security-team-colors)
2. [Penetration Testing Terms](#penetration-testing-terms)
3. [Threat Hunting Terminology](#threat-hunting-terminology)
4. [Incident Response Terms](#incident-response-terms)
5. [Digital Forensics Terms](#digital-forensics-terms)

---

## Security Team Colors

Modern cybersecurity operations use a color-coded system to distinguish between different security roles and exercise types.

### Red Team (Offensive Security)

A group of security professionals who simulate real-world cyberattacks against an organization to test its defenses. Red teams think and act like adversaries.

**Responsibilities**:
- Simulate sophisticated attacks
- Test detection and response capabilities
- Identify weaknesses in people, processes, and technology
- Emulate specific threat actors (APT groups)

**Key characteristics**:
- Goal-oriented (e.g., access the crown jewels)
- Uses real attacker TTPs
- May use social engineering
- Often operates without the knowledge of most staff

**Common red team activities**:
- Phishing campaigns
- Physical security testing
- Network penetration
- Application exploitation
- Social engineering

**Use in context**: "The red team successfully gained domain admin access through a spear-phishing attack targeting the finance department."

### Blue Team (Defensive Security)

Security professionals responsible for defending the organization's systems, detecting threats, and responding to incidents. The blue team maintains and improves security posture.

**Responsibilities**:
- Monitor security systems and alerts
- Detect and analyze threats
- Respond to security incidents
- Maintain security controls
- Improve defensive capabilities

**Key roles**:
- **Security Analyst**: Alert triage and investigation
- **Incident Responder**: Handle active security incidents
- **Threat Hunter**: Proactively search for threats
- **Security Engineer**: Build and maintain security tools

**Core disciplines**:
- Threat detection and monitoring (SIEM, EDR, XDR)
- Incident response
- Vulnerability management
- Security architecture

**Use in context**: "The blue team detected the intrusion within 20 minutes of initial access."

### Purple Team (Collaborative Approach)

A collaborative methodology that combines red team (offensive) and blue team (defensive) efforts to maximize security effectiveness. Purple team is not necessarily a separate team but a way of working together.

**Key principles**:
- Real-time collaboration between attackers and defenders
- Immediate feedback on detection gaps
- Continuous improvement of detection capabilities
- Knowledge sharing between offensive and defensive teams

**Purple team activities**:
- Joint attack-defense exercises
- Detection engineering sessions
- Tabletop exercises
- Adversary emulation with blue team observation

**Benefits**:
- Validates defensive capabilities against realistic threats
- Identifies detection gaps quickly
- Improves both red and blue team skills
- Provides measurable security improvements

**Use in context**: "Our quarterly purple team sessions focus on specific threat scenarios - this quarter we're testing ransomware detection."

### White Team (Oversight and Management)

The group that oversees and manages operations between red and blue teams during security exercises. They set the rules of engagement and act as referees.

**Responsibilities**:
- Define exercise scope and rules of engagement
- Manage exercise timeline
- Ensure safety (no actual damage)
- Mediate disputes
- Evaluate outcomes

**Use in context**: "The white team paused the exercise when the red team attempted to pivot into a production system outside the agreed scope."

### Team Color Summary

| Team | Focus | Mindset |
|------|-------|---------|
| **Red** | Offense | "How do I break in?" |
| **Blue** | Defense | "How do I protect and detect?" |
| **Purple** | Collaboration | "How do we improve together?" |
| **White** | Oversight | "Are we following the rules?" |

---

## Penetration Testing Terms

Penetration testing (pentesting) is an authorized simulated cyberattack to evaluate system security.

### Testing Scope Types

#### Black Box Testing
Testing with no prior knowledge of the target system. Testers approach like external attackers with only publicly available information.

**Characteristics**:
- Most realistic external attack simulation
- Time-consuming reconnaissance phase
- May miss vulnerabilities due to limited time
- Tests detection capabilities

#### White Box Testing
Testing with full knowledge of the target system, including source code, network diagrams, and credentials.

**Characteristics**:
- Most thorough coverage
- Faster and more efficient
- Can find deep architectural issues
- Less realistic attack simulation

#### Gray Box Testing
Testing with partial knowledge of the target system. Balances realism with efficiency.

**Characteristics**:
- Common approach for internal assessments
- May have user-level credentials
- Some documentation provided
- Simulates insider threat or compromised user

### Penetration Testing Phases

#### 1. Reconnaissance (Information Gathering)

The initial phase focused on collecting information about the target without actively engaging systems.

**Passive reconnaissance**:
- OSINT (Open Source Intelligence)
- DNS records
- WHOIS information
- Social media research
- Job postings (reveal technology stack)
- Public documents

**Active reconnaissance**:
- Port scanning
- Service enumeration
- Network mapping
- Banner grabbing

**Tools**: Shodan, Maltego, theHarvester, Google dorking, Nmap

**Use in context**: "During reconnaissance, we discovered an exposed development server through DNS enumeration."

#### 2. Scanning

Technical review of the target to identify potential entry points and vulnerabilities.

**Activities**:
- Port scanning (open ports and services)
- Vulnerability scanning
- Web application scanning
- Network mapping

**Tools**: Nmap, Nessus, Burp Suite, Nikto

#### 3. Vulnerability Assessment

Analysis of scan results to identify exploitable vulnerabilities.

**Activities**:
- Correlate findings with CVE database
- Assess CVSS scores
- Identify false positives
- Prioritize targets

#### 4. Exploitation

Actively attempting to exploit identified vulnerabilities to gain access.

**Exploitation techniques**:
- Web application attacks (SQLi, XSS)
- Network service exploitation
- Password attacks
- Social engineering
- Client-side attacks

**Tools**: Metasploit, Burp Suite, SQLmap, Cobalt Strike

**Use in context**: "Exploitation of the unpatched Apache server gave us initial foothold."

#### 5. Post-Exploitation

Actions taken after gaining initial access to achieve testing objectives.

**Activities**:
- Privilege escalation
- Lateral movement
- Data exfiltration
- Persistence establishment
- Evidence collection

#### 6. Pivoting

Using a compromised system as a jumping point to access other systems that were previously unreachable.

**Use in context**: "We pivoted through the web server to access the internal database server that wasn't exposed to the internet."

#### 7. Reporting

Documenting findings, evidence, and recommendations.

**Report contents**:
- Executive summary
- Methodology
- Findings with risk ratings
- Evidence and screenshots
- Remediation recommendations

### Key Penetration Testing Terms

#### Footprinting
The process of gathering information about a target network and its environment. Similar to reconnaissance.

#### Enumeration
Extracting detailed information from systems, such as usernames, network shares, and services.

#### Privilege Escalation
Gaining higher-level permissions than initially obtained. Can be vertical (user to admin) or horizontal (access another user's data).

**Vertical**: User -> Administrator
**Horizontal**: User A -> User B's data

#### Lateral Movement
Moving from one compromised system to other systems within the network.

**Common techniques**:
- Pass-the-hash
- Remote service exploitation
- Credential reuse
- Remote desktop

**Use in context**: "After compromising the workstation, we used lateral movement to reach the domain controller."

#### Persistence
Maintaining access to a compromised system across reboots and user logouts.

**Techniques**:
- Registry run keys
- Scheduled tasks
- Services
- Startup scripts
- Backdoors

#### Rules of Engagement (RoE)
A formal document defining the scope, limitations, and guidelines for a penetration test.

**Includes**:
- Systems in scope
- Prohibited actions
- Testing windows
- Communication protocols
- Emergency contacts

#### Crown Jewels
The most critical assets an organization wants to protect (often the ultimate objective of a red team exercise).

**Examples**: Customer database, intellectual property, financial systems, domain controllers

---

## Threat Hunting Terminology

Threat hunting is the proactive search for threats that have evaded existing security controls.

### Core Concepts

#### Threat Hunting
A proactive, iterative process of searching through networks and endpoints to detect threats that evade existing security solutions. Unlike reactive monitoring, hunters actively look for adversary activity.

**Key characteristics**:
- Hypothesis-driven
- Proactive (not waiting for alerts)
- Uses TTPs as guide
- Assumes breach mindset

**Use in context**: "Our threat hunting team detected the APT presence that had been in our network for three months."

#### Hypothesis-Driven Hunting
An approach where hunters develop hypotheses about potential threats and search for evidence to confirm or refute them.

**Example hypothesis**: "Attackers may be using PowerShell for lateral movement in our environment."

**Hunt process**:
1. Develop hypothesis based on intelligence
2. Identify data sources
3. Execute hunt queries
4. Analyze results
5. Document findings

#### Assumed Breach
A security mindset that assumes adversaries have already compromised the network. Hunters search for evidence of compromise rather than assuming defenses are working.

### Hunt Types

#### Intelligence-Driven Hunting
Using threat intelligence (IOCs, TTPs, threat reports) to guide hunting activities.

**Use in context**: "Based on the CISA alert about APT29 techniques, we're hunting for their known PowerShell patterns."

#### Situational Awareness Hunting
Building understanding of normal behavior in the environment to identify anomalies.

**Focus areas**:
- Normal user behavior patterns
- Expected network traffic
- Standard processes and services

#### Analytics-Driven Hunting
Using statistical analysis and machine learning to identify anomalies that may indicate threats.

### Threat Intelligence Terms

#### CTI (Cyber Threat Intelligence)
Information about threats and threat actors that helps organizations understand risks and improve defenses.

**Intelligence types**:
| Type | Audience | Content |
|------|----------|---------|
| Strategic | Executives | Threat landscape, trends |
| Operational | Security managers | Attack campaigns, actor profiles |
| Tactical | Analysts | IOCs, TTPs, detection rules |

#### TTP (Tactics, Techniques, and Procedures)
The behavioral patterns describing how threat actors operate.

**Hierarchy**:
```
Tactics (Why) -> Techniques (How) -> Procedures (Specific Implementation)
```

**Example**:
- **Tactic**: Initial Access
- **Technique**: Spear Phishing Attachment
- **Procedure**: Attacker sends Excel file with malicious macro to finance staff

#### ATT&CK Mapping
Correlating observed adversary behavior to the MITRE ATT&CK framework.

**Common tactics** (Enterprise Matrix):
1. Reconnaissance
2. Resource Development
3. Initial Access
4. Execution
5. Persistence
6. Privilege Escalation
7. Defense Evasion
8. Credential Access
9. Discovery
10. Lateral Movement
11. Collection
12. Command and Control
13. Exfiltration
14. Impact

#### Threat Actor
An individual or group that performs cyberattacks. Also called adversary or threat agent.

**Types**:
- **Nation-state**: Government-sponsored (APT groups)
- **Cybercriminal**: Financially motivated
- **Hacktivist**: Ideologically motivated
- **Insider**: Malicious employee
- **Script kiddie**: Unsophisticated attacker using existing tools

#### APT (Advanced Persistent Threat)
Sophisticated threat actors (often nation-state) who gain unauthorized access and maintain presence over extended periods.

**Characteristics**:
- Advanced capabilities
- Persistent (long-term presence)
- Targeted attacks
- Well-resourced
- Specific objectives (espionage, sabotage)

**Naming conventions**:
- **Mandiant**: APT1, APT28, APT29
- **CrowdStrike**: Fancy Bear, Cozy Bear
- **Microsoft**: NOBELIUM, HAFNIUM

---

## Incident Response Terms

Incident response (IR) is the structured approach to handling security incidents.

### IR Team Structures

#### CSIRT (Computer Security Incident Response Team)
A dedicated team responsible for detecting, analyzing, and responding to security incidents. Also called CIRT (Cyber Incident Response Team) or CERT (Computer Emergency Response Team).

**Core functions**:
- Incident detection and analysis
- Containment and eradication
- Recovery coordination
- Communication management
- Documentation and reporting

#### CERT (Computer Emergency Response Team)
A team that responds to computer security incidents. CERT is a registered trademark of Carnegie Mellon University's CERT Coordination Center.

**Note**: Many organizations use CSIRT to avoid trademark issues.

#### ISAC (Information Sharing and Analysis Center)
Sector-specific organizations that facilitate information sharing about threats and vulnerabilities between members.

**Examples**: FS-ISAC (Financial Services), H-ISAC (Healthcare), Auto-ISAC (Automotive)

### IR Lifecycle Phases

#### 1. Preparation
Activities before an incident occurs to ensure readiness.

**Activities**:
- Develop IR plans and playbooks
- Train IR team members
- Deploy detection and response tools
- Establish communication channels
- Conduct tabletop exercises

**Use in context**: "Our preparation phase includes quarterly IR exercises and maintaining current playbooks."

#### 2. Detection and Analysis (Identification)
Recognizing that an incident has occurred and understanding its scope.

**Detection sources**:
- SIEM alerts
- EDR detections
- User reports
- Threat intelligence
- Anomaly detection

**Analysis activities**:
- Alert validation
- False positive elimination
- Scope determination
- Impact assessment

#### 3. Containment
Actions to limit the damage and prevent further spread of an incident.

**Short-term containment**:
- Isolate affected systems
- Block malicious IPs
- Disable compromised accounts
- Disconnect network segments

**Long-term containment**:
- Apply temporary fixes
- Implement additional monitoring
- Prepare for eradication

**Use in context**: "We implemented containment by isolating the infected workstations and blocking C2 communication."

#### 4. Eradication
Completely removing the threat from the environment.

**Activities**:
- Remove malware
- Close vulnerabilities
- Reset compromised credentials
- Clean or rebuild affected systems
- Verify complete removal

**Use in context**: "Eradication required rebuilding 15 systems and resetting all domain credentials."

#### 5. Recovery
Restoring affected systems to normal operation.

**Activities**:
- Restore systems from clean backups
- Validate system integrity
- Return to normal operations
- Implement enhanced monitoring
- Verify business functionality

#### 6. Lessons Learned (Post-Incident Activity)
Analyzing the incident to improve future response.

**Activities**:
- Document timeline
- Identify what worked/didn't work
- Update procedures and playbooks
- Implement recommended improvements
- Share relevant intelligence

### Key IR Terms

#### Triage
The initial assessment process to prioritize incidents based on severity and impact.

**Triage questions**:
- What is affected?
- Is it ongoing?
- What is the potential impact?
- How urgent is response?

**Use in context**: "Triage determined this was a critical incident requiring immediate escalation."

#### Escalation
Moving an incident to a higher level of support or management attention.

**Escalation types**:
- **Technical**: To more skilled responders
- **Management**: To leadership for decisions
- **External**: To law enforcement or regulators

#### MTTR (Mean Time to Respond)
The average time from incident detection to initial response.

#### MTTD (Mean Time to Detect)
The average time from when an attack begins to when it is detected.

#### MTTR (Mean Time to Recover)
The average time from incident detection to full recovery.

#### Playbook (Runbook)
A documented set of procedures for responding to specific incident types.

**Common playbooks**:
- Malware infection
- Ransomware
- Phishing
- Data breach
- Account compromise
- DDoS attack

#### War Room
A dedicated physical or virtual space where the IR team gathers during major incidents.

#### Dwell Time
The duration an attacker remains undetected in an environment.

**Industry average**: 277 days (2024)

**Use in context**: "The threat actor had a dwell time of 6 months before we detected them."

---

## Digital Forensics Terms

Digital forensics is the process of collecting, preserving, analyzing, and presenting digital evidence.

### Core Principles

#### Chain of Custody
A documented record tracking the handling of evidence from collection through court presentation.

**Documentation includes**:
- Who collected the evidence
- Date/time of collection
- How it was collected
- Every transfer of custody
- Storage conditions
- Any analysis performed

**Purpose**: Proves evidence integrity and admissibility in court.

**Use in context**: "The chain of custody documentation shows exactly who handled the evidence at each stage."

#### Forensic Soundness
Ensuring that evidence is collected and handled in a way that maintains its integrity and admissibility.

**Principles**:
- Use forensically sound tools
- Document all actions
- Work on copies, not originals
- Verify integrity with hashes

#### Evidence Integrity
Ensuring that evidence has not been altered or tampered with since collection.

**Verification methods**:
- Hash values (MD5, SHA-1, SHA-256)
- Write blockers
- Documented procedures

### Evidence Collection

#### Acquisition
The process of creating a forensic copy of digital evidence.

**Types**:
- **Physical acquisition**: Bit-for-bit copy of entire storage media
- **Logical acquisition**: Copy of files and folders (not deleted data)
- **Targeted acquisition**: Specific files or data

#### Forensic Image
A bit-for-bit copy of storage media, including deleted files, unallocated space, and metadata.

**Characteristics**:
- Exact duplicate of original
- Includes all data (not just files)
- Verifiable via hash comparison
- Read-only

**Use in context**: "We created a forensic image of the suspect's hard drive before any analysis."

#### Write Blocker
Hardware or software that prevents any writes to storage media, ensuring the original evidence is not modified during acquisition.

**Types**:
- Hardware write blockers (physical devices)
- Software write blockers

**Use in context**: "We connected the drive through a write blocker to prevent any accidental modifications."

#### Hash Value (Digital Fingerprint)
A fixed-size value calculated from data using a cryptographic hash function. Used to verify data integrity.

**Common algorithms**:
- MD5 (128-bit) - fast but deprecated for security
- SHA-1 (160-bit) - deprecated for security
- SHA-256 (256-bit) - current standard

**Use in context**: "The SHA-256 hashes of the original and image match, confirming integrity."

### Forensic Analysis

#### Dead Box Analysis (Static Forensics)
Analyzing powered-off systems. Traditional forensic approach.

**Analyzes**:
- Hard drives
- USB devices
- Removable media

**Advantages**: Repeatable, thorough

#### Live Forensics
Collecting evidence from running systems before powering down.

**Captures**:
- Running processes
- Network connections
- Memory contents
- Logged-in users
- Encryption keys in memory

**When used**: Volatile data is critical, system cannot be powered down

**Use in context**: "We performed live forensics to capture the malware in memory before it could terminate."

#### Memory Forensics
Analysis of a system's RAM to extract evidence that exists only in volatile memory.

**Can extract**:
- Running malware
- Encryption keys
- Network connections
- Passwords in memory
- Process information

**Tools**: Volatility, Rekall

#### Timeline Analysis
Creating a chronological sequence of events from various evidence sources.

**Sources**:
- File system timestamps
- Log files
- Browser history
- Registry entries
- Email timestamps

**Use in context**: "Timeline analysis revealed the attacker's activities over a three-week period."

### Forensic Artifacts

#### Artifact
Digital evidence left behind by user activity or system processes.

**Common Windows artifacts**:
- Prefetch files (program execution)
- Registry hives (configuration and user activity)
- Event logs (system and security events)
- Jump lists (recent files)
- Browser artifacts
- Shellbags (folder access)

#### Metadata
Data about data. Information embedded in files about their creation, modification, and other attributes.

**Examples**:
- File creation/modification dates
- Document author
- Camera information in photos (EXIF)
- GPS coordinates

#### Slack Space
The unused space between the end of a file and the end of the disk cluster. May contain fragments of deleted data.

#### Unallocated Space
Disk space not currently assigned to any file. May contain deleted file fragments.

### Forensic Tools

**Common forensic tools**:
| Tool | Purpose |
|------|---------|
| **FTK Imager** | Disk imaging and acquisition |
| **EnCase** | Complete forensic suite |
| **Autopsy** | Open-source forensic platform |
| **Volatility** | Memory forensics |
| **Cellebrite** | Mobile device forensics |
| **Wireshark** | Network traffic analysis |
| **AXIOM** | Multi-platform forensics |

### Legal Considerations

#### Admissibility
Whether evidence can be accepted in court proceedings.

**Requirements**:
- Relevance
- Authenticity (chain of custody)
- Reliability (forensic soundness)
- Best evidence rule compliance

#### Expert Witness
A forensic examiner who testifies in court about their findings and methodology.

#### e-Discovery
The process of identifying, collecting, and producing electronically stored information (ESI) in legal proceedings.

---

## Summary

This document covers operational cybersecurity terminology across five key areas:

1. **Team Colors**: Red (offense), Blue (defense), Purple (collaboration), White (oversight)
2. **Penetration Testing**: Methodologies, phases, and techniques for authorized security testing
3. **Threat Hunting**: Proactive approaches to finding hidden threats
4. **Incident Response**: Structured approach to handling security incidents
5. **Digital Forensics**: Evidence collection, preservation, and analysis

For governance and compliance terminology, see [03-governance-terms.md](./03-governance-terms.md).

---

## References

- [CrowdStrike - Incident Response Steps](https://www.crowdstrike.com/en-us/cybersecurity-101/incident-response/incident-response-steps/)
- [SANS Institute - Incident Response Cycle](https://www.sans.org/security-resources/glossary-of-terms)
- [EC-Council - Penetration Testing Phases](https://www.eccouncil.org/cybersecurity-exchange/penetration-testing/penetration-testing-phases/)
- [MITRE ATT&CK Framework](https://attack.mitre.org/)
- [NIST SP 800-61 - Computer Security Incident Handling Guide](https://nvlpubs.nist.gov/nistpubs/specialpublications/nist.sp.800-61r2.pdf)
- [InfoSec Institute - Chain of Custody](https://www.infosecinstitute.com/resources/digital-forensics/computer-forensics-chain-custody/)
