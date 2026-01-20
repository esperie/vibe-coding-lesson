# Adversary Simulation

> Comprehensive documentation for breach and attack simulation platforms, purple team exercises, MITRE ATT&CK-based testing, and continuous security validation.

**Last Updated**: January 2026

---

## Table of Contents

1. [Breach and Attack Simulation (BAS) Platforms](#breach-and-attack-simulation-bas-platforms)
2. [Purple Team Exercises](#purple-team-exercises)
3. [MITRE ATT&CK-Based Testing](#mitre-attck-based-testing)
4. [Threat Intelligence Integration](#threat-intelligence-integration)
5. [Continuous Security Validation](#continuous-security-validation)
6. [Exercise Planning and Execution](#exercise-planning-and-execution)
7. [Singapore Government Exercise Integration](#singapore-government-exercise-integration)

---

## Breach and Attack Simulation (BAS) Platforms

### Overview

Breach and Attack Simulation platforms automate the testing of security controls by safely executing attack techniques against production environments. This provides continuous validation of defensive capabilities.

### Enterprise BAS Platforms

#### AttackIQ

**Description**: Leading BAS platform deeply aligned with MITRE ATT&CK framework.

| Aspect | Details |
|--------|---------|
| **Focus** | MITRE ATT&CK-centric security optimization |
| **Deployment** | Agents deployed across environment |
| **Coverage** | Network, endpoint, cloud, email |
| **Framework** | Primary MITRE ATT&CK alignment |

**Core Capabilities**:

| Capability | Description |
|------------|-------------|
| **Attack Scenarios** | Pre-built and custom attack scenarios |
| **Control Validation** | Tests security controls against attacks |
| **Coverage Analysis** | Identifies defensive gaps |
| **Remediation** | Prioritized recommendations |
| **Reporting** | Executive and technical dashboards |

**MITRE ATT&CK Integration**:

| Feature | Description |
|---------|-------------|
| **TTP Library** | Comprehensive technique coverage |
| **Navigator Export** | ATT&CK Navigator compatible |
| **Gap Analysis** | Techniques not covered by controls |
| **Threat Mapping** | Align with specific threat actors |

**Strengths**:
- Deep ATT&CK integration
- MITRE Engenuity partnership
- Extensive scenario library
- Strong analytics

**Considerations**:
- Enterprise pricing
- Agent deployment required
- Learning curve for full utilization

**Government Use Case**: MITRE ATT&CK coverage mapping, control validation, CIDeX preparation.

---

#### SafeBreach

**Description**: Continuous security validation with extensive attack playbook.

| Aspect | Details |
|--------|---------|
| **Deployment** | Cloud-based management, local simulators |
| **Coverage** | Network, endpoint, email, cloud, data |
| **Playbook** | 30,000+ attack methods |
| **Intelligence** | Integrates threat intelligence feeds |

**Core Capabilities**:

| Capability | Description |
|------------|-------------|
| **Attack Playbooks** | Extensive pre-built scenarios |
| **Kill Chain Coverage** | Full attack lifecycle |
| **Prioritization** | Risk-based remediation guidance |
| **Hacker's Playbook** | Real-world attack techniques |

**Strengths**:
- Extensive attack library
- Continuous validation
- Good visualization
- Strong remediation guidance

**Considerations**:
- Simulator deployment needed
- Enterprise pricing

**Government Use Case**: Continuous security validation, threat-informed defense.

---

#### Cymulate

**Description**: Extended security validation platform with broad attack coverage.

| Aspect | Details |
|--------|---------|
| **Deployment** | SaaS with on-premises agents |
| **Coverage** | Email, web, endpoint, network, data |
| **Updates** | Immediate threat updates |
| **Modules** | Multiple attack vectors |

**Assessment Modules**:

| Module | Target |
|--------|--------|
| **Email Gateway** | Phishing, malware delivery |
| **Web Gateway** | URL filtering, web threats |
| **Web Application Firewall** | WAF bypass testing |
| **Endpoint Security** | EDR/AV validation |
| **Data Exfiltration** | DLP effectiveness |
| **Lateral Movement** | Network segmentation |
| **Phishing Awareness** | Human factor testing |

**Strengths**:
- Broad attack vector coverage
- Rapid threat updates
- User-friendly interface
- Phishing awareness module

**Considerations**:
- Module-based pricing
- Some modules require specific setup

**Government Use Case**: Comprehensive control validation, phishing resilience.

---

#### Picus Security

**Description**: Security control validation platform with mitigation focus.

| Aspect | Details |
|--------|---------|
| **Approach** | Attack simulation with mitigation mapping |
| **Integration** | SIEM, SOAR, EDR, firewall |
| **Coverage** | Network, endpoint, email |
| **Mitigation** | Specific remediation steps |

**Strengths**:
- Strong mitigation guidance
- Vendor-specific recommendations
- Good SIEM integration
- Threat intelligence integration

**Considerations**:
- Best with supported integrations
- Setup complexity

**Government Use Case**: Security stack optimization, detection engineering.

---

#### Mandiant Security Validation (formerly Verodin)

**Description**: Security effectiveness testing with Mandiant threat intelligence.

| Aspect | Details |
|--------|---------|
| **Intelligence** | Mandiant threat intelligence integration |
| **Coverage** | Network, endpoint, cloud |
| **Approach** | Evidence-based security measurement |

**Strengths**:
- Mandiant intelligence integration
- Strong APT coverage
- Evidence-based metrics
- Professional services support

**Considerations**:
- Premium pricing
- Mandiant ecosystem dependency

**Government Use Case**: APT-focused validation, threat intelligence-driven testing.

---

### BAS Platform Comparison

| Platform | ATT&CK Depth | Coverage Breadth | Intelligence | Ease of Use | Government Fit |
|----------|-------------|------------------|--------------|-------------|----------------|
| AttackIQ | Excellent | Good | Good | Moderate | Excellent |
| SafeBreach | Good | Excellent | Good | Good | Good |
| Cymulate | Good | Excellent | Good | Excellent | Good |
| Picus | Good | Good | Good | Good | Good |
| Mandiant SV | Excellent | Good | Excellent | Moderate | Excellent |

---

## Purple Team Exercises

### Overview

Purple teaming combines red team (offensive) and blue team (defensive) operations in a collaborative environment to improve overall security posture.

### Purple Team Models

#### Traditional Model

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    TRADITIONAL PURPLE TEAM MODEL                            │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│    ┌───────────────┐                           ┌───────────────┐            │
│    │   RED TEAM    │      Collaboration        │   BLUE TEAM   │            │
│    │               │◄─────────────────────────►│               │            │
│    │  • Attack     │                           │  • Detect     │            │
│    │  • Exploit    │                           │  • Respond    │            │
│    │  • Persist    │                           │  • Remediate  │            │
│    └───────────────┘                           └───────────────┘            │
│            │                                           │                     │
│            └─────────────────┬─────────────────────────┘                    │
│                              │                                               │
│                              ▼                                               │
│                    ┌───────────────────┐                                    │
│                    │   PURPLE TEAM     │                                    │
│                    │   COORDINATOR     │                                    │
│                    │                   │                                    │
│                    │  • Plan scenarios │                                    │
│                    │  • Facilitate     │                                    │
│                    │  • Document       │                                    │
│                    │  • Measure        │                                    │
│                    └───────────────────┘                                    │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

#### Integrated Model

| Phase | Red Team | Blue Team | Joint |
|-------|----------|-----------|-------|
| **Planning** | Attack scenarios | Detection strategy | Exercise objectives |
| **Execution** | Execute attacks | Monitor and detect | Real-time debrief |
| **Analysis** | Attack success/failure | Detection rate | Gap identification |
| **Improvement** | Refine techniques | Enhance detection | Update playbooks |

### Purple Team Exercise Framework

#### Exercise Objectives

| Objective Type | Examples |
|----------------|----------|
| **Detection** | Validate SIEM rules, EDR alerts |
| **Response** | Test incident response procedures |
| **Prevention** | Verify blocking controls |
| **Recovery** | Test containment and recovery |
| **Process** | Validate communication, escalation |

#### Exercise Phases

##### Phase 1: Planning

| Activity | Output |
|----------|--------|
| Define objectives | Exercise scope document |
| Select techniques | ATT&CK technique list |
| Develop scenarios | Attack playbook |
| Brief participants | Pre-exercise briefing |

##### Phase 2: Execution

| Activity | Description |
|----------|-------------|
| Attack execution | Red team executes planned attacks |
| Detection monitoring | Blue team monitors for alerts |
| Real-time debrief | Discuss each technique immediately |
| Documentation | Record outcomes for each step |

##### Phase 3: Analysis

| Activity | Output |
|----------|--------|
| Gap identification | Techniques not detected |
| Detection analysis | True/false positive rates |
| Response assessment | Time to detect/respond |
| Control effectiveness | What worked, what didn't |

##### Phase 4: Improvement

| Activity | Output |
|----------|--------|
| Detection engineering | New/improved SIEM rules |
| Process updates | Updated playbooks |
| Training | Skill development plan |
| Re-testing | Validation of improvements |

### Purple Team Metrics

#### Detection Metrics

| Metric | Description | Target |
|--------|-------------|--------|
| **Detection Rate** | % of attacks detected | >90% |
| **Mean Time to Detect (MTTD)** | Average detection time | <15 minutes |
| **False Positive Rate** | % of false alerts | <5% |
| **Alert Fidelity** | Quality of alert information | High |

#### Response Metrics

| Metric | Description | Target |
|--------|-------------|--------|
| **Mean Time to Respond (MTTR)** | Time from detection to containment | <1 hour |
| **Containment Success** | % of attacks successfully contained | >95% |
| **Escalation Accuracy** | Correct escalation decisions | >95% |

---

## MITRE ATT&CK-Based Testing

### MITRE ATT&CK v18 Overview

Current version as of October 2025:

| Domain | Tactics | Techniques | Sub-Techniques |
|--------|---------|------------|----------------|
| Enterprise | 14 | 216 | 475 |
| Mobile | 12 | 77 | 47 |
| ICS | 12 | 83 | - |

Reference: [Defense Frameworks - MITRE ATT&CK](/docs/01-research/01-fundamentals/03-defense-frameworks.md#2-mitre-attck)

### ATT&CK-Based Testing Methodology

#### Step 1: Threat Identification

Identify relevant threat actors for Singapore government:

| Threat Actor | Primary Tactics | Priority |
|--------------|-----------------|----------|
| **UNC3886** | Initial Access, Persistence, Defense Evasion | Critical |
| **Volt Typhoon** | Living off the Land, Persistence | Critical |
| **Mustang Panda** | Spear Phishing, C2 | High |
| **APT41** | Web Compromise, Supply Chain | High |
| **Lazarus Group** | Spear Phishing, Cryptocurrency | Medium |

Reference: [Singapore Threats](/docs/01-research/05-singapore-ecosystem/05-threats-focus-areas.md)

#### Step 2: Technique Prioritization

Map threat actor TTPs to ATT&CK:

| Tactic | Priority Techniques | Rationale |
|--------|-------------------|-----------|
| **Initial Access** | T1566 (Phishing), T1190 (Exploit Public-Facing) | Primary attack vectors |
| **Execution** | T1059 (Command and Script), T1204 (User Execution) | Common execution methods |
| **Persistence** | T1547 (Boot/Logon), T1053 (Scheduled Task) | APT persistence methods |
| **Defense Evasion** | T1070 (Indicator Removal), T1036 (Masquerading) | Living off the Land |
| **Credential Access** | T1003 (OS Credential Dumping), T1558 (Kerberos) | Lateral movement enabler |
| **Lateral Movement** | T1021 (Remote Services), T1570 (Lateral Tool Transfer) | Network spread |
| **C2** | T1071 (Application Layer Protocol), T1572 (Protocol Tunneling) | C2 communication |
| **Exfiltration** | T1048 (Exfiltration Over Alternative Protocol) | Data theft |

#### Step 3: Detection Coverage Assessment

Map current detection capabilities:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    ATT&CK COVERAGE HEAT MAP (Example)                        │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  Tactic              Coverage    Gap Analysis                               │
│  ─────────────────────────────────────────────────────────────────          │
│  Initial Access      ████████░░  80%   Good phishing detection              │
│  Execution           ██████░░░░  60%   Need script monitoring               │
│  Persistence         █████░░░░░  50%   Registry monitoring gap              │
│  Priv Escalation     ████░░░░░░  40%   Limited local escalation detection   │
│  Defense Evasion     ███░░░░░░░  30%   Significant gaps                     │
│  Credential Access   ██████░░░░  60%   LSASS monitoring needed              │
│  Discovery           ████████░░  80%   Good AD query detection              │
│  Lateral Movement    █████░░░░░  50%   RDP monitoring gap                   │
│  Collection          ████░░░░░░  40%   Limited file monitoring              │
│  C2                  ███████░░░  70%   DNS tunneling gap                    │
│  Exfiltration        █████░░░░░  50%   Cloud exfil gap                      │
│  Impact              ████████░░  80%   Ransomware detection good            │
│                                                                              │
│  Legend: █ = Covered  ░ = Gap                                               │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

#### Step 4: Testing Execution

Execute tests against identified gaps:

| Test Category | Tools | Focus |
|---------------|-------|-------|
| **Atomic Tests** | Atomic Red Team | Individual technique testing |
| **Scenario Tests** | BAS platforms | Multi-technique chains |
| **Full Simulation** | Red team operations | Realistic APT simulation |

### ATT&CK Testing Tools

#### Atomic Red Team

**Description**: Library of small, portable tests mapped to ATT&CK.

| Aspect | Details |
|--------|---------|
| **Type** | Open source (Red Canary) |
| **Coverage** | 700+ tests |
| **Execution** | PowerShell, Bash, manual |
| **Purpose** | Individual technique validation |

**Usage**:

```powershell
# Example: Test T1003.001 (LSASS Memory)
Invoke-AtomicTest T1003.001
```

**Strengths**:
- Free and open source
- Extensive coverage
- Easy to execute
- Well-documented

**Considerations**:
- Individual tests only
- May trigger alerts (intended)
- Requires test environment

**Government Use Case**: Detection rule validation, SOC training.

---

#### MITRE Caldera

**Description**: Automated adversary emulation platform from MITRE.

| Aspect | Details |
|--------|---------|
| **Type** | Open source (MITRE) |
| **Capabilities** | Automated adversary emulation |
| **Agents** | Cross-platform agents |
| **Planning** | Automated attack planning |

**Strengths**:
- Official MITRE tool
- Automated operations
- Extensible
- Free

**Considerations**:
- Setup complexity
- Agent management
- Limited evasion

**Government Use Case**: Automated ATT&CK testing, exercise automation.

---

#### MITRE ATT&CK Navigator

**Description**: Web-based tool for ATT&CK matrix visualization.

| Aspect | Details |
|--------|---------|
| **Type** | Open source (MITRE) |
| **Purpose** | Coverage visualization |
| **Export** | JSON, SVG, Excel |

**Use Cases**:
- Coverage mapping
- Gap visualization
- Exercise planning
- Reporting

---

## Threat Intelligence Integration

### Overview

Integrating threat intelligence into adversary simulation ensures testing reflects real-world threats facing Singapore.

### Intelligence Sources

#### Government Sources

| Source | Type | Relevance |
|--------|------|-----------|
| **CSA Advisories** | National | Singapore-specific threats |
| **CISA Advisories** | International | APT TTPs, vulnerabilities |
| **NCSC (UK)** | International | Five Eyes intelligence |
| **ACSC (Australia)** | Regional | Regional threat landscape |

#### Commercial Intelligence

| Provider | Strengths | Government Fit |
|----------|-----------|----------------|
| **Mandiant** | APT expertise, incident response | Excellent |
| **CrowdStrike** | Adversary tracking | Excellent |
| **Recorded Future** | Open source aggregation | Good |
| **Intel471** | Underground monitoring | Good |

### Intelligence-Driven Simulation

#### Process Flow

```
┌─────────────────────────────────────────────────────────────────────────────┐
│              INTELLIGENCE-DRIVEN ADVERSARY SIMULATION                        │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│  ┌─────────────┐   ┌─────────────┐   ┌─────────────┐   ┌─────────────┐     │
│  │   Threat    │──>│    TTP      │──>│  Simulation │──>│    Gap      │     │
│  │Intelligence │   │  Extraction │   │  Execution  │   │  Analysis   │     │
│  └─────────────┘   └─────────────┘   └─────────────┘   └─────────────┘     │
│        │                │                  │                  │             │
│        ▼                ▼                  ▼                  ▼             │
│  • APT reports    • Map to ATT&CK   • BAS platform    • Detection gaps     │
│  • ISAC feeds     • Identify TTPs   • Red team        • Process gaps       │
│  • Vendor intel   • Prioritize      • Atomic tests    • Remediation        │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

#### Threat Profile Example: UNC3886

Based on research from [Singapore Threats](/docs/01-research/05-singapore-ecosystem/05-threats-focus-areas.md):

| Attribute | Value |
|-----------|-------|
| **Attribution** | State-sponsored (China-nexus) |
| **Targets** | Critical infrastructure, government |
| **Primary TTPs** | Zero-day exploitation, LoTL techniques |
| **Tools** | Custom implants, legitimate tools |

**Simulation Priority**:

| ATT&CK Technique | UNC3886 Usage | Test Priority |
|------------------|---------------|---------------|
| T1190 (Exploit Public-Facing) | Zero-day exploitation | Critical |
| T1059 (Command and Script) | PowerShell, Python | High |
| T1036 (Masquerading) | Living off the Land | High |
| T1071 (Application Layer Protocol) | HTTPS C2 | High |
| T1003 (OS Credential Dumping) | Credential harvesting | Critical |

---

## Continuous Security Validation

### Overview

Continuous security validation moves from periodic testing to ongoing assessment, providing real-time security posture awareness.

### Continuous Validation Framework

```
┌─────────────────────────────────────────────────────────────────────────────┐
│              CONTINUOUS SECURITY VALIDATION FRAMEWORK                        │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│                    ┌───────────────────────────────┐                        │
│                    │     Continuous Monitoring      │                        │
│                    │    (24/7 Automated Testing)    │                        │
│                    └───────────────┬───────────────┘                        │
│                                    │                                         │
│              ┌─────────────────────┼─────────────────────┐                  │
│              │                     │                     │                  │
│              ▼                     ▼                     ▼                  │
│    ┌─────────────────┐   ┌─────────────────┐   ┌─────────────────┐         │
│    │   Scheduled     │   │   Event-Driven  │   │   Ad-Hoc        │         │
│    │   Testing       │   │   Testing       │   │   Testing       │         │
│    │                 │   │                 │   │                 │         │
│    │ • Daily scans   │   │ • New threat    │   │ • Incident      │         │
│    │ • Weekly deep   │   │ • Config change │   │ • Audit prep    │         │
│    │ • Monthly full  │   │ • Deployment    │   │ • Exercise      │         │
│    └─────────────────┘   └─────────────────┘   └─────────────────┘         │
│              │                     │                     │                  │
│              └─────────────────────┼─────────────────────┘                  │
│                                    │                                         │
│                                    ▼                                         │
│                    ┌───────────────────────────────┐                        │
│                    │    Security Posture Score     │                        │
│                    │    (Real-time Dashboard)      │                        │
│                    └───────────────────────────────┘                        │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Testing Cadence

| Test Type | Frequency | Scope | Purpose |
|-----------|-----------|-------|---------|
| **Baseline** | Daily | Critical controls | Ensure no regression |
| **Standard** | Weekly | Full control set | Comprehensive coverage |
| **Deep Dive** | Monthly | Specific domains | Thorough analysis |
| **Threat-Based** | On intelligence | Specific TTPs | Emerging threat response |
| **Full Simulation** | Quarterly | End-to-end | Realistic assessment |

### Security Posture Metrics

#### Security Score Components

| Component | Weight | Data Source |
|-----------|--------|-------------|
| **Control Effectiveness** | 40% | BAS test results |
| **Detection Coverage** | 25% | ATT&CK coverage |
| **Response Capability** | 20% | Exercise results |
| **Vulnerability Posture** | 15% | VM platform |

#### Trend Analysis

| Metric | Tracking | Goal |
|--------|----------|------|
| **Score Improvement** | Monthly trend | Continuous increase |
| **Gap Closure** | Techniques covered | 90%+ coverage |
| **MTTD Trend** | Detection time | Decreasing |
| **False Positive Trend** | Alert quality | Decreasing |

---

## Exercise Planning and Execution

### Exercise Types

| Type | Duration | Scope | Frequency |
|------|----------|-------|-----------|
| **Tabletop** | 2-4 hours | Scenario discussion | Quarterly |
| **Functional** | 1-2 days | Limited execution | Bi-annually |
| **Full-Scale** | 3-5 days | Comprehensive | Annually |
| **Purple Team** | 1-3 days | Collaborative | Monthly |

### Exercise Planning Template

#### Pre-Exercise Planning

| Week | Activity |
|------|----------|
| **-8** | Define objectives, scope, participants |
| **-6** | Develop scenarios, injects |
| **-4** | Prepare infrastructure, tools |
| **-2** | Briefings, logistics |
| **-1** | Final checks, communications test |

#### Exercise Execution

| Day | Activities |
|-----|------------|
| **Day 1** | Initial access, establish foothold |
| **Day 2** | Lateral movement, persistence |
| **Day 3** | Objective execution, exfiltration |
| **Day 4** | Detection response, containment |
| **Day 5** | Hot wash, initial findings |

#### Post-Exercise

| Week | Activity |
|------|----------|
| **+1** | Detailed analysis, evidence collection |
| **+2** | Draft report, findings compilation |
| **+3** | Report review, recommendations |
| **+4** | Final report, improvement plan |
| **+8** | Re-test improvements |

---

## Singapore Government Exercise Integration

### Exercise Cyber Star

Annual national cyber readiness exercise:

| Aspect | Details |
|--------|---------|
| **Organizer** | CSA |
| **Participants** | Government agencies, CII owners, DIS |
| **Duration** | 11 days (2024 edition) |
| **Scope** | National cyber incident response |

**Integration Opportunities**:
- Align red team scenarios with exercise themes
- Contribute findings to national assessment
- Validate detection capabilities pre-exercise
- Participate in cross-sector coordination

### Critical Infrastructure Defence Exercise (CIDeX)

| Aspect | Details |
|--------|---------|
| **Organizers** | DIS and CSA |
| **Participants** | 11 CII sectors, 200+ participants |
| **Focus** | IT and OT network defense |
| **Innovation** | AI-driven attack simulations (2025) |

**CIDeX 2025 Features**:
- AI-enhanced attack scenarios
- Cross-sector coordination
- OT testbed environment
- Cloud infrastructure testing

**Integration Opportunities**:
- Use CIDeX scenarios for internal testing
- Leverage OT testbed capabilities
- Validate findings against CIDeX results
- Cross-sector threat sharing

### Counter Ransomware Initiative (CRI)

Singapore hosting CRI Summit October 2025:

| Focus Area | Relevance |
|------------|-----------|
| Ransomware defense | Priority simulation scenarios |
| Payment disruption | Financial sector testing |
| Threat intelligence | Intelligence-driven simulation |
| International cooperation | Shared TTPs and indicators |

### OT-ISAC Coordination

| Opportunity | Value |
|-------------|-------|
| Threat intelligence | OT-specific threats |
| Testing coordination | Avoid duplicate efforts |
| Shared scenarios | Cross-organization testing |
| Lessons learned | Collective improvement |

---

## Recommendations for Government Implementation

### Initial Implementation (Year 1)

| Quarter | Focus |
|---------|-------|
| **Q1** | BAS platform selection and deployment |
| **Q2** | Initial ATT&CK coverage assessment |
| **Q3** | First purple team exercise |
| **Q4** | Establish continuous validation baseline |

### Ongoing Operations (Year 2+)

| Activity | Cadence |
|----------|---------|
| Automated BAS testing | Daily/Weekly |
| Purple team exercises | Monthly |
| Threat intelligence integration | Continuous |
| Full simulation exercises | Quarterly |
| National exercise participation | Annually |

### Success Metrics

| Metric | Year 1 Target | Year 2 Target |
|--------|---------------|---------------|
| ATT&CK coverage | 50% | 75% |
| Detection rate | 70% | 85% |
| MTTD | <30 minutes | <15 minutes |
| Exercise participation | Cyber Star | Cyber Star + CIDeX |

---

## Sources

- [MITRE ATT&CK](https://attack.mitre.org/)
- [MITRE ATT&CK v18 Updates](https://attack.mitre.org/resources/updates/)
- [Atomic Red Team](https://github.com/redcanaryco/atomic-red-team)
- [MITRE Caldera](https://github.com/mitre/caldera)
- [Defense Frameworks Research](/docs/01-research/01-fundamentals/03-defense-frameworks.md)
- [Singapore Threats Research](/docs/01-research/05-singapore-ecosystem/05-threats-focus-areas.md)
- [CSA Exercise Cyber Star](https://www.csa.gov.sg/)
- [CIDeX 2024](https://www.mindef.gov.sg/news-and-events/latest-releases/15nov24_nr/)

---

*Return to [Offensive Solutions Overview](./README.md)*
