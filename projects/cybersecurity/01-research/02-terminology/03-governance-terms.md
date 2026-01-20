# Governance and Compliance Terminology

Comprehensive reference for governance, risk, compliance (GRC), audit, policy, and regulatory terminology in cybersecurity.

## Table of Contents

1. [GRC Fundamentals](#grc-fundamentals)
2. [Audit Terminology](#audit-terminology)
3. [Policy and Standards Terms](#policy-and-standards-terms)
4. [Regulatory Terms](#regulatory-terms)
5. [Risk Management Terms](#risk-management-terms)

---

## GRC Fundamentals

GRC (Governance, Risk, and Compliance) is a structured approach to aligning IT with business goals while managing risks and meeting regulatory requirements.

### Core GRC Components

#### Governance
The system of rules, policies, practices, and structures that guide how an organization operates and makes decisions.

**Key elements**:
- Leadership and organizational structure
- Decision-making frameworks
- Accountability mechanisms
- Strategic alignment
- Performance monitoring

**In cybersecurity context**: Defines who is responsible for security decisions, how security strategy aligns with business objectives, and how security performance is measured.

**Use in context**: "Our governance framework ensures security investments align with business risk priorities."

#### Risk Management
The process of identifying, assessing, and controlling threats and risks to the organization.

**Risk types**:
- **Cybersecurity risk**: Threats to IT systems and data
- **Operational risk**: Business process failures
- **Compliance risk**: Regulatory violations
- **Strategic risk**: Business environment changes
- **Reputational risk**: Public perception damage

**Risk management process**:
1. Risk identification
2. Risk assessment
3. Risk treatment
4. Risk monitoring

**Use in context**: "Risk management identified unpatched systems as our highest priority vulnerability."

#### Compliance
Adhering to laws, regulations, and internal policies that apply to an organization's operations.

**Compliance types**:
- **Regulatory compliance**: Government regulations (GDPR, PDPA)
- **Industry compliance**: Sector standards (PCI-DSS, HIPAA)
- **Corporate compliance**: Internal policies
- **Contractual compliance**: Customer requirements

**Use in context**: "Compliance requires us to encrypt all customer data at rest and in transit."

### GRC Roles and Responsibilities

#### Chief Information Security Officer (CISO)
Senior executive responsible for establishing and maintaining the organization's security vision, strategy, and program.

**Responsibilities**:
- Develop security strategy
- Manage security team
- Report to board/executive leadership
- Oversee security investments
- Drive security culture

#### Chief Compliance Officer (CCO)
Executive responsible for driving regulatory compliance and ethical behavior across the organization.

**Responsibilities**:
- Interpret applicable regulations
- Monitor compliance across departments
- Conduct training and awareness
- Investigate violations
- Report to leadership

#### Data Protection Officer (DPO)
Required by GDPR for certain organizations. Independent officer responsible for data protection compliance.

**Responsibilities**:
- Monitor GDPR compliance
- Advise on data protection impact assessments
- Cooperate with supervisory authorities
- Serve as contact point for data subjects

**Use in context**: "Our DPO reviewed the new customer data processing before launch."

#### Internal Audit
Independent function providing assurance on GRC program effectiveness.

**Responsibilities**:
- Audit GRC processes
- Issue recommendations
- Report findings to management and board
- Follow up on remediation

### GRC Frameworks

#### COBIT (Control Objectives for Information and Related Technologies)
A framework for IT governance and management that helps organizations develop, implement, and improve IT management practices.

**Components**:
- Governance objectives
- Management objectives
- Design factors
- Focus areas

#### COSO (Committee of Sponsoring Organizations)
Framework for internal control and enterprise risk management.

**COSO ERM Components**:
1. Governance and culture
2. Strategy and objective setting
3. Performance
4. Review and revision
5. Information, communication, and reporting

#### NIST Cybersecurity Framework (CSF)
Voluntary framework for managing cybersecurity risk.

**Core functions**:
| Function | Purpose |
|----------|---------|
| **Identify** | Understand assets and risks |
| **Protect** | Implement safeguards |
| **Detect** | Identify security events |
| **Respond** | Take action on incidents |
| **Recover** | Restore capabilities |

---

## Audit Terminology

### Audit Types

#### Internal Audit
Assessment conducted by the organization's own audit function or an independent auditor reporting to management.

**Characteristics**:
- Regular cadence
- Identifies control weaknesses
- Recommends improvements
- Reports to audit committee

#### External Audit
Assessment conducted by an independent third party, often for regulatory or certification purposes.

**Triggers**:
- Regulatory requirements
- Certification audits
- Customer requirements
- Due diligence

#### Compliance Audit
Assessment focused on adherence to specific regulations, standards, or policies.

**Examples**: GDPR compliance audit, PCI-DSS audit, SOX audit

#### Security Audit
Assessment of an organization's security controls, policies, and practices.

**Focus areas**:
- Technical controls
- Administrative controls
- Physical controls
- Security policies
- Incident response capabilities

### Audit Process Terms

#### Audit Scope
The boundaries of an audit, defining what systems, processes, and timeframes are included.

**Use in context**: "The audit scope includes all production systems processing customer data."

#### Audit Evidence
Documentation and information collected during an audit to support findings.

**Types**:
- System configurations
- Policy documents
- Log files
- Screenshots
- Interview notes
- Test results

#### Control Testing
Evaluating whether security controls are properly designed and operating effectively.

**Test types**:
- **Design effectiveness**: Is the control properly designed?
- **Operating effectiveness**: Is the control working as intended?

#### Audit Finding
A gap or deficiency identified during an audit.

**Finding components**:
- Condition (what was found)
- Criteria (what should be)
- Cause (why gap exists)
- Effect (risk/impact)
- Recommendation (how to fix)

**Finding ratings**:
| Rating | Description |
|--------|-------------|
| Critical | Immediate action required |
| High | Significant risk requiring prompt attention |
| Medium | Moderate risk needing remediation |
| Low | Minor issue for awareness |
| Observation | Best practice recommendation |

#### Remediation
Actions taken to address audit findings and close gaps.

**Remediation plan includes**:
- Action items
- Responsible parties
- Target dates
- Evidence of completion

#### Audit Trail
A chronological record of system activities enabling reconstruction of events.

**Contains**:
- Who (user identity)
- What (action taken)
- When (timestamp)
- Where (system/location)
- Outcome (success/failure)

**Use in context**: "The audit trail shows who accessed the customer database and when."

### Attestations and Certifications

#### SOC 2 (System and Organization Controls 2)
An audit report on controls relevant to security, availability, processing integrity, confidentiality, and privacy at a service organization.

**Trust Service Criteria**:
- Security
- Availability
- Processing Integrity
- Confidentiality
- Privacy

**Report types**:
- **Type I**: Controls design at a point in time
- **Type II**: Controls design and operating effectiveness over a period

**Use in context**: "We require SOC 2 Type II reports from all cloud vendors."

#### ISO 27001
International standard for information security management systems (ISMS).

**Key elements**:
- Risk assessment
- Control implementation
- Continuous improvement
- Management commitment

**Certification**: Third-party audit by accredited certification body

#### PCI-DSS (Payment Card Industry Data Security Standard)
Security standard for organizations handling credit card data.

**12 Requirements** (summarized):
1. Install and maintain firewalls
2. Change default passwords
3. Protect stored cardholder data
4. Encrypt cardholder data transmission
5. Use and update antivirus
6. Develop secure systems
7. Restrict data access
8. Assign unique IDs
9. Restrict physical access
10. Track and monitor access
11. Test security systems
12. Maintain security policy

**Compliance levels**: Based on transaction volume

---

## Policy and Standards Terms

### Document Hierarchy

#### Policy
High-level statement of management intent and direction for achieving security objectives.

**Characteristics**:
- Mandates requirements
- Approved by executive leadership
- Broadly applicable
- Infrequently changed

**Examples**: Information Security Policy, Acceptable Use Policy, Data Protection Policy

**Use in context**: "Our Information Security Policy requires multi-factor authentication for all privileged access."

#### Standard
Mandatory requirements for implementing policy objectives, often technical specifications.

**Characteristics**:
- Specific and measurable
- Technology or process focused
- Updated more frequently
- References industry standards

**Examples**: Password Standard, Encryption Standard, System Hardening Standard

**Use in context**: "Our password standard requires 14+ characters with complexity requirements."

#### Procedure
Step-by-step instructions for performing specific tasks or activities.

**Characteristics**:
- Detailed and specific
- Task-oriented
- Easily updatable
- Role-specific

**Examples**: Incident Response Procedure, User Provisioning Procedure, Backup Procedure

#### Guideline
Recommended practices that are not mandatory but represent best practices.

**Characteristics**:
- Advisory in nature
- Provides flexibility
- Helps with interpretation
- Suggests approaches

### Document Hierarchy Pyramid

```
              ┌─────────────┐
              │   Policy    │  ← What (high-level direction)
              │ (Mandatory) │
              ├─────────────┤
              │  Standard   │  ← What specifically (requirements)
              │ (Mandatory) │
         ┌────┴─────────────┴────┐
         │      Procedure        │  ← How (step-by-step)
         │     (Mandatory)       │
    ┌────┴───────────────────────┴────┐
    │           Guideline             │  ← Suggestions (recommended)
    │         (Recommended)           │
    └─────────────────────────────────┘
```

### Policy Management Terms

#### Policy Exception
Formal approval to deviate from a policy requirement, typically with compensating controls.

**Exception process**:
1. Business justification
2. Risk assessment
3. Compensating controls
4. Approval authority
5. Time limit
6. Regular review

**Use in context**: "We granted a policy exception for the legacy system, with enhanced monitoring as a compensating control."

#### Compensating Control
An alternative control implemented when the primary control cannot be applied.

**Requirements**:
- Address same risk
- Provide equivalent protection
- Be documented and approved

#### Policy Review
Regular assessment to ensure policies remain current and effective.

**Typical review cycle**: Annually or after significant changes

### Security Frameworks and Standards

#### NIST Special Publications
US government cybersecurity guidance documents.

**Key publications**:
| Publication | Topic |
|-------------|-------|
| SP 800-53 | Security and Privacy Controls |
| SP 800-61 | Incident Handling |
| SP 800-171 | Protecting CUI |
| SP 800-63 | Digital Identity Guidelines |

#### CIS Controls (Center for Internet Security)
Prioritized set of actions to protect organizations from known attack vectors.

**Control categories**:
- Basic (foundational)
- Foundational (essential)
- Organizational (advanced)

**Implementation Groups (IG)**:
- IG1: Essential cyber hygiene
- IG2: Medium enterprise
- IG3: Large enterprise with sensitive data

---

## Regulatory Terms

### Data Protection Regulations

#### GDPR (General Data Protection Regulation)
European Union regulation on data protection and privacy, effective May 25, 2018.

**Scope**: Applies to any organization processing EU residents' personal data.

**Key principles**:
1. **Lawfulness, fairness, transparency**: Clear legal basis for processing
2. **Purpose limitation**: Collect only for specified purposes
3. **Data minimization**: Collect only what is necessary
4. **Accuracy**: Keep data accurate and up to date
5. **Storage limitation**: Retain only as long as necessary
6. **Integrity and confidentiality**: Protect data security
7. **Accountability**: Demonstrate compliance

**Key rights** (data subject rights):
- Right to access
- Right to rectification
- Right to erasure ("right to be forgotten")
- Right to restrict processing
- Right to data portability
- Right to object

**Breach notification**: 72 hours to supervisory authority

**Penalties**: Up to EUR 20 million or 4% of global annual revenue

**Use in context**: "GDPR requires us to notify the supervisory authority within 72 hours of discovering a data breach."

#### PDPA (Personal Data Protection Act)
Data protection laws in various countries (notably Singapore and Thailand).

**Singapore PDPA** key requirements:
- Consent obligation
- Purpose limitation
- Notification obligation
- Access and correction rights
- Accuracy obligation
- Protection obligation
- Retention limitation
- Transfer limitation
- Openness obligation

**Penalties** (Singapore): Up to SGD 1 million

#### CCPA/CPRA (California Consumer Privacy Act/California Privacy Rights Act)
California state privacy law providing consumer data rights.

**Key rights**:
- Right to know what data is collected
- Right to delete personal information
- Right to opt-out of data sale
- Right to non-discrimination

#### HIPAA (Health Insurance Portability and Accountability Act)
US law protecting health information.

**Key components**:
- **Privacy Rule**: Standards for PHI use and disclosure
- **Security Rule**: Technical, physical, and administrative safeguards
- **Breach Notification Rule**: Notification requirements

**Protected Health Information (PHI)**: Any health information linked to an individual

### Regulatory Concepts

#### Personal Data
Any information relating to an identified or identifiable natural person.

**Examples**:
- Name
- Identification number
- Location data
- Online identifiers
- Physical, genetic, mental, economic, cultural, or social identity factors

#### Data Subject
The individual whose personal data is being processed.

#### Data Controller
The entity that determines the purposes and means of processing personal data.

**Use in context**: "As the data controller, we are responsible for ensuring lawful processing."

#### Data Processor
An entity that processes data on behalf of the controller.

**Examples**: Cloud providers, payroll processors, marketing agencies

#### Supervisory Authority
The government body responsible for enforcing data protection regulations.

**Examples**:
- UK: Information Commissioner's Office (ICO)
- Singapore: Personal Data Protection Commission (PDPC)
- France: Commission Nationale de l'Informatique et des Libertes (CNIL)

#### Data Breach
A security incident that results in unauthorized access, disclosure, or loss of personal data.

**Breach notification requirements**:
| Regulation | Timeline | Recipient |
|------------|----------|-----------|
| GDPR | 72 hours | Supervisory authority |
| HIPAA | 60 days | HHS and individuals |
| Singapore PDPA | "As soon as practicable" | PDPC |

#### Privacy Impact Assessment (PIA) / Data Protection Impact Assessment (DPIA)
A process to identify and minimize data protection risks of a project or system.

**Required when**:
- Processing likely to result in high risk
- Large-scale processing of sensitive data
- Systematic monitoring of public areas

**Assessment contents**:
- Description of processing
- Assessment of necessity and proportionality
- Assessment of risks to individuals
- Measures to address risks

---

## Risk Management Terms

### Risk Assessment

#### Risk
The potential for loss or damage when a threat exploits a vulnerability.

**Risk formula**: Risk = Threat x Vulnerability x Impact

#### Threat
Any circumstance or event with the potential to cause harm to an asset.

**Threat sources**:
- Natural (earthquake, flood)
- Human intentional (hackers, insiders)
- Human unintentional (errors, accidents)
- Technical (system failure)

#### Vulnerability
A weakness that can be exploited by a threat.

**Examples**: Unpatched software, weak passwords, misconfiguration

#### Impact
The consequence or harm resulting from a threat exploiting a vulnerability.

**Impact categories**:
- Financial loss
- Reputational damage
- Operational disruption
- Legal liability
- Regulatory penalties

#### Likelihood
The probability that a threat will exploit a vulnerability.

**Assessment factors**:
- Historical occurrence
- Threat actor motivation
- Vulnerability accessibility
- Existing controls

### Risk Treatment Options

#### Risk Acceptance
Acknowledging a risk and choosing to retain it without additional controls.

**When appropriate**:
- Cost of mitigation exceeds potential loss
- Risk is within risk appetite
- No feasible mitigation exists

**Requires**: Documented approval from appropriate authority

#### Risk Mitigation
Implementing controls to reduce the likelihood or impact of a risk.

**Examples**:
- Installing security controls
- Implementing policies
- Training employees
- Patching vulnerabilities

#### Risk Transfer
Shifting risk to another party, typically through insurance or contracts.

**Examples**:
- Cyber insurance
- Vendor contracts with liability clauses
- Outsourcing to managed service providers

#### Risk Avoidance
Eliminating the risk by not engaging in the risky activity.

**Examples**:
- Not collecting certain data
- Discontinuing vulnerable services
- Not entering certain markets

### Risk Management Concepts

#### Risk Appetite
The amount and type of risk an organization is willing to accept in pursuit of objectives.

**Use in context**: "Our risk appetite does not allow for unencrypted storage of customer data."

#### Risk Tolerance
The acceptable level of variation around specific objectives.

**Relationship**: Risk tolerance is more specific than risk appetite

#### Risk Register
A documented list of identified risks, their assessments, and treatment plans.

**Register contents**:
- Risk ID and description
- Likelihood and impact ratings
- Risk score/priority
- Risk owner
- Treatment plan
- Status

#### Residual Risk
The risk remaining after controls are applied.

**Formula**: Residual Risk = Inherent Risk - Control Effectiveness

#### Inherent Risk
The risk level before controls are applied.

#### Key Risk Indicator (KRI)
A metric used to monitor risk levels and provide early warning of risk changes.

**Examples**:
- Number of unpatched critical vulnerabilities
- Percentage of users without MFA
- Number of failed login attempts
- Time to patch critical vulnerabilities

**Use in context**: "Our KRIs show an increase in phishing attempts this quarter."

### Business Continuity Terms

#### BCP (Business Continuity Plan)
A plan for maintaining business operations during and after a disaster or disruption.

#### DRP (Disaster Recovery Plan)
A plan specifically focused on recovering IT systems and data after a disaster.

#### RTO (Recovery Time Objective)
The maximum acceptable time to restore a system or process after a disruption.

**Use in context**: "Our critical systems have an RTO of 4 hours."

#### RPO (Recovery Point Objective)
The maximum acceptable data loss measured in time (how old the restored data can be).

**Use in context**: "With an RPO of 1 hour, we need backup frequency of at least hourly."

#### BIA (Business Impact Analysis)
Assessment of how disruptions would affect business operations and what resources are needed for recovery.

---

## Summary

This document covers governance, risk, and compliance terminology across five key areas:

1. **GRC Fundamentals**: Governance, risk management, compliance, and key roles
2. **Audit Terminology**: Audit types, processes, attestations, and certifications
3. **Policy and Standards**: Document hierarchy and framework references
4. **Regulatory Terms**: Data protection regulations (GDPR, PDPA, HIPAA)
5. **Risk Management**: Risk assessment, treatment, and business continuity

For industry slang and common jargon, see [04-slang-and-jargon.md](./04-slang-and-jargon.md).

---

## References

- [AWS - What is GRC?](https://aws.amazon.com/what-is/grc/)
- [IBM - What is GRC?](https://www.ibm.com/think/topics/grc)
- [GDPR.eu - What is GDPR?](https://gdpr.eu/what-is-gdpr/)
- [NIST Cybersecurity Framework](https://www.nist.gov/cyberframework)
- [OCEG - What is GRC?](https://www.oceg.org/ideas/what-is-grc/)
- [TechTarget - GDPR Explained](https://www.techtarget.com/whatis/definition/General-Data-Protection-Regulation-GDPR)
