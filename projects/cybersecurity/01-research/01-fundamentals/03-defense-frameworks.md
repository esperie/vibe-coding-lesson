# Defense Frameworks

> Major cybersecurity frameworks, standards, and methodologies for organizational defense
>
> Last Updated: January 2026

## Table of Contents

1. [NIST Cybersecurity Framework (CSF) 2.0](#1-nist-cybersecurity-framework-csf-20)
2. [MITRE ATT&CK](#2-mitre-attck)
3. [OWASP Top 10](#3-owasp-top-10)
4. [ISO 27001/27002](#4-iso-2700127002)
5. [CIS Controls](#5-cis-controls)
6. [STRIDE/DREAD Threat Modeling](#6-stridedread-threat-modeling)

---

## 1. NIST Cybersecurity Framework (CSF) 2.0

The NIST Cybersecurity Framework is a voluntary framework consisting of standards, guidelines, and best practices to manage cybersecurity risk.

### 1.1 Overview

**Current Version**: CSF 2.0 (Released 2024)

**Key Changes from CSF 1.1**:
- Added new **GOVERN** function (6 functions total)
- Expanded scope to **all organizations** (not just critical infrastructure)
- Enhanced supply chain risk management guidance
- Improved alignment with other frameworks

### 1.2 The Six Core Functions

```
┌─────────────────────────────────────────────────────────────────────┐
│                           GOVERN (New in 2.0)                       │
│         Organizational context, strategy, and oversight             │
└─────────────────────────────────────────────────────────────────────┘
                                   │
        ┌──────────────────────────┼──────────────────────────┐
        │                          │                          │
        ▼                          ▼                          ▼
┌───────────────┐          ┌───────────────┐          ┌───────────────┐
│   IDENTIFY    │          │    PROTECT    │          │    DETECT     │
│  Asset & Risk │          │  Safeguards   │          │   Anomalies   │
│  Management   │          │               │          │   & Events    │
└───────────────┘          └───────────────┘          └───────────────┘
                                   │
                    ┌──────────────┴──────────────┐
                    │                             │
                    ▼                             ▼
            ┌───────────────┐             ┌───────────────┐
            │    RESPOND    │             │    RECOVER    │
            │   Incident    │             │  Restoration  │
            │   Response    │             │   & Learning  │
            └───────────────┘             └───────────────┘
```

#### GOVERN (GV)
**Purpose**: Establish and monitor cybersecurity risk management strategy, expectations, and policy.

**Categories**:
- Organizational Context (GV.OC)
- Risk Management Strategy (GV.RM)
- Roles, Responsibilities, and Authorities (GV.RR)
- Policy (GV.PO)
- Oversight (GV.OV)
- Cybersecurity Supply Chain Risk Management (GV.SC)

#### IDENTIFY (ID)
**Purpose**: Understand organizational context and cybersecurity risk to systems, assets, data, and capabilities.

**Categories**:
- Asset Management (ID.AM)
- Risk Assessment (ID.RA)
- Improvement (ID.IM)

#### PROTECT (PR)
**Purpose**: Implement appropriate safeguards to ensure delivery of critical services.

**Categories**:
- Identity Management, Authentication, and Access Control (PR.AA)
- Awareness and Training (PR.AT)
- Data Security (PR.DS)
- Platform Security (PR.PS)
- Technology Infrastructure Resilience (PR.IR)

#### DETECT (DE)
**Purpose**: Develop and implement activities to identify cybersecurity events.

**Categories**:
- Continuous Monitoring (DE.CM)
- Adverse Event Analysis (DE.AE)

#### RESPOND (RS)
**Purpose**: Take action regarding detected cybersecurity incidents.

**Categories**:
- Incident Management (RS.MA)
- Incident Analysis (RS.AN)
- Incident Response Reporting and Communication (RS.CO)
- Incident Mitigation (RS.MI)

#### RECOVER (RC)
**Purpose**: Maintain plans for resilience and restore capabilities impaired by cybersecurity incidents.

**Categories**:
- Incident Recovery Plan Execution (RC.RP)
- Incident Recovery Communication (RC.CO)

### 1.3 Implementation Tiers

| Tier | Name | Description |
|------|------|-------------|
| **Tier 1** | Partial | Ad hoc, reactive, limited awareness |
| **Tier 2** | Risk Informed | Management approved but not organization-wide |
| **Tier 3** | Repeatable | Formally approved, regularly updated |
| **Tier 4** | Adaptive | Continuously improving based on lessons learned |

### 1.4 2025-2026 Updates and Resources

**Recent Publications**:
- **SP 800-61r3** (April 2025): Incident Response Recommendations aligned with CSF 2.0
- **NIST IR 8286 series** (December 2025): Updated for CSF 2.0 alignment
- **CSWP 39** (December 2025): Crypto Agility strategies

**CSF 2.0 Profiles**:
- **Cyber AI Profile** (NIST IR 8596, December 2025): Guidance for AI risk management
- **Community Profiles**: Sector-specific implementations

**Available in Multiple Languages**: Including Mandarin and Thai (2025)

### 1.5 CSF 2.0 Quick-Start Guide

NIST SP 1308 provides integration guidance for:
- Cybersecurity Risk Management
- Enterprise Risk Management (ERM)
- Workforce Management (NICE Framework)

---

## 2. MITRE ATT&CK

MITRE ATT&CK (Adversarial Tactics, Techniques, and Common Knowledge) is a globally-accessible knowledge base of adversary tactics and techniques based on real-world observations.

### 2.1 Overview

**Current Version**: ATT&CK v18 (Released October 28, 2025)

**Framework Statistics (v18)**:
| Domain | Tactics | Techniques | Sub-Techniques | Groups | Software |
|--------|---------|------------|----------------|--------|----------|
| Enterprise | 14 | 216 | 475 | 172 | 784 |
| Mobile | 12 | 77 | 47 | 17 | 122 |
| ICS | 12 | 83 | - | 14 | 23 |

**Total**: 910 pieces of software, 176 groups, 55 campaigns

### 2.2 Major Changes in v18

**Detection Evolution**:
The biggest change in v18 is the retirement of traditional Detections and Data Sources, replaced by:
- **Detection Strategies**: Behavior-driven detection approaches
- **Analytics**: Specific detection implementations

| Domain | Detection Strategies | Analytics |
|--------|---------------------|-----------|
| Enterprise | 691 | 1,739 |
| Mobile | 124 | 211 |
| ICS | 83 | 82 |

### 2.3 Enterprise ATT&CK Tactics

| ID | Tactic | Description |
|----|--------|-------------|
| TA0043 | Reconnaissance | Gathering information for targeting |
| TA0042 | Resource Development | Establishing resources for operations |
| TA0001 | Initial Access | Gaining initial foothold |
| TA0002 | Execution | Running malicious code |
| TA0003 | Persistence | Maintaining access |
| TA0004 | Privilege Escalation | Gaining higher-level permissions |
| TA0005 | Defense Evasion | Avoiding detection |
| TA0006 | Credential Access | Stealing credentials |
| TA0007 | Discovery | Learning about the environment |
| TA0008 | Lateral Movement | Moving through the network |
| TA0009 | Collection | Gathering data of interest |
| TA0011 | Command and Control | Communicating with compromised systems |
| TA0010 | Exfiltration | Stealing data |
| TA0040 | Impact | Manipulating, interrupting, or destroying systems |

### 2.4 New Techniques in v18 (Examples)

| ID | Name | Description |
|----|------|-------------|
| T1059.013 | Container CLI/API | Adversaries using Docker CLI and Kubernetes APIs |
| T1680 | Local Storage Discovery | Mapping drives and volumes across systems |
| T1213.006 | Data from Databases | Targeting MySQL, PostgreSQL, RDS, Azure SQL |
| T1677 | Poisoned Pipeline Execution | CI/CD pipeline poisoning |

### 2.5 New ICS Assets (v18)

| ID | Asset Type | Description |
|----|------------|-------------|
| A0017 | DCS Controller | Distributed Control System Controller |
| A0016 | Firewall | ICS environment firewall |
| A0015 | Switch | Network devices connecting endpoints |

### 2.6 Using ATT&CK

**Primary Use Cases**:
1. **Threat Intelligence**: Map adversary behaviors
2. **Detection Engineering**: Develop detection strategies
3. **Red Team Operations**: Emulate adversary techniques
4. **Security Assessment**: Evaluate defensive coverage
5. **Vendor Evaluation**: Compare security product capabilities

**Tools**:
- **ATT&CK Navigator**: Visualize technique coverage
- **MITRE Caldera**: Adversary emulation platform
- **ATT&CK Evaluations**: Vendor capability assessments

### 2.7 2025 ATT&CK Evaluations

The evaluation framework now emphasizes:
- **Protection Capability**: Ability to block adversaries in real-time
- **High-Fidelity Alerts**: Actionable context for SOC teams
- **Alert Fatigue Reduction**: Prioritizing quality over quantity

---

## 3. OWASP Top 10

The OWASP Top 10 is a standard awareness document representing broad consensus about the most critical security risks to web applications.

### 3.1 OWASP Top 10:2025

**Released**: 2025 (Eighth edition)

**Methodology**:
- Analyzed 175,000+ CVE records
- Feedback from global security practitioners
- 589 CWEs evaluated (up from ~400 in 2021)

### 3.2 The Complete List

| Rank | ID | Category | Change from 2021 |
|------|----|----------|------------------|
| 1 | A01:2025 | Broken Access Control | Maintained #1 |
| 2 | A02:2025 | Security Misconfiguration | Up from #5 |
| 3 | A03:2025 | Software Supply Chain Failures | **NEW** |
| 4 | A04:2025 | Cryptographic Failures | Down from #2 |
| 5 | A05:2025 | Injection | Down from #3 |
| 6 | A06:2025 | Insecure Design | Down from #4 |
| 7 | A07:2025 | Authentication Failures | Renamed |
| 8 | A08:2025 | Software or Data Integrity Failures | Maintained |
| 9 | A09:2025 | Logging & Alerting Failures | Renamed |
| 10 | A10:2025 | Mishandling of Exceptional Conditions | **NEW** |

### 3.3 Category Details

#### A01:2025 - Broken Access Control
**Prevalence**: 3.73% of tested applications
**Description**: Failures in enforcing access restrictions
**CWEs**: 40 related CWEs

**Common Vulnerabilities**:
- Bypassing access control checks
- Insecure direct object references (IDOR)
- Missing function-level access control
- CORS misconfiguration

**Note**: Server-Side Request Forgery (SSRF) consolidated into this category

#### A02:2025 - Security Misconfiguration
**Prevalence**: 3% of tested applications
**Description**: Improper security configuration of systems

**Common Issues**:
- Default credentials
- Unnecessary features enabled
- Verbose error messages
- Missing security headers
- Outdated software

#### A03:2025 - Software Supply Chain Failures (NEW)
**Description**: Vulnerabilities introduced through third-party components

**Key Concerns**:
- Malicious packages in ecosystems
- Compromised maintainers
- Tampered build processes
- Unknown vulnerabilities in dependencies

**Evolution**: Expanded from "Vulnerable and Outdated Components"

#### A04:2025 - Cryptographic Failures
**Description**: Failures related to cryptography leading to sensitive data exposure

**Common Issues**:
- Weak algorithms
- Poor key management
- Missing encryption
- Insecure transmission

#### A05:2025 - Injection
**Description**: Untrusted data sent to interpreters

**Types**:
- SQL Injection
- NoSQL Injection
- OS Command Injection
- LDAP Injection
- XSS (Cross-Site Scripting)

#### A06:2025 - Insecure Design
**Description**: Design flaws that cannot be fixed by implementation

**Focus Areas**:
- Threat modeling
- Secure design patterns
- Reference architectures
- Security requirements

#### A07:2025 - Authentication Failures
**Description**: Failures in identity and session management

**Common Issues**:
- Weak credentials
- Session fixation
- Missing MFA
- Improper session management

#### A08:2025 - Software or Data Integrity Failures
**Description**: Failures to protect against integrity violations

**Examples**:
- Insecure deserialization
- CI/CD pipeline compromise
- Auto-update without verification

#### A09:2025 - Logging & Alerting Failures
**Description**: Insufficient logging and monitoring

**Consequences**:
- Unable to detect attacks
- No audit trail
- Delayed incident response

#### A10:2025 - Mishandling of Exceptional Conditions (NEW)
**Description**: Improper handling of errors and abnormal conditions
**CWEs**: 24 related CWEs

**Examples**:
- Improper error handling
- Logical errors
- Failing open (rather than secure)
- Resource exhaustion

### 3.4 Key Shifts in 2025

**Focus on Root Causes**: OWASP explicitly aims to identify root causes rather than symptoms

**Supply Chain Priority**: Elevated importance of third-party component security

**Exception Handling**: Recognition that abnormal conditions create vulnerabilities

---

## 4. ISO 27001/27002

ISO/IEC 27001 and 27002 are international standards for information security management.

### 4.1 ISO 27001: Information Security Management Systems

**Current Version**: ISO/IEC 27001:2022

**Purpose**: Define requirements for establishing, implementing, maintaining, and continually improving an Information Security Management System (ISMS).

**Certification**: Organizations can be certified against ISO 27001

### 4.2 Structure

**Clauses 1-3**: Scope, References, Terms
**Clause 4**: Context of the Organization
**Clause 5**: Leadership
**Clause 6**: Planning
**Clause 7**: Support
**Clause 8**: Operation
**Clause 9**: Performance Evaluation
**Clause 10**: Improvement

**Annex A**: 93 Security Controls

### 4.3 ISO 27002: Security Controls

**Current Version**: ISO/IEC 27002:2022

**Purpose**: Guidance for implementing security controls from ISO 27001

**Key Point**: Cannot be certified against ISO 27002 (guidance only)

### 4.4 Control Categories (ISO 27002:2022)

| Category | Focus |
|----------|-------|
| Organizational Controls | Policies, roles, responsibilities |
| People Controls | HR security, awareness |
| Physical Controls | Physical and environmental security |
| Technological Controls | Technical security measures |

### 4.5 Benefits of ISO 27001

1. **Structured Approach**: Comprehensive framework for security management
2. **Risk Management**: Systematic identification and treatment of risks
3. **Compliance**: Helps meet regulatory requirements
4. **Customer Confidence**: Demonstrates security commitment
5. **Continuous Improvement**: Built-in improvement mechanisms

### 4.6 2025-2026 Outlook

**Growing Adoption**:
> "With the threat landscape evolving so rapidly, attack surfaces expanding, and regulatory burden growing, standards like ISO 27001 will increasingly be prioritized in 2026."

**Compliance Challenges**:
- 37% of organizations find compliance challenging
- 66% struggle with in-house management
- 85% want more alignment across jurisdictions
- 66% say regulatory change speed makes compliance difficult

**Integration**:
- Aligns with ISO 9001 (Quality)
- Maps to GDPR requirements
- Complements other frameworks (NIST, CIS)

**AI Management**:
- ISO 42001 (AI systems management) adoption grew from 1% to 28% (2024-2025)

---

## 5. CIS Controls

The CIS Critical Security Controls are a prioritized set of best practices to defend against common cyber attacks.

### 5.1 Overview

**Current Version**: CIS Controls v8.1 (2024)

**Evolution**: Reduced from 20 controls (v7) to 18 controls (v8), aligned with modern IT environments including cloud and hybrid infrastructure

**Alignment**: Updated for NIST CSF 2.0 and modern frameworks

### 5.2 The 18 CIS Controls

| # | Control | Description |
|---|---------|-------------|
| 1 | Inventory and Control of Enterprise Assets | Know what you have |
| 2 | Inventory and Control of Software Assets | Know what software runs |
| 3 | Data Protection | Protect sensitive data |
| 4 | Secure Configuration of Enterprise Assets | Harden systems |
| 5 | Account Management | Control who has access |
| 6 | Access Control Management | Manage permissions |
| 7 | Continuous Vulnerability Management | Find and fix vulnerabilities |
| 8 | Audit Log Management | Collect and analyze logs |
| 9 | Email and Web Browser Protections | Protect common vectors |
| 10 | Malware Defenses | Prevent and detect malware |
| 11 | Data Recovery | Maintain backups |
| 12 | Network Infrastructure Management | Secure network devices |
| 13 | Network Monitoring and Defense | Watch network traffic |
| 14 | Security Awareness and Skills Training | Train users |
| 15 | Service Provider Management | Manage third parties |
| 16 | Application Software Security | Secure applications |
| 17 | Incident Response Management | Plan for incidents |
| 18 | Penetration Testing | Test defenses |

### 5.3 Implementation Groups (IGs)

CIS introduced Implementation Groups to help organizations adopt controls based on their risk profile:

| Group | Description | Target |
|-------|-------------|--------|
| **IG1** | Essential Cyber Hygiene | All organizations |
| **IG2** | Foundational Security | More resources, higher risk |
| **IG3** | Advanced Security | Sophisticated defenses |

**IG1**: Represents the minimum standard every organization should implement

**IG2**: Builds on IG1 for organizations with more complexity

**IG3**: Full implementation for organizations handling sensitive data or facing sophisticated threats

### 5.4 Safeguards

Each control contains multiple **Safeguards** (formerly Sub-Controls):
- Specific, actionable security measures
- Asset type classifications
- Security function alignment

### 5.5 2026 Cybersecurity Predictions from CIS

**AI Focus**:
> "AI continues to dominate the headlines and security landscape. Organizations will require contextualization of specific AI applications and use cases, including Model Context Protocol (MCP), Agentic AI, and Large Language Models (LLMs)."

**Continuous Evolution**:
> "Security programs must anticipate and adapt to meet the complexity of the threats they are facing."

### 5.6 Mapping to Other Frameworks

| CIS Control | NIST CSF 2.0 Function |
|-------------|----------------------|
| Controls 1-2 | Identify |
| Controls 3-14 | Protect |
| Controls 8, 13 | Detect |
| Control 17 | Respond |
| Control 11 | Recover |
| Multiple | Govern |

---

## 6. STRIDE/DREAD Threat Modeling

STRIDE and DREAD are complementary threat modeling methodologies developed by Microsoft.

### 6.1 STRIDE Overview

**Developed by**: Loren Kohnfelder and Praerit Garg (1999)

**Purpose**: Systematically identify potential vulnerabilities and threats

**Approach**: Categorizes threats into six distinct types

### 6.2 The STRIDE Categories

| Category | Description | Security Property Violated |
|----------|-------------|---------------------------|
| **S**poofing | Impersonating something or someone | Authentication |
| **T**ampering | Modifying data or code | Integrity |
| **R**epudiation | Denying actions performed | Non-repudiation |
| **I**nformation Disclosure | Exposing information | Confidentiality |
| **D**enial of Service | Making systems unavailable | Availability |
| **E**levation of Privilege | Gaining unauthorized permissions | Authorization |

### 6.3 STRIDE Mapping to Security Principles

| STRIDE Category | Security Principle |
|-----------------|-------------------|
| Spoofing | Authenticity |
| Tampering | Integrity |
| Repudiation | Non-repudiability |
| Information Disclosure | Confidentiality |
| Denial of Service | Availability |
| Elevation of Privilege | Authorization |

### 6.4 STRIDE Process

1. **Create a Data Flow Diagram (DFD)**: Map system components and data flows
2. **Identify Threats**: Apply STRIDE categories to each element
3. **Document Threats**: Record potential attack scenarios
4. **Mitigate**: Develop countermeasures
5. **Validate**: Verify mitigations are effective

### 6.5 DREAD Overview

**Purpose**: Quantitative risk assessment methodology for prioritizing threats

**Note**: Largely deprecated by Microsoft due to subjectivity concerns, but still useful for prioritization

### 6.6 The DREAD Categories

| Category | Question | Scale |
|----------|----------|-------|
| **D**amage | How bad would an attack be? | 0-10 |
| **R**eproducibility | How easy is it to reproduce? | 0-10 |
| **E**xploitability | How much work to launch? | 0-10 |
| **A**ffected Users | How many people impacted? | 0-10 |
| **D**iscoverability | How easy to discover? | 0-10 |

### 6.7 DREAD Calculation

**Formula**:
```
Risk = (Damage + Reproducibility + Exploitability + Affected Users + Discoverability) / 5
```

**Risk Levels**:
| Score | Risk Level |
|-------|------------|
| 12-15 | Critical |
| 8-11 | High |
| 5-7 | Medium |
| 1-4 | Low |

### 6.8 STRIDE + DREAD Together

**Combined Workflow**:
1. Use STRIDE to **identify and categorize** threats
2. Use DREAD to **prioritize** those threats for mitigation

```
┌────────────────────────────────────────────────────────┐
│                        STRIDE                          │
│              (Threat Identification)                   │
├────────────────────────────────────────────────────────┤
│  Spoofing → Tampering → Repudiation → Info Disclosure │
│                    ↓                                   │
│           Denial of Service → Elevation of Privilege  │
└────────────────────────────────────────────────────────┘
                          │
                          ▼
┌────────────────────────────────────────────────────────┐
│                        DREAD                           │
│               (Risk Prioritization)                    │
├────────────────────────────────────────────────────────┤
│     Damage + Reproducibility + Exploitability +        │
│     Affected Users + Discoverability = Risk Score      │
└────────────────────────────────────────────────────────┘
                          │
                          ▼
┌────────────────────────────────────────────────────────┐
│              Prioritized Mitigation Plan               │
└────────────────────────────────────────────────────────┘
```

### 6.9 Modern Tools (2025)

**AI-Powered Threat Modeling**:
- **STRIDE-GPT**: AI-powered tool using OpenAI GPT models
  - Generate threat models based on STRIDE
  - DREAD risk scoring for identified threats
  - Gherkin test case generation
  - GitHub repository analysis

### 6.10 Alternative Methodologies

| Methodology | Focus | Best For |
|-------------|-------|----------|
| STRIDE | Threat categorization | Application security |
| DREAD | Risk quantification | Prioritization |
| PASTA | Process-driven, risk-centric | Enterprise applications |
| VAST | Scalable, agile-friendly | DevSecOps environments |
| OCTAVE | Asset-focused | Organizational risk |

---

## Framework Comparison and Selection

### Comparison Matrix

| Framework | Scope | Focus | Best For |
|-----------|-------|-------|----------|
| NIST CSF 2.0 | Organization-wide | Risk management | Overall program |
| MITRE ATT&CK | Adversary behavior | Detection | Threat intelligence, SOC |
| OWASP Top 10 | Web applications | Vulnerabilities | Application security |
| ISO 27001/27002 | ISMS | Compliance | Certification, governance |
| CIS Controls | Technical controls | Implementation | Practical security |
| STRIDE/DREAD | Applications | Threat modeling | Secure design |

### Recommended Combinations

**For Government Agencies**:
- NIST CSF 2.0 (overall program)
- NIST RMF (risk management)
- CIS Controls (implementation)
- MITRE ATT&CK (threat intelligence)

**For Application Development**:
- OWASP Top 10 (vulnerabilities)
- STRIDE/DREAD (threat modeling)
- MITRE ATT&CK (adversary techniques)

**For Compliance-Driven Organizations**:
- ISO 27001/27002 (certification)
- NIST CSF 2.0 (framework alignment)
- CIS Controls (technical implementation)

---

## Sources

- [NIST Cybersecurity Framework](https://www.nist.gov/cyberframework)
- [NIST CSF 2.0 Quick-Start Guide](https://csrc.nist.gov/news/2025/implementing-a-zero-trust-architecture-sp-1800-35)
- [MITRE ATT&CK](https://attack.mitre.org/)
- [MITRE ATT&CK v18 Updates](https://attack.mitre.org/resources/updates/updates-october-2025/)
- [OWASP Top 10:2025](https://owasp.org/Top10/2025/)
- [GitLab - OWASP Top 10 2025 Analysis](https://about.gitlab.com/blog/2025-owasp-top-10-whats-changed-and-why-it-matters/)
- [ISO/IEC 27001:2022](https://www.iso.org/standard/27001)
- [CIS Critical Security Controls](https://www.cisecurity.org/controls)
- [CIS 2026 Predictions](https://www.cisecurity.org/insights/blog/7-cis-experts-2026-cybersecurity-predictions)
- [STRIDE Threat Modeling](https://threat-modeling.com/dread-threat-modeling/)
- [Destcert - Threat Modeling Methodologies](https://destcert.com/resources/threat-modeling-methodologies/)
