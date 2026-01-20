# Core Cybersecurity Concepts

> Fundamental principles and foundational knowledge for cybersecurity professionals
>
> Last Updated: January 2026

## Table of Contents

1. [CIA Triad](#1-cia-triad)
2. [Defense in Depth](#2-defense-in-depth)
3. [Zero Trust Architecture](#3-zero-trust-architecture)
4. [Attack Surface Management](#4-attack-surface-management)
5. [Risk Management Frameworks](#5-risk-management-frameworks)
6. [Security Controls](#6-security-controls)

---

## 1. CIA Triad

The CIA Triad (Confidentiality, Integrity, Availability) is the foundational model for information security, embedded in virtually every modern security framework including ISO 27001 and GDPR.

### 1.1 Confidentiality

**Definition**: Ensuring that sensitive data is accessed only by authorized parties.

**Key Measures**:
- **Encryption**: Protecting data at rest and in transit
- **Access Controls**: Role-based and attribute-based access management
- **Data Classification**: Categorizing data by sensitivity level
- **Multi-Factor Authentication (MFA)**: Additional verification layers
- **Data Masking**: Obscuring sensitive information in non-production environments

**Industry Applications**:
| Sector | Confidentiality Focus |
|--------|----------------------|
| Healthcare | Protecting electronic health records (EHRs) |
| Financial Services | Safeguarding investment data and customer PII |
| Government | Maintaining operational secrecy and classified information |
| E-commerce | Encrypting payment information |

### 1.2 Integrity

**Definition**: Protecting data from unauthorized modification to ensure accuracy and trustworthiness.

**Key Measures**:
- **Hashing**: Creating cryptographic fingerprints to detect changes
- **Checksums**: Verifying data hasn't been altered during transmission
- **Version Control**: Tracking changes and maintaining audit trails
- **Digital Signatures**: Authenticating the source and integrity of data
- **Input Validation**: Preventing malicious data injection

**Integrity Threats**:
- Man-in-the-middle attacks
- SQL injection
- Unauthorized database modifications
- Malware that alters files
- Insider manipulation

### 1.3 Availability

**Definition**: Making sure data and systems are accessible when needed by authorized users.

**Key Measures**:
- **Redundancy**: Eliminating single points of failure
- **Disaster Recovery**: Planning for system restoration
- **Load Balancing**: Distributing traffic across resources
- **Uptime Monitoring**: Continuous system health checks
- **DDoS Protection**: Mitigating denial-of-service attacks
- **Backup Systems**: Regular, tested backup procedures

**Availability Metrics**:
| Availability % | Downtime per Year |
|---------------|-------------------|
| 99% | 3.65 days |
| 99.9% | 8.76 hours |
| 99.99% | 52.56 minutes |
| 99.999% | 5.26 minutes |

### 1.4 Balancing the Triad

Security controls rarely support only one pillar. Often, strengthening one may impact another:

| Trade-off | Example |
|-----------|---------|
| Confidentiality vs. Availability | Strong encryption and MFA can slow access |
| Integrity vs. Availability | Extensive validation checks may impact performance |
| Confidentiality vs. Usability | Complex access controls may frustrate users |

**Current Statistics (2025)**:
- Global cybercrime impact: $10.5 trillion projected
- Average data breach cost: $4.44 million (IBM 2025 report)
- Insider threats affecting: 83%+ of organizations (year-over-year increase)

### 1.5 Beyond the CIA Triad

Modern security frameworks extend the CIA Triad with additional principles:
- **Non-repudiation**: Ensuring actions cannot be denied
- **Authentication**: Verifying identity
- **Authorization**: Confirming permissions
- **Accountability**: Maintaining audit trails

---

## 2. Defense in Depth

Defense in Depth (DiD) is a cybersecurity strategy using multiple security layers to protect critical assets. Originating from military strategy, it ensures that if one defense layer fails, additional layers provide backup protection.

### 2.1 The Three Pillars

#### Physical Security
- **Data Center Controls**: Biometric access, surveillance, environmental controls
- **Device Security**: Locked cabinets, cable locks, secure disposal
- **Perimeter Security**: Fencing, guards, access badges

#### Technical Security
- **Network Security**: Firewalls, IDS/IPS, network segmentation
- **Endpoint Security**: Antivirus, EDR, host-based firewalls
- **Application Security**: Secure coding, WAF, input validation
- **Data Security**: Encryption, DLP, database activity monitoring

#### Administrative Security
- **Policies and Procedures**: Acceptable use, security policies
- **Training and Awareness**: Security education, phishing simulations
- **Governance**: Risk management, compliance oversight
- **Access Management**: Least privilege, separation of duties

### 2.2 Modern DiD Components (2025-2026)

| Layer | Technologies | Purpose |
|-------|--------------|---------|
| Perimeter | Next-gen firewalls, CASB | First line of defense |
| Network | Microsegmentation, NDR | Lateral movement prevention |
| Endpoint | EDR, XDR, MDM | Device-level protection |
| Application | RASP, WAF, SAST/DAST | Application hardening |
| Data | Encryption, DLP, Rights Management | Data-centric protection |
| Identity | IAM, PAM, MFA | Access control |
| Monitoring | SIEM, SOAR, UEBA | Detection and response |

### 2.3 Key Modern Strategies

**Privileged Access Management (PAM)**:
- Monitor and secure privileged accounts
- Implement just-in-time access
- Session recording and auditing

**Endpoint Privilege Management**:
- Lock down privilege across endpoints
- Prevent lateral movement
- Defend against ransomware

**Machine Learning for Anomaly Detection**:
- Behavioral analytics for users and endpoints
- Automated threat detection
- Predictive security analytics

### 2.4 Why Defense in Depth Matters Now

> "Instead of smashing through the front door, more attackers will simply walk in using valid credentials, abusing identity systems, single sign-on and trusted AI agents to blend into normal activity."
>
> — Morgan Adamski, former Executive Director at U.S. Cyber Command (2026 Predictions)

**Current Threat Context**:
- 56% of ransomware attacks in 2024 used legitimate tools like PowerShell
- Attackers exploit multiple entry points simultaneously
- A single security layer is no longer sufficient

---

## 3. Zero Trust Architecture

Zero Trust is a security framework requiring all users, inside or outside the network, to be authenticated, authorized, and continuously validated before accessing applications and data.

### 3.1 Core Principles

| Principle | Description |
|-----------|-------------|
| **Never Trust, Always Verify** | No implicit trust based on location or network |
| **Assume Breach** | Design as if adversaries are already present |
| **Verify Explicitly** | Always authenticate and authorize based on all data points |
| **Least Privilege Access** | Grant minimum necessary permissions |
| **Microsegmentation** | Divide networks into secure zones |

### 3.2 The Seven Pillars of Zero Trust

Based on NIST SP 800-207 and DoD Zero Trust guidelines:

1. **Identity**: Continuous authentication and identity verification
2. **Devices**: Device health and compliance verification
3. **Network**: Microsegmentation and encrypted communications
4. **Applications**: Secure application access and monitoring
5. **Data**: Data classification, protection, and access control
6. **Infrastructure**: Secure configuration and monitoring
7. **Visibility & Analytics**: Continuous monitoring and threat intelligence

### 3.3 NIST Zero Trust Guidance (2025)

**NIST SP 1800-35** (June 2025) provides comprehensive implementation guidance:

**Key Features**:
- Developed through 4-year project with 24 industry partners
- 19 real-world implementation models
- Technical configurations and best practices
- Three primary deployment approaches:
  1. **Enhanced Identity Governance**: Identity and attribute-based access
  2. **Microsegmentation**: Smart devices isolating specific resources
  3. **Software-Defined Perimeter**: Dynamic perimeter establishment

**Implementation Reality**:
> "Switching from traditional protection to zero trust requires a lot of changes. You have to understand who's accessing what resources and why. Also, everyone's network environments are different, so every ZTA is a custom build."
>
> — Alper Kerman, NIST Computer Scientist

### 3.4 DoD Zero Trust Implementation (January 2026)

The Department of Defense Zero Trust Implementation Guidelines (ZIGs) emphasize:

- Continuous authentication of every User/Person Entity (PE)
- Device/Non-Person Entity (NPE) verification
- Application-level access controls
- Operating under "never trust, always verify" and "assume breach" principles

### 3.5 Zero Trust Maturity Model

| Stage | Characteristics |
|-------|-----------------|
| **Traditional** | Perimeter-based, implicit trust inside network |
| **Initial** | Beginning identity-centric approach, some MFA |
| **Advanced** | Microsegmentation, continuous verification |
| **Optimal** | Fully automated, AI-driven, real-time adaptation |

### 3.6 Implementation Challenges

- **Legacy Systems**: Older systems may not support modern authentication
- **Complexity**: Requires understanding of all data flows
- **User Experience**: Balance security with productivity
- **Cost**: Significant investment in technology and training
- **Cultural Change**: Shift from "trust but verify" mindset

---

## 4. Attack Surface Management

Attack Surface Management (ASM) is the continuous process of identifying, monitoring, and reducing every possible point of unauthorized access to a system.

### 4.1 The Expanding Attack Surface

**Growth Statistics**:
- Attack surface has grown by more than **67% since 2022** (TechTarget)
- **82% of enterprises** now use hybrid environments (CSA)
- **Two-thirds** work with two or more cloud providers

**Contributing Factors**:
- Rise of IoT devices
- Increasing API usage and microservices
- Remote/hybrid work expansion
- Shadow IT proliferation
- Decentralized infrastructure management

### 4.2 Types of Attack Surfaces

#### External Attack Surface
- Public-facing web applications
- APIs and services
- Cloud infrastructure
- Email systems
- DNS and domain infrastructure

#### Internal Attack Surface
- Internal applications
- Databases
- File shares
- Endpoints
- Network infrastructure

#### Human Attack Surface
- Employees (phishing targets)
- Contractors and vendors
- Social engineering vulnerabilities

### 4.3 External Attack Surface Management (EASM)

EASM focuses on finding and managing every asset an organization exposes to the internet:

**Key Capabilities**:
- Asset discovery and inventory
- Vulnerability identification
- Risk prioritization
- Continuous monitoring
- Third-party risk assessment

### 4.4 2026 Predictions

**AI Integration**:
> "By 2026, AI for attack surface management will be a given. This goes beyond using AI to automate scans. It will include intelligent and agentic AI that spots threats and remediates them autonomously and far faster than humans could."

**Zero Trust Convergence**:
- Zero trust will evolve from concept to configuration
- Integrated directly into platform architecture

**Security Function Convergence**:
- Cloud, identity, and exposure management will converge
- New cross-disciplinary skill requirements

### 4.5 Emerging Challenges

| Challenge | Description |
|-----------|-------------|
| **API Sprawl** | AI APIs becoming major attack vectors |
| **Shadow AI** | 20% of 2025 breaches involved unauthorized AI tools (IBM) |
| **Supply Chain** | Wider mapping covering nth-party risk |
| **Dynamic Entry Points** | Thousands of fragmenting entry points |

**Financial Impact**:
- Average ransomware recovery cost: **$2.73 million** (nearly $1 million more than 2023)

---

## 5. Risk Management Frameworks

Risk management frameworks provide structured approaches to identifying, assessing, and mitigating cybersecurity risks.

### 5.1 NIST Risk Management Framework (RMF)

The NIST RMF (SP 800-37) provides a comprehensive 7-step process for managing information security and privacy risk.

#### The Seven RMF Steps

| Step | Purpose | Key Activities |
|------|---------|----------------|
| **Prepare** | Essential activities to prepare for risk management | Establish context, priorities, resources |
| **Categorize** | Determine impact levels for systems | Based on confidentiality, integrity, availability |
| **Select** | Choose appropriate security controls | Based on risk assessment and system categorization |
| **Implement** | Deploy security controls | Document implementation details |
| **Assess** | Evaluate control effectiveness | Determine if controls meet requirements |
| **Authorize** | Senior management risk acceptance | Authorize system operation |
| **Monitor** | Ongoing assessment and response | Continuous monitoring and maintenance |

#### 2025 Updates

**SP 800-53 Release 5.2.0** (August 2025):
- New controls: SA-15(13), SA-24, SI-02(07)
- Revisions to SI-07(12)
- Updated control discussions
- Response to Executive Order 14306

**Cyber AI Profile** (December 2025):
- NIST IR 8596 guidance for AI-related risks
- Aligned with CSF 2.0
- Addresses AI adoption cybersecurity challenges

### 5.2 ISO 31000 Risk Management

International standard providing principles and guidelines:

**Key Principles**:
- Integrated into organizational processes
- Structured and comprehensive
- Customized to the organization
- Inclusive and transparent
- Dynamic and responsive to change
- Continually improved

### 5.3 Risk Assessment Process

1. **Risk Identification**: Determine what could go wrong
2. **Risk Analysis**: Understand likelihood and impact
3. **Risk Evaluation**: Prioritize risks for treatment
4. **Risk Treatment**: Select and implement controls
5. **Risk Monitoring**: Ongoing assessment and adjustment

### 5.4 Risk Calculation

**Qualitative Formula**:
```
Risk = Likelihood x Impact
```

**Risk Matrix**:
| | Low Impact | Medium Impact | High Impact |
|---|------------|---------------|-------------|
| **High Likelihood** | Medium | High | Critical |
| **Medium Likelihood** | Low | Medium | High |
| **Low Likelihood** | Low | Low | Medium |

### 5.5 Risk Treatment Options

| Option | Description | Example |
|--------|-------------|---------|
| **Avoid** | Eliminate the risk entirely | Don't deploy vulnerable technology |
| **Mitigate** | Reduce likelihood or impact | Implement security controls |
| **Transfer** | Share risk with third party | Cyber insurance, outsourcing |
| **Accept** | Acknowledge and monitor | Document low-priority risks |

---

## 6. Security Controls

Security controls are safeguards designed to protect information systems and data. They are categorized by function: Preventive, Detective, and Corrective.

### 6.1 Preventive Controls

**Purpose**: Stop security incidents before they occur.

**Examples**:
| Control | Description |
|---------|-------------|
| Access Control | Restrict who can access resources |
| Authentication | Verify user identity |
| Encryption | Protect data confidentiality |
| Firewalls | Block unauthorized network traffic |
| Security Awareness Training | Educate users about threats |
| Secure Configuration | Harden systems against attack |
| Input Validation | Prevent injection attacks |

**Effectiveness Metrics**:
- Number of blocked intrusion attempts
- Percentage of employees passing phishing tests
- Vulnerability remediation time

### 6.2 Detective Controls

**Purpose**: Identify and alert on security incidents as they occur.

**Examples**:
| Control | Description |
|---------|-------------|
| Intrusion Detection Systems (IDS) | Monitor for malicious activity |
| SIEM | Aggregate and analyze security logs |
| Audit Logs | Record system and user activities |
| Network Monitoring | Observe traffic patterns |
| File Integrity Monitoring | Detect unauthorized changes |
| Security Cameras | Physical surveillance |

**Effectiveness Metrics**:
- **Mean Time to Detect (MTTD)**: Average time to discover incidents
- False positive rate
- Detection coverage percentage

### 6.3 Corrective Controls

**Purpose**: Restore systems and mitigate damage after an incident.

**Examples**:
| Control | Description |
|---------|-------------|
| Incident Response Plans | Documented response procedures |
| Backup and Restore | Data recovery capabilities |
| Patch Management | Fix vulnerabilities |
| System Recovery | Restore operations |
| Forensic Analysis | Investigate incidents |
| Lessons Learned | Improve future response |

**Effectiveness Metrics**:
- **Mean Time to Respond (MTTR)**: Average time to contain and recover
- Recovery Point Objective (RPO) achievement
- Recovery Time Objective (RTO) achievement

### 6.4 Additional Control Categories

#### Compensating Controls
Alternative controls when primary controls are not feasible:
- Network segmentation when patching isn't possible
- Additional monitoring for legacy systems

#### Deterrent Controls
Discourage potential attackers:
- Warning banners
- Security signage
- Published security policies

#### Physical Controls
Protect physical assets:
- Locks and access badges
- Security guards
- Environmental controls

### 6.5 Framework Alignment

| Framework | Preventive | Detective | Corrective |
|-----------|------------|-----------|------------|
| NIST CSF 2.0 | Protect | Detect | Respond, Recover |
| ISO 27001 | Various Annex A | Various Annex A | Various Annex A |
| CIS Controls | Multiple | Multiple | Multiple |

### 6.6 Implementing Complete Controls

**Best Practice**: Implement a combination of all three control types at each layer of defense:

```
                    ┌─────────────────────────────────┐
                    │      PREVENTIVE CONTROLS        │
                    │  (Stop incidents from occurring)│
                    └─────────────────────────────────┘
                                   │
                                   ▼
                    ┌─────────────────────────────────┐
                    │       DETECTIVE CONTROLS        │
                    │    (Identify when they occur)   │
                    └─────────────────────────────────┘
                                   │
                                   ▼
                    ┌─────────────────────────────────┐
                    │       CORRECTIVE CONTROLS       │
                    │     (Respond and recover)       │
                    └─────────────────────────────────┘
```

**Key Principle**: No preventive control is perfect. Always implement detective and corrective controls as backup.

---

## Summary

### Key Takeaways

1. **CIA Triad** remains the foundation of information security, with modern extensions for non-repudiation and accountability

2. **Defense in Depth** requires multiple security layers across physical, technical, and administrative domains

3. **Zero Trust** is becoming the standard security architecture, requiring continuous verification and assuming breach

4. **Attack Surface Management** is critical as organizations face exponentially growing digital footprints

5. **Risk Management** must be systematic, using frameworks like NIST RMF to ensure comprehensive coverage

6. **Security Controls** should combine preventive, detective, and corrective measures at every layer

### Recommended Next Steps

1. Assess your organization's current alignment with CIA Triad principles
2. Map your defense-in-depth layers and identify gaps
3. Begin Zero Trust journey with identity and access management
4. Implement continuous attack surface discovery and monitoring
5. Adopt a formal risk management framework
6. Audit security controls across all three categories

---

## Sources

- [Fortinet - CIA Triad](https://www.fortinet.com/resources/cyberglossary/cia-triad)
- [IT Governance UK - CIA Triad 2025](https://www.itgovernance.co.uk/blog/what-is-the-cia-triad-and-why-is-it-important)
- [NIST SP 800-207 - Zero Trust Architecture](https://csrc.nist.gov/pubs/sp/800/207/final)
- [NIST SP 1800-35 - Implementing Zero Trust Architecture](https://pages.nist.gov/zero-trust-architecture/)
- [DoD Zero Trust Implementation Guidelines (January 2026)](https://media.defense.gov/2026/Jan/08/2003852320/-1/-1/0/CTR_ZERO_TRUST_IMPLEMENTATION_GUIDELINE_PRIMER.PDF)
- [NIST Risk Management Framework](https://csrc.nist.gov/projects/risk-management)
- [ISACA - Defense in Depth 2025](https://www.isaca.org/resources/news-and-trends/isaca-now-blog/2025/beyond-the-moat-modern-defense-in-depth-strategies)
- [SentinelOne - Defense in Depth AI Cybersecurity 2025](https://www.sentinelone.com/cybersecurity-101/cybersecurity/defense-in-depth-ai-cybersecurity/)
- [SecurityWeek - Attack Surface Management 2026](https://www.securityweek.com/cyber-insights-2026-external-attack-surface-management/)
- [6clicks - Security Controls](https://www.6clicks.com/resources/answers/what-are-the-three-types-of-security-controls-nist)
