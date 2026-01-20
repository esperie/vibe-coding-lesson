# Attacker Perspective

> Understanding threat actor motivations, economics, methods, and operational patterns
>
> Last Updated: January 2026

---

## Table of Contents

1. [Threat Actor Taxonomy](#threat-actor-taxonomy)
2. [Financial Crime Use-Cases](#financial-crime-use-cases)
3. [Nation-State Espionage Use-Cases](#nation-state-espionage-use-cases)
4. [Hacktivism Use-Cases](#hacktivism-use-cases)
5. [Insider Threat Scenarios](#insider-threat-scenarios)
6. [Attack Chain Analysis](#attack-chain-analysis)
7. [Cybercrime Economics](#cybercrime-economics)
8. [Attacker Tools and Infrastructure](#attacker-tools-and-infrastructure)
9. [Defensive Intelligence Value](#defensive-intelligence-value)

---

## Threat Actor Taxonomy

### Actor Categories by Motivation

| Category | Primary Motivation | Typical Targets | Sophistication |
|----------|-------------------|-----------------|----------------|
| **Nation-State** | Strategic advantage | Government, CII, IP holders | Very High |
| **Cybercriminal** | Financial gain | Anyone with money/data | Variable |
| **Hacktivist** | Ideological | Perceived opponents | Low-Medium |
| **Insider** | Various (money, revenge) | Own organization | Variable |
| **Script Kiddie** | Notoriety, curiosity | Easy targets | Low |
| **Terrorist** | Fear, disruption | High-impact targets | Variable |

### Actor Sophistication Levels

```
Level 5: Nation-State APT
├── Zero-day development
├── Custom malware
├── Multi-year campaigns
├── Extensive resources
└── Operational security

Level 4: Organized Crime
├── Purchased zero-days
├── Modified malware
├── Months-long campaigns
├── Significant resources
└── Good operational security

Level 3: Advanced Criminal
├── Known exploits
├── Commercial tools
├── Weeks-long campaigns
├── Moderate resources
└── Basic operational security

Level 2: Opportunistic Criminal
├── Automated tools
├── Public exploits
├── Days to weeks
├── Limited resources
└── Poor operational security

Level 1: Script Kiddie
├── Downloaded tools
├── Copy-paste attacks
├── Hours to days
├── Minimal resources
└── Minimal operational security
```

---

## Financial Crime Use-Cases

### Use-Case FC1: Ransomware-as-a-Service Operation

**Threat Actor Profile**:
- **Type**: RaaS affiliate (independent operator using criminal platform)
- **Motivation**: Direct financial profit
- **Capability**: Medium (platform provides tools)
- **Target Selection**: Opportunistic, based on access acquired

**Operational Model**:

```
RaaS Ecosystem
      │
      ├── RaaS Developer (Core Group)
      │   ├── Develops ransomware code
      │   ├── Maintains infrastructure
      │   ├── Provides affiliate portal
      │   └── Takes 20-30% of ransom
      │
      ├── Initial Access Broker (IAB)
      │   ├── Finds vulnerable organizations
      │   ├── Establishes initial foothold
      │   ├── Sells access to affiliates
      │   └── Price: $500-$50,000+ per access
      │
      ├── Affiliate (Attacker)
      │   ├── Purchases/acquires access
      │   ├── Conducts internal reconnaissance
      │   ├── Deploys ransomware
      │   └── Keeps 70-80% of ransom
      │
      └── Money Laundering
          ├── Cryptocurrency mixing
          ├── Mule networks
          └── Cash-out operations
```

**Affiliate Decision-Making**:

| Factor | Consideration | Impact on Targeting |
|--------|---------------|---------------------|
| **Revenue** | Annual revenue of target | Higher = bigger ransom potential |
| **Cyber Insurance** | Does target have coverage? | Insured targets more likely to pay |
| **Sector** | Industry of target | Healthcare, education = softer |
| **Geography** | Location of target | Avoid Russia, CIS countries |
| **Access Quality** | Level of access available | Domain admin = premium |
| **Security Posture** | Defensive capability | Weaker = easier deployment |

**Attack Execution Timeline**:

```
Day 0: Access Acquisition
├── Purchase from IAB ($2,000-$10,000)
├── OR exploit published vulnerability
└── OR successful phishing campaign

Days 1-3: Internal Reconnaissance
├── Network mapping
├── Active Directory enumeration
├── Identify backup systems
├── Locate sensitive data
└── Assess security tools

Days 4-7: Preparation
├── Disable security tools
├── Escalate privileges
├── Deploy persistence mechanisms
├── Exfiltrate sensitive data (for double extortion)
└── Stage ransomware

Day 8: Deployment
├── Destroy/encrypt backups first
├── Deploy ransomware across network
├── Maximize encryption coverage
└── Drop ransom note

Days 8+: Negotiation
├── Victim contacts attacker
├── Ransom negotiation (often 10-50% reduction)
├── Payment in cryptocurrency
├── Decryption keys provided (usually)
└── OR data leaked if no payment
```

**Economics**:

| Metric | Value |
|--------|-------|
| Initial access cost | $500-$50,000 |
| Average ransom demand | $1.32 million |
| Average ransom payment | $1 million |
| Affiliate share | 70-80% |
| Net profit per attack | $700,000-$800,000 |
| Success rate | ~37% victims pay |

---

### Use-Case FC2: Business Email Compromise Gang

**Threat Actor Profile**:
- **Type**: Organized BEC group (often West African-based)
- **Motivation**: Financial fraud
- **Capability**: Medium (social engineering focused)
- **Target Selection**: Companies with international transactions

**Organizational Structure**:

```
BEC Organization
      │
      ├── Leader/Organizer
      │   ├── Strategic direction
      │   ├── Target selection
      │   └── Money management
      │
      ├── Technical Team
      │   ├── Email infrastructure
      │   ├── Domain registration
      │   ├── Account compromise
      │   └── Malware deployment
      │
      ├── Social Engineering Team
      │   ├── Executive impersonation
      │   ├── Vendor impersonation
      │   ├── Conversation management
      │   └── Urgency creation
      │
      └── Money Mule Network
          ├── Domestic mules
          ├── International transfers
          └── Cryptocurrency conversion
```

**Attack Variants**:

| Variant | Technique | Average Loss |
|---------|-----------|--------------|
| **CEO Fraud** | Impersonate executive to finance | $50,000-$500,000 |
| **Vendor Fraud** | Redirect legitimate invoice payments | $100,000-$1,000,000 |
| **Payroll Diversion** | Change direct deposit details | $5,000-$50,000 |
| **Lawyer Impersonation** | Urgent legal transaction | $25,000-$250,000 |
| **Data Theft** | Request employee W-2/tax data | Value in identity theft |

**Success Factors**:

1. **Research Quality**: Better research = more convincing
2. **Timing**: Strike during travel, vacation, busy periods
3. **Urgency**: Create pressure to act quickly
4. **Authority**: Leverage organizational hierarchy
5. **Isolation**: Keep transaction confidential

---

### Use-Case FC3: Cryptocurrency Theft Operation

**Threat Actor Profile**:
- **Type**: Specialized crypto theft group (often North Korean - Lazarus)
- **Motivation**: Financial (state revenue or criminal profit)
- **Capability**: High
- **Target Selection**: Exchanges, DeFi protocols, high-value wallets

**Attack Vectors**:

```
Target Types
      │
      ├── Cryptocurrency Exchanges
      │   ├── Hot wallet compromise
      │   ├── Employee targeting
      │   ├── Smart contract exploitation
      │   └── Potential: $10M-$500M+
      │
      ├── DeFi Protocols
      │   ├── Smart contract vulnerabilities
      │   ├── Flash loan attacks
      │   ├── Oracle manipulation
      │   └── Potential: $1M-$100M+
      │
      ├── Individual Wallets
      │   ├── Phishing for keys
      │   ├── Malware (clipboard hijacking)
      │   ├── SIM swapping for 2FA bypass
      │   └── Potential: $10K-$10M
      │
      └── Bridge Protocols
          ├── Cross-chain vulnerabilities
          ├── Validator compromise
          └── Potential: $100M-$500M+
```

**Lazarus Group Tactics**:

| Phase | Technique | Example |
|-------|-----------|---------|
| **Targeting** | LinkedIn reconnaissance | Identify exchange employees |
| **Contact** | Fake job opportunity | "Great opportunity at competitor" |
| **Delivery** | Malicious document | "Job description" with macro |
| **Compromise** | Remote access established | Corporate network access |
| **Lateral Movement** | Target hot wallet systems | HSM access, signing keys |
| **Theft** | Unauthorized transfers | Multiple wallets, fast movement |
| **Laundering** | Mixing, chain-hopping | Tornado Cash, bridges |

**North Korean Operations Scale**:
- Estimated $3+ billion stolen (2017-2024)
- Funds critical regime revenue source
- Sanctions evasion through crypto
- Sophisticated money laundering

---

### Use-Case FC4: Data Broker / Credential Seller

**Threat Actor Profile**:
- **Type**: Data theft and resale operation
- **Motivation**: Monetization of stolen data
- **Capability**: Variable
- **Target Selection**: High-volume data stores

**Data Monetization Ecosystem**:

```
Data Sources
├── Direct breaches
├── Phishing campaigns
├── Malware (infostealers)
├── Purchased from other actors
└── Insider theft

      │
      ▼

Data Processing
├── Deduplication
├── Validation
├── Categorization
├── Pricing
└── Packaging

      │
      ▼

Sale Channels
├── Dark web markets
├── Private forums
├── Direct sales
├── Subscription services
└── Bulk deals
```

**Data Pricing (2025)**:

| Data Type | Price Range | Notes |
|-----------|-------------|-------|
| Email/password combo | $0.50-$10 | Volume discounts |
| Credit card (with CVV) | $10-$100 | Fresh = premium |
| Bank account credentials | $50-$500 | Balance dependent |
| Full identity package | $15-$200 | Name, address, SSN/NRIC, DOB |
| Medical records | $50-$500 | High value for fraud |
| Corporate credentials | $500-$50,000 | Access dependent |

**Infostealer Malware Operations**:

Common strains in 2025:
- RedLine Stealer
- Raccoon Stealer
- Vidar
- LummaC2

Capabilities:
- Browser credential extraction
- Cryptocurrency wallet theft
- Cookie theft (session hijacking)
- Form data capture
- Screenshot capture

---

## Nation-State Espionage Use-Cases

### Use-Case NS1: Long-Term Strategic Intelligence Collection

**Threat Actor Profile**:
- **Type**: Nation-state intelligence agency APT
- **Motivation**: Strategic/military intelligence
- **Capability**: Very high
- **Target Selection**: Government, defense, policy institutions

**Operational Characteristics**:

```
Planning Phase (Months)
├── Target selection based on intelligence requirements
├── Multi-source reconnaissance
├── Access path identification
├── Operational security planning
└── Tool and infrastructure preparation

Access Phase (Weeks-Months)
├── Multiple entry attempts
├── Spear-phishing campaigns
├── Supply chain compromise
├── Zero-day exploitation
└── Human intelligence support

Persistence Phase (Years)
├── Multiple backdoors
├── Living off the land
├── Periodic check-ins
├── Adaptation to security changes
└── Continuous access maintenance

Collection Phase (Ongoing)
├── Targeted document collection
├── Communication monitoring
├── Credential harvesting
├── Lateral movement as needed
└── New target identification

Exfiltration (Continuous)
├── Encrypted channels
├── Legitimate service abuse
├── Low and slow transfer
├── Multiple exfil paths
└── Data staging and batching
```

**Intelligence Requirements (China Example)**:

| Priority | Target Information | Use |
|----------|-------------------|-----|
| **Strategic** | Military capabilities, alliances | Policy planning |
| **Economic** | Trade negotiations, industrial policy | Competitive advantage |
| **Technology** | R&D, intellectual property | Development acceleration |
| **Political** | Decision-making, leadership views | Influence operations |
| **Operational** | Security practices, personnel | Future targeting |

---

### Use-Case NS2: Technology Acquisition Campaign

**Threat Actor Profile**:
- **Type**: Nation-state economic espionage unit
- **Motivation**: Technology transfer
- **Capability**: High
- **Target Selection**: Tech companies, R&D facilities, universities

**Target Technologies (Singapore/ASEAN Context)**:

| Sector | Target Technologies | Strategic Value |
|--------|---------------------|-----------------|
| **Semiconductors** | Design processes, manufacturing | Critical supply chain |
| **Aerospace** | Materials, systems, designs | Defense/commercial |
| **AI/ML** | Algorithms, training data | Dual-use capability |
| **Biotech** | Research, pharmaceutical processes | Health security |
| **Maritime** | Shipbuilding, autonomous systems | Regional power |

**Multi-Vector Approach**:

```
Technical Operations
├── Network intrusion
├── Email compromise
├── Cloud storage access
└── Code repository theft

Human Operations
├── Insider recruitment
├── Academic partnerships
├── Joint venture access
├── "Talent programs"

Legal/Gray Zone
├── Investment in targets
├── Acquisition attempts
├── Joint ventures
├── Research collaboration
```

---

### Use-Case NS3: Pre-Positioning for Disruption

**Threat Actor Profile**:
- **Type**: Nation-state military/intelligence cyber unit
- **Motivation**: Capability development for potential conflict
- **Capability**: Very high
- **Target Selection**: Critical infrastructure

**Strategic Logic**:

> Maintain persistent access to adversary critical infrastructure to enable disruption during future crisis or conflict, without triggering current retaliation.

**Operational Pattern**:

```
Phase 1: Access Establishment
├── Target critical infrastructure sectors
├── Exploit edge devices (firewalls, VPNs)
├── Supply chain compromise
├── Establish multiple access paths
└── Avoid detection at all costs

Phase 2: Deep Persistence
├── Map internal networks
├── Understand operational technology
├── Identify critical systems
├── Position for action
└── Test access periodically

Phase 3: Capability Maintenance
├── Adapt to security changes
├── Maintain redundant access
├── Update understanding
├── Wait for activation order
└── Potentially years of dormancy

Phase 4 (Contingency): Activation
├── Disruption on command
├── Data destruction
├── OT manipulation
├── Cascading failures
└── Deny, degrade, destroy
```

**Volt Typhoon Pattern**:
- Targeting US critical infrastructure
- Pre-positioning in energy, water, communications
- Minimal malware (living off the land)
- Extended dwell times
- Positioned for future conflict scenarios

---

## Hacktivism Use-Cases

### Use-Case H1: Ideological Website Defacement

**Threat Actor Profile**:
- **Type**: Hacktivist collective or individual
- **Motivation**: Political/ideological message
- **Capability**: Low-Medium
- **Target Selection**: Symbolic targets related to cause

**Typical Targets**:

| Cause | Target Types | Examples |
|-------|-------------|----------|
| **Environmental** | Oil companies, manufacturers | Corporate websites |
| **Political** | Government, political parties | Agency websites |
| **Social Justice** | Corporations, institutions | Company homepages |
| **Geopolitical** | Foreign governments, embassies | Official sites |

**Attack Pattern**:

```
Target Selection
├── Symbolic value to cause
├── Vulnerability assessment
├── Low security preferred
└── Maximum visibility desired

Exploitation
├── Web application vulnerability
├── CMS exploitation
├── Credential stuffing
└── SQL injection

Defacement
├── Replace homepage
├── Post political message
├── Claim attribution
└── Document and publicize

Aftermath
├── Social media announcement
├── Media coverage sought
├── Potential criminal investigation
└── Site restored within hours
```

---

### Use-Case H2: DDoS Campaign

**Threat Actor Profile**:
- **Type**: Hacktivist group with DDoS capability
- **Motivation**: Disruption, protest
- **Capability**: Medium (often botnet rental)
- **Target Selection**: Organizations related to cause

**DDoS-as-a-Service**:

```
Attacker obtains DDoS capability
├── Botnet rental ($50-$500/day)
├── Stresser/booter service ($10-$100)
├── Own botnet (rare for hacktivists)
└── Volunteer network (LOIC-style)

Attack Execution
├── Target selection
├── Attack type selection (volumetric, application, etc.)
├── Attack duration
└── Often timed for symbolic dates/events

Impact
├── Service unavailable
├── Reputational damage
├── Operational disruption
└── Usually temporary
```

---

### Use-Case H3: Data Leak for Exposure

**Threat Actor Profile**:
- **Type**: Hacktivist with data exfiltration capability
- **Motivation**: Expose perceived wrongdoing
- **Capability**: Medium-High
- **Target Selection**: Organizations with "secrets to expose"

**Leak Operation**:

```
Intrusion
├── Network compromise
├── Database access
├── Email access
└── Document repositories

Data Selection
├── Evidence of wrongdoing (perceived)
├── Embarrassing communications
├── Financial impropriety
├── Hypocrisy exposure
└── Personal information (controversial)

Publication
├── Leak site (dedicated or third-party)
├── Journalist contacts
├── Social media distribution
└── Searchable database creation

Objectives
├── Public outrage
├── Accountability
├── Policy change
├── Personal harm to targets (in some cases)
└── Notoriety
```

---

## Insider Threat Scenarios

### Use-Case I1: Financially Motivated Data Theft

**Threat Actor Profile**:
- **Type**: Employee with data access
- **Motivation**: Financial gain
- **Capability**: High (legitimate access)
- **Target**: Customer data, trade secrets

**Insider Theft Pattern**:

```
Opportunity Recognition
├── Employee realizes data value
├── Access to valuable information
├── Perceived low detection risk
└── Financial pressure or opportunity

Data Acquisition
├── Authorized access used
├── Gradual collection over time
├── Personal device transfer
├── Cloud storage upload
└── Email to personal accounts

Monetization
├── Sell to competitors
├── Sell on dark web
├── Use for new employment
├── Start competing business
└── Extort employer

Detection (Often Late)
├── Unusual access patterns
├── Data loss prevention alerts
├── Whistleblower tips
├── Post-employment discovery
└── Competitor suddenly has information
```

**Warning Signs**:
- Accessing data outside job scope
- Working unusual hours
- Large downloads/transfers
- Expressed dissatisfaction
- Financial difficulties
- Resignation followed by data access

---

### Use-Case I2: Disgruntled Employee Sabotage

**Threat Actor Profile**:
- **Type**: Current or former employee
- **Motivation**: Revenge, grievance
- **Capability**: High (system knowledge)
- **Target**: Employer's systems and reputation

**Sabotage Actions**:

| Action | Trigger | Impact |
|--------|---------|--------|
| **Data Destruction** | Termination | Business disruption |
| **System Sabotage** | Perceived unfair treatment | Operational impact |
| **Logic Bomb** | Departure | Delayed damage |
| **Credential Sharing** | Anger at employer | External attack enabled |
| **Data Leak** | Whistleblowing (perceived) | Reputational damage |

**Time Bomb Scenario**:

```
Employee Departure
├── Maintains hidden access
├── OR plants logic bomb before leaving
├── OR shares credentials with external actor
└── Appears to leave normally

Delay Period
├── Weeks to months
├── Access maintained covertly
├── Logic bomb waiting to trigger
└── Organization unaware

Activation
├── Timed trigger activates
├── OR remote command
├── Data destroyed
├── Systems disrupted
└── Attribution difficult initially
```

---

### Use-Case I3: Recruited Insider

**Threat Actor Profile**:
- **Type**: Employee recruited by external actor
- **Motivation**: Financial (payment from external party)
- **Capability**: Varies by position
- **Target**: Specific information or access

**Recruitment Pattern (Nation-State)**:

```
Identification
├── Employee with valuable access identified
├── Financial vulnerabilities assessed
├── Personal vulnerabilities assessed
├── Approach method planned
└── Cover story developed

Approach
├── Social contact established
├── Relationship built over time
├── Gradual requests begin
├── Increasing value of requests
└── Relationship becomes dependency

Tasking
├── Specific information requests
├── Access provision
├── Internal information about security
├── Credential sharing
└── Physical access facilitation

Control
├── Payments for services
├── Potential blackmail (if compromising)
├── Continued relationship
└── Expanding requests
```

**Insider Threat Statistics (2025)**:
- 76% of organizations experienced insider attacks
- Average cost per malicious insider incident: $715,366
- Average detection time: 81 days
- Only 17% of organizations had zero incidents

---

## Attack Chain Analysis

### Generalized Attack Kill Chain

```
1. RECONNAISSANCE
   ├── Passive: OSINT, social media, public records
   └── Active: Scanning, probing, social engineering

2. WEAPONIZATION
   ├── Exploit selection/development
   ├── Payload creation
   └── Delivery mechanism preparation

3. DELIVERY
   ├── Phishing (email, SMS, voice)
   ├── Watering hole
   ├── Supply chain
   └── Direct exploitation

4. EXPLOITATION
   ├── Vulnerability exploitation
   ├── Social engineering success
   └── Credential use

5. INSTALLATION
   ├── Malware deployment
   ├── Persistence mechanisms
   └── Backdoor establishment

6. COMMAND & CONTROL
   ├── C2 communication established
   ├── Remote access confirmed
   └── Operational control gained

7. ACTIONS ON OBJECTIVES
   ├── Data exfiltration
   ├── Lateral movement
   ├── Privilege escalation
   ├── Ransomware deployment
   └── Destruction/disruption
```

### MITRE ATT&CK Mapping Example

**Ransomware Attack Chain**:

| Phase | ATT&CK Tactic | Techniques |
|-------|---------------|------------|
| **Entry** | Initial Access | T1566 (Phishing), T1190 (Exploit Public-Facing) |
| **Foothold** | Execution | T1059 (Command and Scripting), T1204 (User Execution) |
| **Persist** | Persistence | T1547 (Boot/Logon Autostart), T1078 (Valid Accounts) |
| **Escalate** | Privilege Escalation | T1068 (Exploitation for Privilege Escalation) |
| **Move** | Lateral Movement | T1021 (Remote Services), T1570 (Lateral Tool Transfer) |
| **Collect** | Collection | T1005 (Data from Local System), T1560 (Archive Collected Data) |
| **Exfil** | Exfiltration | T1041 (Exfiltration Over C2), T1567 (Exfiltration to Cloud) |
| **Impact** | Impact | T1486 (Data Encrypted for Impact), T1490 (Inhibit System Recovery) |

---

## Cybercrime Economics

### Market Statistics (2025)

| Metric | Value |
|--------|-------|
| **Global Cybercrime Costs** | $10.5 trillion annually |
| **Dark Web Marketplaces** | 37+ active |
| **Dark Web Annual Revenue** | $3.2 billion |
| **Stolen Credentials Available** | 15 billion |
| **RaaS Average Revenue** | $1-10 million per group annually |

### Attack ROI Comparison

| Attack Type | Investment | Potential Return | ROI |
|-------------|------------|------------------|-----|
| **Phishing Campaign** | $500-$5,000 | $10,000-$100,000 | Very High |
| **Ransomware (Affiliate)** | $5,000-$50,000 | $100,000-$1,000,000 | High |
| **BEC** | $1,000-$10,000 | $50,000-$500,000 | High |
| **Card Fraud** | $100-$1,000 | $1,000-$10,000 | Medium |
| **Zero-Day Development** | $100,000-$1,000,000 | Variable | Low (for criminals) |

### Criminal Service Pricing

| Service | Price | Notes |
|---------|-------|-------|
| **DDoS-for-hire** | $10-$500/day | Subscription available |
| **RaaS Access** | Free-30% cut | Affiliate model |
| **Malware (off-shelf)** | $50-$5,000 | Depending on capability |
| **Initial Access** | $500-$50,000 | Quality dependent |
| **Money Laundering** | 20-50% of value | Risk-based pricing |
| **Bulletproof Hosting** | $100-$1,000/month | No takedowns |

---

## Attacker Tools and Infrastructure

### Common Attacker Tools (2025)

**Reconnaissance**:
- Maltego (OSINT)
- Shodan (Internet scanning)
- LinkedIn (social engineering)
- Google dorking

**Exploitation**:
- Metasploit
- Cobalt Strike
- Covenant
- Sliver

**Post-Exploitation**:
- Mimikatz (credential theft)
- BloodHound (AD mapping)
- PowerShell Empire
- Impacket

**C2 Infrastructure**:
- Cobalt Strike Team Servers
- Sliver C2
- Mythic
- Custom frameworks

**Malware Families**:
- Ransomware: LockBit, Qilin, Akira
- RATs: AsyncRAT, Quasar, njRAT
- Stealers: RedLine, Raccoon, LummaC2

### Infrastructure Patterns

```
Attacker Infrastructure
      │
      ├── Domain Infrastructure
      │   ├── Phishing domains
      │   ├── Lookalike domains
      │   └── C2 domains
      │
      ├── Server Infrastructure
      │   ├── Bulletproof hosting
      │   ├── Compromised servers
      │   └── Cloud services abuse
      │
      ├── Anonymization
      │   ├── VPNs (often compromised)
      │   ├── Tor network
      │   ├── Proxy chains
      │   └── Compromised infrastructure
      │
      └── Communication
          ├── Encrypted channels
          ├── Legitimate service abuse (Telegram, Discord)
          └── Custom protocols
```

---

## Defensive Intelligence Value

### Using Attacker Knowledge for Defense

| Knowledge Area | Defensive Application |
|----------------|----------------------|
| **Attack Economics** | Prioritize high-ROI attack prevention |
| **TTPs** | Detection rule development |
| **Target Selection** | Self-assessment of attractiveness |
| **Timeline** | Incident response planning |
| **Tools** | Signature and behavior detection |
| **Infrastructure** | Threat intelligence blocking |

### Actionable Intelligence from Attacker Perspective

1. **Why would attackers target us?**
   - Assess organizational value to different actor types
   - Identify what makes you attractive/vulnerable

2. **How would they attack?**
   - Map likely attack paths based on actor capabilities
   - Identify weakest entry points

3. **What would they want?**
   - Identify crown jewel assets
   - Understand data/access value

4. **When would they strike?**
   - Recognize high-risk periods
   - Plan enhanced monitoring

5. **How can we detect them?**
   - Map TTPs to detection opportunities
   - Focus on high-value detection points

---

*Return to [README.md](./README.md) for navigation*
