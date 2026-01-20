# Current Threat Landscape

> Comprehensive overview of cybersecurity threats, attack vectors, and threat actors
>
> Last Updated: January 2026

## Table of Contents

1. [Malware Types](#1-malware-types)
2. [Social Engineering Attacks](#2-social-engineering-attacks)
3. [Advanced Persistent Threats (APTs)](#3-advanced-persistent-threats-apts)
4. [Supply Chain Attacks](#4-supply-chain-attacks)
5. [Insider Threats](#5-insider-threats)
6. [Nation-State Actors](#6-nation-state-actors)

---

## 1. Malware Types

Malware (malicious software) encompasses any code designed to damage, disrupt, steal, or perform unauthorized actions on systems, data, or networks.

### 1.1 Current Statistics

- **Estimated 6.5 billion infections** will affect enterprises in 2025 (up from 6.2 billion in 2024)
- Malware is present in the majority of cyber incidents
- Modern malware increasingly combines multiple types (hybrid threats)

### 1.2 Ransomware

**Definition**: Malware that encrypts files or locks systems, demanding payment for restoration.

**2025-2026 Statistics**:
| Metric | Value | Change |
|--------|-------|--------|
| Ransomware in breaches | 44% | +37% YoY |
| US attacks (Jan-Oct 2025) | 5,010 incidents | +50% YoY |
| Global claimed victims | 8,000+ annually | +53-63% since 2023 |
| Average ransom payment | ~$1.0 million | -50% from 2024 |
| Organizations refusing payment | 63% | +4% from 2024 |

**Most Active Groups (2025)**:
1. **Qilin** - 81 attacks in June 2025 alone (+47.3%)
2. **Dragonforce** - Surge of +212.5%
3. **Akira** - Growth of +9.7%
4. **Play** - Declined -31.8%

**New Developments**:
- **350+ new ransomware strains** discovered in 2025
- **57 new ransomware groups** observed
- **27 new extortion groups** identified
- **Codefinger** - New threat targeting AWS S3 buckets
- **80% of ransomware attacks** now leverage AI tools

**Double and Triple Extortion**:
1. Encrypt data and demand ransom
2. Threaten to leak stolen data
3. Launch DDoS attacks or contact victims' customers

**Notable 2025 Attacks**:
- **Change Healthcare**: Nearly 193 million individuals affected
- **Jaguar Land Rover**: Britain's costliest cyberattack (estimated at $1.9B)
- **UK Retailers (M&S, Co-op, Harrods)**: Coordinated attacks in April-May 2025

### 1.3 Trojans

**Definition**: Malware disguised as legitimate software to trick users into execution.

**Characteristics**:
- Does NOT self-replicate (unlike viruses and worms)
- Requires user interaction to spread
- Creates backdoors for attackers

**Common Trojan Types**:
| Type | Purpose |
|------|---------|
| Remote Access Trojan (RAT) | Provide remote control of infected systems |
| Banking Trojan | Steal financial credentials |
| Downloader Trojan | Download additional malware |
| Information Stealer | Extract sensitive data |
| Backdoor Trojan | Create persistent access |

**Attack Vectors**:
- Email attachments
- Fake software downloads
- Malicious websites
- Compromised legitimate software

### 1.4 Worms

**Definition**: Self-replicating malware that spreads across networks without user interaction.

**Characteristics**:
- Exploits operating system vulnerabilities
- Standalone program (doesn't need host file)
- Can spread rapidly across networks

**Worm Capabilities**:
- Delete files on host systems
- Encrypt data for ransomware attacks
- Steal information
- Create botnets
- Launch DDoS attacks

**Propagation Methods**:
- Network vulnerabilities
- Software backdoors
- Flash drives
- Email systems

**Historical Example**: Stuxnet - Combined worm, virus, and rootkit capabilities

### 1.5 Spyware

**Definition**: Malware that covertly collects information about users and systems.

**Types**:
| Type | Function |
|------|----------|
| Keyloggers | Record keystrokes to capture passwords |
| Screen Capturers | Take screenshots of user activity |
| Tracking Cookies | Monitor browsing behavior |
| System Monitors | Track all computer activity |
| Mobile Spyware | Access location, camera, microphone |

**Data Targeted**:
- Login credentials
- Banking information
- Personal communications
- Browsing history
- Location data

**Mobile Spyware Dangers**:
- Spreads via SMS/MMS
- Accesses device camera and microphone
- Tracks physical location
- Reads messages and contacts

### 1.6 Rootkits

**Definition**: Malware that obtains administrator-level access while remaining hidden.

**Characteristics**:
- Modifies operating system to create backdoors
- Extremely difficult to detect
- Survives system reboots
- Can hide other malware

**Types**:
| Type | Location |
|------|----------|
| User-mode Rootkit | Application level |
| Kernel-mode Rootkit | OS kernel |
| Bootkit | Boot process |
| Firmware Rootkit | Hardware firmware |
| Hypervisor Rootkit | Virtual machine level |

**Propagation Methods**:
- Phishing emails
- Malicious websites
- USB drives
- Software vulnerabilities
- Malicious advertisements

### 1.7 Additional Malware Types

#### Adware
- Displays unwanted advertisements
- Often bundled with free software
- Can slow systems and track behavior

#### Botnets
- Networks of infected computers
- Controlled remotely by attackers
- Used for DDoS attacks, spam, mining

#### Fileless Malware
- Operates entirely in memory
- Leaves minimal forensic evidence
- Exploits legitimate system tools (e.g., PowerShell)
- 56% of ransomware attacks in 2024 used PowerShell

#### Cryptominers
- Hijack computing resources
- Mine cryptocurrency without consent
- Can significantly impact performance

### 1.8 Hybrid/Blended Threats

Modern malware frequently combines multiple types:

```
┌─────────────────────────────────────────────────────────┐
│                    HYBRID MALWARE                       │
├─────────────────┬─────────────────┬─────────────────────┤
│   Trojan        │     Worm        │     Rootkit         │
│   (Entry)       │   (Spread)      │    (Persistence)    │
├─────────────────┴─────────────────┴─────────────────────┤
│               Ransomware/Spyware Payload                │
└─────────────────────────────────────────────────────────┘
```

---

## 2. Social Engineering Attacks

Social engineering exploits human psychology rather than technical vulnerabilities, manipulating people into divulging information or taking harmful actions.

### 2.1 Scale of the Threat (2025-2026)

| Metric | Value |
|--------|-------|
| Q1 2025 phishing attacks | 1,003,924 (APWG) |
| Q2 2025 phishing attacks | 1,130,393 (+13% QoQ) |
| Social engineering as initial access | 36% of incidents |
| AI-generated phishing content | 82.6% of emails |
| Organizations hit by deepfake attacks | 62% (Gartner) |

### 2.2 Phishing

**Definition**: Fraudulent attempts to obtain sensitive information by impersonating trustworthy entities.

**Types of Phishing**:
| Type | Description |
|------|-------------|
| Email Phishing | Mass emails impersonating legitimate organizations |
| Spear Phishing | Targeted attacks on specific individuals |
| Whaling | Attacks targeting executives and senior leaders |
| Vishing | Voice-based phishing via phone calls |
| Smishing | SMS-based phishing messages |
| Quishing | QR code-based phishing |

**2025 Trends**:
- **Phishing-as-a-Service (PhaaS)** kits grew 21%
- **QR code phishing (quishing)** increasing rapidly
- **Malicious MFA prompts** bypassing security
- **Cloud-hosted credential lures** appearing legitimate

### 2.3 Business Email Compromise (BEC)

**Definition**: Attacks impersonating executives or business partners to request fraudulent transfers or sensitive data.

**2024-2025 Statistics**:
- **21,442 BEC complaints** reported to FBI IC3 (2024)
- **$2.77 billion** in reported losses
- **40% of BEC emails** in Q2 2025 were AI-generated
- **Pretexting incidents** doubled, now 50%+ of social engineering

**Common BEC Scenarios**:
1. CEO fraud (impersonating executives)
2. Vendor email compromise
3. Attorney impersonation
4. Data theft requests
5. W-2/tax form phishing

### 2.4 AI-Powered Attacks

**Current State (2025)**:
- **80%+ of observed social engineering** uses AI (ENISA 2025)
- **91% of security professionals** encountered AI-enabled email attacks
- **Phishing surge of 1,265%** driven partly by AI tools

**AI Capabilities in Attacks**:
| Capability | Impact |
|------------|--------|
| Content Generation | Perfect grammar, personalized messages |
| Deepfake Voice | Impersonate executives in voice calls |
| Deepfake Video | Fake video conferences |
| Translation | Multi-language campaigns at scale |
| Personalization | Scraped data for targeted attacks |

### 2.5 Emerging Attack Vectors

**Non-Phishing Social Engineering**:
- Voice-based lures
- Spoofed browser alerts
- Direct manipulation of support teams
- **Fake CAPTCHA attacks (ClickFix)**: 1,450% spike in early 2025

**Microsoft Teams Exploitation**:
- Attackers posing as IT staff
- Tricking users into installing remote access tools
- Identified as common vector in Q1 2025

### 2.6 Pretexting

**Definition**: Creating fabricated scenarios to manipulate victims into providing information or access.

**Common Pretexts**:
- IT support requests
- Authority figures (law enforcement, executives)
- Vendor or partner impersonation
- Job recruiters
- Survey or research requests

### 2.7 Regional Variations

| Region | Key Trends |
|--------|------------|
| EU | 60% of social engineering was phishing (2024) |
| APAC | 30.5% YoY increase in phishing |
| UK | Authorized push payment fraud up 12% YoY |

### 2.8 Financial Impact

- **Global average breach cost**: $4.4 million (2025)
- **UK fraud losses (H1 2025)**: $629.3 million
- **Authorized push payment fraud**: $257.5 million (UK)

---

## 3. Advanced Persistent Threats (APTs)

APTs are sophisticated, prolonged cyberattacks by well-resourced threat actors, typically nation-states or state-sponsored groups.

### 3.1 Characteristics of APTs

| Characteristic | Description |
|---------------|-------------|
| **Advanced** | Use sophisticated techniques and tools |
| **Persistent** | Maintain long-term access (months to years) |
| **Threat** | Clear objectives and significant resources |
| **Targeted** | Focus on specific organizations or sectors |
| **Stealthy** | Designed to evade detection |

### 3.2 APT Lifecycle

```
┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│  1. Recon    │───>│  2. Initial  │───>│ 3. Establish │
│              │    │    Access    │    │  Foothold    │
└──────────────┘    └──────────────┘    └──────────────┘
                                               │
┌──────────────┐    ┌──────────────┐    ┌──────▼───────┐
│ 6. Exfiltrate│<───│  5. Collect  │<───│ 4. Escalate  │
│    Data      │    │     Data     │    │  Privileges  │
└──────────────┘    └──────────────┘    └──────────────┘
                           │
                    ┌──────▼───────┐
                    │ 7. Maintain  │
                    │   Access     │
                    └──────────────┘
```

### 3.3 Major APT Groups (2025)

**By Nation-State**:

| Country | Notable Groups | Primary Targets |
|---------|---------------|-----------------|
| China | APT41, Mustang Panda | Technology, manufacturing, diplomatic |
| Russia | APT28 (Fancy Bear), APT29 | Political entities, government, critical infrastructure |
| Iran | APT34 (OilRig) | Middle East governments, financial, energy |
| North Korea | Lazarus Group | Financial (cryptocurrency), supply chain |

**Current Intelligence**:
- Microsoft tracks over **600 distinct nation-state hacker groups** worldwide
- Lines have blurred between APT and criminal group capabilities
- "Fine dining to fast food" - APT techniques now widely adopted

### 3.4 APT Naming Conventions

| Organization | Naming Scheme | Example |
|--------------|---------------|---------|
| CrowdStrike | Animals by nation | "Kitten" (Iran), "Spider" (cybercrime) |
| Mandiant | Numbered acronyms | APT, FIN, UNC |
| Microsoft | Element-based | Various |
| Dragos | Minerals | Various |
| Kaspersky | Various | Various |

### 3.5 Evolution of APT Tactics

**2025-2026 Trends**:
- **Increasing geopolitical motivation**: Eastern Europe, South China Sea, Middle East
- **Shift toward conflict**: Beyond espionage to active disruption
- **Credential-based intrusion**: Living off the land with valid credentials
- **AI integration**: For reconnaissance and social engineering

---

## 4. Supply Chain Attacks

Supply chain attacks compromise a single point to impact multiple downstream organizations, making them among the most damaging threat vectors.

### 4.1 2025-2026 Statistics

| Metric | Value |
|--------|-------|
| Third-party related breaches | ~30% of all breaches |
| Average supply chain breach cost | $4.9+ million |
| Downtime cost per hour | $300,000+ |
| Monthly average (April-Dec 2025) | 26 attacks |
| Year-over-year increase | 2x (doubled) |

### 4.2 Types of Supply Chain Attacks

#### Software Supply Chain
- Compromised development tools
- Malicious code in dependencies
- Poisoned package repositories
- Compromised build pipelines

#### Hardware Supply Chain
- Tampered components
- Counterfeit parts
- Firmware manipulation
- Pre-installed malware

#### Service Provider Attacks
- Managed service providers (MSPs)
- Cloud service providers
- Third-party vendors
- SaaS platform compromises

### 4.3 Notable 2025 Supply Chain Attacks

#### Jaguar Land Rover (August 2025)
- **Impact**: Britain's costliest cyberattack ($1.9B expected)
- **Duration**: Production halted for 5 weeks
- **Scope**: 5,000+ businesses in global supply chain affected
- **Attribution**: Scattered Lapsus$ Hunters collective
- **Method**: Exploited third-party supplier software vulnerabilities

#### GitHub Actions Compromise
- **Method**: CVE-2025-30066 vulnerability in tj-actions/changed-files
- **Impact**: CI/CD secrets leaked in public build logs
- **Related**: reviewdog/action-setup also compromised

#### npm Ecosystem Attacks (Shai-Hulud Campaign)
- **August-November 2025**: Coordinated attacks
- **s1ngularity campaign**: 2,349 credentials from 1,079 developer systems
- **PhantomRaven**: 126 malicious packages, 86,000+ installs

#### Salesloft-Drift OAuth Token Theft
- **Method**: Compromised GitHub account
- **Impact**: Hundreds of Salesforce customer instances affected

### 4.4 Attack Vectors

| Vector | Description |
|--------|-------------|
| Package Managers | npm, PyPI, Maven, NuGet compromise |
| CI/CD Pipelines | Build process manipulation |
| OAuth/API Tokens | Credential theft and abuse |
| Third-party Integrations | Exploitation of trust relationships |
| Update Mechanisms | Malicious software updates |

### 4.5 2026 Predictions

**Expected Developments**:
- Attacks targeting additional package managers beyond npm
- Focus on Kubernetes secrets and container registries
- Infrastructure-as-Code platform compromises
- Smart transportation and satellite communications targeting
- Attacks becoming faster, broader, harder to contain

> "2026 will likely bring an escalation of incidents disrupting global logistics and high-tech supply chains, along with more attacks on non-traditional targets."
>
> — Kaspersky 2026 Predictions

### 4.6 Supply Chain Risk Management

**Key Strategies**:
1. Vendor security assessments
2. Software Bill of Materials (SBOM)
3. Dependency scanning and monitoring
4. Zero Trust for third-party access
5. Incident response planning for supply chain events

---

## 5. Insider Threats

Insider threats originate from individuals within an organization who have authorized access to systems and data.

### 5.1 2025-2026 Statistics

| Metric | Value |
|--------|-------|
| Flashpoint observed insider activity | 91,321 instances (2025) |
| Monthly average insider posts | 1,162 |
| Organizations experiencing insider attacks | 76% (up from 66% in 2019) |
| Organizations with zero incidents | Only 17% (down from 40% in 2023) |
| Annual cost per business | $17.4 million |
| Cost per malicious insider incident | $715,366 |
| Average detection time | 81 days |

### 5.2 Types of Insider Threats

| Type | Description | Motivation |
|------|-------------|------------|
| **Malicious Insider** | Intentional harm | Financial gain, revenge, ideology |
| **Negligent Insider** | Careless actions | Convenience, ignorance |
| **Compromised Insider** | Account takeover | External attacker control |
| **Collusive Insider** | Working with external actors | Financial gain |

### 5.3 Detection Challenges

**Key Statistics**:
- **93% of security leaders** say insider threats are as difficult or harder to detect than external attacks
- **Only 23%** express strong confidence in stopping them
- **Only 12%** of organizations have mature predictive risk models
- **Only 12%** of incidents contained in less than 31 days

**Why Detection is Difficult**:
- Legitimate access makes activity appear normal
- Behavior gradually changes over time
- Traditional security tools focus on external threats
- High false positive rates in monitoring

### 5.4 Common Attack Methods

| Method | Prevalence |
|--------|------------|
| Stolen credentials | 22% of all breaches |
| Misdelivery (accidental) | 72% of internal action types |
| Privilege misuse | 89% financially motivated |
| Data exfiltration | Various methods |

### 5.5 AI and Emerging Risks

**Organizational Concerns**:
- **60%** highly concerned about AI misuse by insiders
- **69%** worried about deepfake phishing/social engineering
- **61%** concerned about automated data exfiltration
- **53%** worried about AI-assisted credential abuse

### 5.6 Remote/Hybrid Work Impact

- **75%** identify remote/hybrid workforce as biggest emerging insider risk
- **70%** concerned about insider risk in hybrid workplaces
- **72%** lack full visibility into how employees interact with sensitive data
- **Only 28%** have effective data discovery and classification

### 5.7 Most Targeted Industries

| Industry | Why Targeted |
|----------|--------------|
| Telecommunications | Central role in identity verification, SIM swapping |
| Technology | Valuable IP, access to systems |
| E-commerce | Financial data, customer information |
| Financial Services | Direct monetary access |
| Healthcare | Valuable personal data |

### 5.8 Insider Threat Indicators

**Behavioral Indicators**:
- Working unusual hours without justification
- Accessing systems outside job requirements
- Expressing dissatisfaction or grievances
- Sudden financial changes
- Attempting to bypass security controls

**Technical Indicators**:
- Large data downloads or transfers
- Use of unauthorized storage devices
- Accessing sensitive files atypically
- Failed access attempts to restricted areas
- Use of anonymizing tools

---

## 6. Nation-State Actors

Nation-state cyber actors are government-sponsored threat groups conducting cyber operations to advance national interests.

### 6.1 Primary Nation-State Actors

According to CISA, the primary nation-state cyber threat actors are:

#### China
**Characteristics**:
- Focus on infiltrating critical infrastructure
- Pursuing economic and technological advantage
- Extensive cyber espionage capabilities

**Notable Groups**:
- **APT41**: Espionage and financially motivated operations
- **Mustang Panda**: Targets diplomatic entities and technology sectors
- Custom malware development and deployment

**Targets**: Technology, manufacturing, diplomatic organizations, defense contractors

#### Russia
**Characteristics**:
- Political and military objectives
- Disruptive and destructive capabilities
- Information operations integration

**Notable Groups**:
- **APT28 (Fancy Bear)**: Political entities, elections, government
- **APT29 (Cozy Bear)**: Government and diplomatic targets
- Linked to high-profile attacks including 2016 DNC breach

**Targets**: Government, political organizations, critical infrastructure

#### Iran
**Characteristics**:
- Increasingly sophisticated capabilities
- Suppression of social and political activity
- Regional adversary focus

**Notable Groups**:
- **APT34 (OilRig)**: Middle East focus, governments, financial, energy

**Targets**: Regional governments, energy sector, financial institutions

#### North Korea
**Characteristics**:
- Financial motivation (cryptocurrency theft)
- Intelligence collection
- Supply chain targeting

**Notable Groups**:
- **Lazarus Group**: Active since 2009
- Responsible for WannaCry (2017), multiple cryptocurrency thefts
- Recent supply chain attacks (2024-2025)

**Targets**: Cryptocurrency exchanges, financial institutions, technology companies

### 6.2 Operational Objectives

| Objective | Description | Example |
|-----------|-------------|---------|
| **Espionage** | Intelligence collection | APT campaigns against government agencies |
| **Disruption** | Destabilize operations | Critical infrastructure attacks |
| **Destruction** | Cause physical damage | Stuxnet targeting Iranian nuclear facilities |
| **Financial** | Generate revenue | North Korean cryptocurrency theft |
| **Influence** | Shape public opinion | Election interference operations |

### 6.3 Evolution of Capabilities

**2025-2026 Trends**:
- **Geopolitical escalation**: Eastern Europe, South China Sea, Middle East
- **Beyond espionage**: Active conflict and disruption
- **AI integration**: Enhanced reconnaissance and social engineering
- **Capability diffusion**: APT techniques spreading to criminal groups

### 6.4 Defending Against Nation-State Actors

**CISA Recommendations**:
1. Assess organizational security posture
2. Implement Cybersecurity Performance Goals (CPGs)
3. Focus on resilience and detection
4. Information sharing with government partners
5. Incident response planning

**Key Defensive Measures**:
- Advanced threat detection and hunting
- Network segmentation
- Zero Trust implementation
- Employee awareness training
- Incident response capabilities
- Threat intelligence integration

---

## Summary

### Key Threat Trends (2025-2026)

1. **AI Integration**: Both attackers and defenders increasingly using AI
2. **Supply Chain Focus**: Doubled attack volume, major incidents
3. **Ransomware Evolution**: Higher volume, lower payouts, faster operations
4. **Insider Risks**: Hybrid work expanding attack surface
5. **Nation-State Activity**: Increasing geopolitical motivations
6. **Social Engineering**: AI-powered attacks becoming mainstream

### Threat Priority Matrix

| Threat | Likelihood | Impact | Trend |
|--------|------------|--------|-------|
| Ransomware | High | Critical | Increasing |
| Phishing/Social Engineering | Very High | High | Increasing (AI) |
| Supply Chain | Medium-High | Critical | Increasing |
| Insider Threats | Medium | High | Stable |
| APT/Nation-State | Medium | Critical | Increasing |
| Malware (General) | High | Medium-High | Stable |

### Recommended Actions

1. **Implement Defense in Depth** against all threat vectors
2. **Adopt Zero Trust** to minimize insider and credential-based risks
3. **Secure Supply Chains** with vendor assessments and monitoring
4. **Deploy AI-Powered Detection** to counter AI-powered attacks
5. **Continuous Training** for all employees on social engineering
6. **Incident Response Planning** with regular exercises

---

## Sources

- [Fortinet - Ransomware Statistics 2025](https://www.fortinet.com/resources/cyberglossary/ransomware-statistics)
- [Heimdal Security - Ransomware Statistics 2026](https://heimdalsecurity.com/blog/ransomware-statistics/)
- [Cyble - 10 New Ransomware Groups 2025](https://cyble.com/knowledge-hub/10-new-ransomware-groups-of-2025-threat-trend-2026/)
- [Secureframe - Social Engineering Statistics 2026](https://secureframe.com/blog/social-engineering-statistics)
- [Unit 42 - 2025 Global Incident Response Report](https://unit42.paloaltonetworks.com/2025-unit-42-global-incident-response-report-social-engineering-edition/)
- [CISA - Nation-State Threats](https://www.cisa.gov/topics/cyber-threats-and-advisories/nation-state-cyber-actors)
- [SOCRadar - Top 10 APT Groups 2025](https://socradar.io/blog/top-10-apt-groups-in-2025/)
- [Integrity360 - Biggest Cyber Attacks 2025](https://insights.integrity360.com/the-biggest-cyber-attacks-of-2025-and-what-they-mean-for-2026)
- [Silobreaker - Supply Chain Attacks 2025](https://www.silobreaker.com/blog/cyber-threats/supply-chain-attacks-in-2025-a-month-by-month-summary/)
- [Flashpoint - Insider Threats 2025-2026](https://flashpoint.io/blog/insider-threats-2025-intelligence-2026-strategy/)
- [CrowdStrike - Types of Malware](https://www.crowdstrike.com/en-us/cybersecurity-101/malware/types-of-malware/)
