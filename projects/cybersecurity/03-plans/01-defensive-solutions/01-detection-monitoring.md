# Detection and Monitoring Solutions

> Strategic planning guide for implementing detection and monitoring capabilities in a government cybersecurity environment.

**Last Updated**: January 2026

**NIST CSF 2.0 Alignment**: DETECT (DE) - Continuous Monitoring (DE.CM), Adverse Event Analysis (DE.AE)

---

## Table of Contents

1. [Executive Summary](#executive-summary)
2. [SIEM Implementation](#siem-implementation)
3. [EDR/XDR Deployment](#edrxdr-deployment)
4. [Network Detection and Response (NDR)](#network-detection-and-response-ndr)
5. [Log Management and Analysis](#log-management-and-analysis)
6. [Threat Detection Capabilities](#threat-detection-capabilities)
7. [AI-Powered Detection](#ai-powered-detection)
8. [Integration Architecture](#integration-architecture)
9. [Vendor Landscape](#vendor-landscape)
10. [Implementation Roadmap](#implementation-roadmap)

---

## Executive Summary

### Detection Challenges in 2025-2026

The detection landscape faces unprecedented challenges:

| Challenge | Singapore Context | Impact |
|-----------|-------------------|--------|
| **APT Dwell Time** | UNC3886 uses LoTL techniques | Difficult to detect with signatures |
| **Alert Volume** | 1,925 attacks/week globally | SOC fatigue, missed threats |
| **Talent Shortage** | 4,000 unfilled positions | Need for automation |
| **AI-Powered Attacks** | 12% of phishing AI-generated | Traditional detection failing |

### Detection Maturity Model

| Level | Capability | Description |
|-------|------------|-------------|
| **Level 1** | Basic | Signature-based AV, basic logging |
| **Level 2** | Reactive | SIEM alerts, manual investigation |
| **Level 3** | Proactive | Threat hunting, behavioral analytics |
| **Level 4** | Predictive | AI/ML detection, automated response |
| **Level 5** | Adaptive | Continuous improvement, threat intel integration |

**Target**: Government cybersecurity units should aim for Level 4-5.

---

## SIEM Implementation

### Overview

Security Information and Event Management (SIEM) provides centralized log collection, correlation, and alerting across the enterprise.

### Core Requirements

#### Data Collection

| Source Category | Examples | Priority |
|-----------------|----------|----------|
| **Security Devices** | Firewalls, IDS/IPS, WAF | Critical |
| **Endpoints** | Windows, Linux, macOS | Critical |
| **Identity** | Active Directory, IAM, MFA | Critical |
| **Cloud** | AWS, Azure, GCP audit logs | High |
| **Applications** | Web servers, databases | High |
| **Network** | Flow data, DNS, proxy | High |
| **OT/ICS** | SCADA, PLCs (where applicable) | Medium-High |

#### Log Volume Estimation

| Environment Size | Daily Log Volume | Storage (90 days) |
|------------------|------------------|-------------------|
| Small (<1,000 endpoints) | 50-100 GB/day | 5-10 TB |
| Medium (1,000-10,000) | 100-500 GB/day | 10-50 TB |
| Large (10,000-50,000) | 500 GB-2 TB/day | 50-200 TB |
| Enterprise (50,000+) | 2-10+ TB/day | 200 TB-1+ PB |

### SIEM Architecture Options

#### Option 1: Cloud-Native SIEM

```
+------------------+     +------------------+     +------------------+
|  Log Sources     | --> |  Cloud SIEM      | --> |  Analyst         |
|  (On-Prem/Cloud) |     |  (Microsoft      |     |  Workstation     |
|                  |     |   Sentinel)      |     |                  |
+------------------+     +------------------+     +------------------+
                               |
                               v
                         +------------------+
                         |  SOAR Platform   |
                         |  (Automated      |
                         |   Response)      |
                         +------------------+
```

**Advantages**:
- Rapid deployment
- Automatic scaling
- Lower infrastructure management
- Integration with cloud workloads

**Considerations**:
- Data residency requirements (Singapore data sovereignty)
- Network bandwidth for log shipping
- Ongoing operational costs

#### Option 2: On-Premises SIEM

```
+------------------+     +------------------+     +------------------+
|  Log Collectors  | --> |  SIEM Cluster    | --> |  Analytics       |
|  (Agents/        |     |  (Splunk         |     |  Dashboard       |
|   Syslog)        |     |   Enterprise)    |     |                  |
+------------------+     +------------------+     +------------------+
                               |
                               v
                         +------------------+
                         |  Hot/Warm/Cold   |
                         |  Storage Tiers   |
                         +------------------+
```

**Advantages**:
- Full data control
- No cloud dependency
- Predictable costs at scale
- Compliance with data localization

**Considerations**:
- Higher upfront investment
- Infrastructure management burden
- Scaling complexity

#### Option 3: Hybrid SIEM

**Recommended for government deployments** - combines cloud scalability with on-premises control for sensitive data.

### SIEM Use Case Development

#### Priority Use Cases for Government

| Use Case | MITRE ATT&CK Coverage | Detection Method |
|----------|----------------------|------------------|
| **Credential Theft** | T1003, T1558 | Failed auth patterns, unusual access |
| **Lateral Movement** | T1021, T1076 | Network flow analysis, auth logs |
| **Data Exfiltration** | T1041, T1048 | Volume anomalies, unusual destinations |
| **Malware Activity** | T1059, T1105 | Process execution, network connections |
| **Privilege Escalation** | T1078, T1068 | Privilege changes, admin activity |
| **APT Indicators** | Multiple | Threat intel correlation |

#### Use Case Development Process

1. **Threat Mapping**: Align to MITRE ATT&CK techniques relevant to Singapore threats
2. **Data Source Identification**: Determine required log sources
3. **Detection Logic**: Define correlation rules and thresholds
4. **Tuning**: Reduce false positives through baselining
5. **Validation**: Test with red team or ATT&CK evaluations

### SIEM Vendor Comparison

| Vendor | Deployment | Strengths | Considerations |
|--------|------------|-----------|----------------|
| **Microsoft Sentinel** | Cloud | Azure integration, AI, cost model | Azure-centric |
| **Splunk Enterprise** | On-Prem/Cloud | Flexibility, ecosystem | High cost at scale |
| **Elastic Security** | On-Prem/Cloud | Open source core, flexible | Requires expertise |
| **IBM QRadar** | On-Prem/Cloud | Offense analysis, compliance | Legacy architecture |
| **Chronicle (Google)** | Cloud | Unlimited storage, speed | Google ecosystem |

---

## EDR/XDR Deployment

### Endpoint Detection and Response (EDR)

#### Core Capabilities

| Capability | Description | Threat Coverage |
|------------|-------------|-----------------|
| **Continuous Recording** | Full process, network, file activity | Forensics, hunting |
| **Behavioral Detection** | ML-based anomaly detection | Zero-day, fileless |
| **Threat Intelligence** | IOC matching, reputation | Known threats |
| **Response Actions** | Isolation, kill process, quarantine | Containment |
| **Investigation** | Timeline, process tree, pivoting | Analysis |

#### Deployment Considerations

| Factor | Recommendation |
|--------|----------------|
| **Coverage** | 100% of managed endpoints |
| **Agent Management** | Centralized console, auto-update |
| **Performance** | Resource impact assessment |
| **Offline Protection** | Local detection capability |
| **Integration** | SIEM, SOAR, threat intel |

### Extended Detection and Response (XDR)

XDR extends EDR to include network, cloud, email, and identity telemetry.

#### XDR Architecture

```
+------------+  +------------+  +------------+  +------------+
|  Endpoint  |  |  Network   |  |   Email    |  |  Identity  |
|    EDR     |  |    NDR     |  |  Security  |  |   (IAM)    |
+------------+  +------------+  +------------+  +------------+
       |              |              |              |
       +------+-------+------+-------+------+-------+
              |              |              |
              v              v              v
        +----------------------------------------+
        |              XDR Platform              |
        |  - Unified Detection                   |
        |  - Cross-Domain Correlation            |
        |  - Automated Investigation             |
        |  - Coordinated Response                |
        +----------------------------------------+
```

#### XDR Benefits for Government

| Benefit | Description |
|---------|-------------|
| **Unified Visibility** | Single console for all domains |
| **Faster Investigation** | Automated correlation reduces MTTR |
| **Reduced Alert Fatigue** | Consolidated, high-fidelity alerts |
| **Coordinated Response** | Cross-domain containment actions |

### EDR/XDR Vendor Comparison

| Vendor | Type | Strengths | MITRE ATT&CK Performance |
|--------|------|-----------|--------------------------|
| **CrowdStrike Falcon** | XDR | Cloud-native, threat intel, lightweight | Industry leading |
| **Microsoft Defender XDR** | XDR | M365 integration, comprehensive | Strong across domains |
| **SentinelOne** | XDR | Autonomous response, speed | High detection rate |
| **Palo Alto Cortex XDR** | XDR | Network integration, analytics | Strong protection |
| **VMware Carbon Black** | EDR/XDR | Hybrid support, custom rules | Good enterprise fit |

### Deployment Strategy

#### Phase 1: Pilot (1-2 months)
- Deploy to 500-1,000 diverse endpoints
- Validate detection efficacy
- Assess performance impact
- Integration testing

#### Phase 2: Rollout (3-6 months)
- Staged deployment by department/criticality
- Policy tuning based on pilot learnings
- SOC playbook development

#### Phase 3: Optimization (Ongoing)
- Threat hunting program activation
- Advanced detection rule development
- Red team validation

---

## Network Detection and Response (NDR)

### Overview

NDR provides visibility into network traffic patterns and threats that evade endpoint detection.

### Core Capabilities

| Capability | Description | Use Case |
|------------|-------------|----------|
| **Traffic Analysis** | Deep packet inspection, metadata | Malware C2, exfiltration |
| **Behavioral Analytics** | Baseline deviation detection | Lateral movement, insider threat |
| **Protocol Analysis** | Application-layer visibility | Protocol abuse, tunneling |
| **Encrypted Traffic Analysis** | JA3/JA4 fingerprinting, metadata | TLS-encrypted threats |
| **Threat Intelligence** | IOC correlation | Known malicious infrastructure |

### NDR Architecture

#### Sensor Placement

```
                    +------------------+
                    |    Internet      |
                    +--------+---------+
                             |
                    +--------+---------+
                    |  Perimeter FW    |  <-- NDR Sensor (North-South)
                    +--------+---------+
                             |
              +--------------+--------------+
              |                             |
     +--------+---------+          +--------+---------+
     |   DMZ Network    |          |  Internal Net    |
     +--------+---------+          +--------+---------+
              |                             |
     +--------+---------+          +--------+---------+
     |  NDR Sensor      |          |  NDR Sensor      | <-- (East-West)
     |  (DMZ Traffic)   |          |  (Core Traffic)  |
     +------------------+          +--------+---------+
                                            |
                                   +--------+---------+
                                   |  Sensitive       |
                                   |  Segments        |
                                   +--------+---------+
                                            |
                                   +--------+---------+
                                   |  NDR Sensor      | <-- (Critical Assets)
                                   +------------------+
```

### Deployment Considerations

| Factor | Recommendation |
|--------|----------------|
| **Traffic Mirroring** | SPAN/TAP at key points |
| **Bandwidth** | Ensure sensors handle peak traffic |
| **Encryption** | Plan for TLS 1.3, consider decryption |
| **Storage** | 30-90 days of metadata, PCAP for incidents |
| **Integration** | SIEM, XDR, SOAR bidirectional |

### NDR for OT/ICS Environments

For government units with OT responsibilities:

| Consideration | Approach |
|---------------|----------|
| **Passive Monitoring** | Non-intrusive, no traffic injection |
| **Protocol Support** | Modbus, DNP3, OPC, BACnet |
| **Asset Discovery** | Automated OT device inventory |
| **Anomaly Detection** | Process behavior baselines |
| **Safety** | No impact on safety systems |

### NDR Vendor Comparison

| Vendor | Strengths | OT Support | AI/ML Capability |
|--------|-----------|------------|------------------|
| **Vectra AI** | Strong ML, identity focus | Limited | Advanced |
| **Darktrace** | Self-learning AI, autonomous | Good | Industry leading |
| **ExtraHop** | Performance analytics, cloud | Limited | Strong |
| **Corelight** | Zeek-based, open format | Limited | Good |
| **Claroty** | Purpose-built OT | Excellent | Good |
| **Nozomi Networks** | OT/IoT focus | Excellent | Good |

---

## Log Management and Analysis

### Log Retention Requirements

#### Regulatory Requirements

| Regulation | Minimum Retention | Log Types |
|------------|-------------------|-----------|
| **Cybersecurity Act** | As required by sector | CII-related logs |
| **MAS TRM** | 7 years | Financial transaction logs |
| **PDPA** | Reasonable period | Personal data access logs |
| **IM8** | Per classification | Government system logs |
| **Best Practice** | 1-7 years | Security-relevant logs |

#### Recommended Retention Tiers

| Tier | Retention | Log Types | Storage |
|------|-----------|-----------|---------|
| **Hot** | 30-90 days | Active investigation | Fast SSD |
| **Warm** | 90-365 days | Compliance, hunting | Standard |
| **Cold** | 1-7 years | Archive, legal | Object storage |

### Log Normalization

#### Common Event Format (CEF) / OCSF

Normalize logs to a common schema for:
- Consistent correlation rules
- Cross-source analysis
- Vendor independence

#### Key Normalized Fields

| Field | Description | Example |
|-------|-------------|---------|
| **timestamp** | Event time (UTC) | 2026-01-20T10:30:00Z |
| **source.ip** | Origin IP address | 192.168.1.100 |
| **destination.ip** | Target IP address | 10.0.0.50 |
| **user.name** | User account | john.doe |
| **action** | Event action | login, file_access |
| **outcome** | Success/failure | success |

### Log Analysis Techniques

| Technique | Purpose | Tools |
|-----------|---------|-------|
| **Statistical Analysis** | Baseline deviation | SIEM analytics |
| **Frequency Analysis** | Unusual patterns | Custom queries |
| **Link Analysis** | Entity relationships | Graph databases |
| **Timeline Analysis** | Incident reconstruction | SIEM, forensic tools |
| **ML Clustering** | Anomaly grouping | AI/ML platforms |

---

## Threat Detection Capabilities

### Detection Engineering Program

#### Detection Content Lifecycle

```
+----------+     +----------+     +----------+     +----------+
|  Threat  | --> |  Rule    | --> |  Test    | --> |  Deploy  |
|  Intel   |     |  Dev     |     |  Validate|     |  Tune    |
+----------+     +----------+     +----------+     +----------+
     ^                                                  |
     |                                                  |
     +--------------------------------------------------+
                    Continuous Improvement
```

#### Detection Categories

| Category | Description | False Positive Rate |
|----------|-------------|---------------------|
| **Signature-Based** | Known IOCs, patterns | Low |
| **Heuristic** | Suspicious behaviors | Medium |
| **Behavioral** | Baseline deviations | Medium-High |
| **ML-Based** | Statistical anomalies | Varies |
| **Threat Intel** | TTP matching | Low-Medium |

### MITRE ATT&CK Coverage

#### Priority Techniques for Singapore Threat Landscape

| Tactic | Priority Techniques | Detection Source |
|--------|---------------------|------------------|
| **Initial Access** | T1566 (Phishing), T1078 (Valid Accounts) | Email, Auth logs |
| **Execution** | T1059 (Scripting), T1204 (User Execution) | Endpoint, Process |
| **Persistence** | T1547 (Boot/Logon), T1053 (Scheduled Task) | Registry, Endpoint |
| **Privilege Escalation** | T1068 (Exploitation), T1134 (Token) | Endpoint, Auth |
| **Defense Evasion** | T1055 (Injection), T1070 (Log Clear) | Endpoint, SIEM |
| **Credential Access** | T1003 (OS Credential), T1558 (Kerberos) | Endpoint, AD |
| **Discovery** | T1087 (Account), T1083 (File Discovery) | Endpoint, AD |
| **Lateral Movement** | T1021 (Remote Services) | Network, Auth |
| **Collection** | T1074 (Data Staged) | Endpoint, Network |
| **Exfiltration** | T1041 (C2 Channel), T1048 (Alt Protocol) | Network, Proxy |

### Threat Hunting Program

#### Hunting Approaches

| Approach | Description | Trigger |
|----------|-------------|---------|
| **Hypothesis-Driven** | Test specific threat theories | Intel, research |
| **Intel-Driven** | Hunt for known TTPs | Threat reports |
| **Data-Driven** | Statistical anomalies | Analytics |
| **Situational** | Response to events | Incidents, alerts |

#### Hunting Cadence

| Hunt Type | Frequency | Focus |
|-----------|-----------|-------|
| **APT Hunt** | Weekly | UNC3886, Volt Typhoon TTPs |
| **Credential Abuse** | Weekly | Anomalous authentication |
| **Lateral Movement** | Weekly | Internal traffic patterns |
| **Data Exfiltration** | Bi-weekly | Outbound anomalies |
| **Living Off the Land** | Bi-weekly | Native tool abuse |

---

## AI-Powered Detection

### AI/ML Detection Use Cases

| Use Case | ML Technique | Benefit |
|----------|--------------|---------|
| **Anomaly Detection** | Unsupervised learning | Zero-day detection |
| **User Behavior Analytics** | Sequence modeling | Insider threat |
| **Malware Classification** | Supervised learning | Speed, accuracy |
| **Alert Prioritization** | Risk scoring | SOC efficiency |
| **Entity Resolution** | Graph analytics | Investigation |
| **Phishing Detection** | NLP, image analysis | AI-generated content |

### CISA AI Integration Model

Based on CISA's AI use cases:

| Application | Description | Implementation |
|-------------|-------------|----------------|
| **Malware Analysis** | Deep learning for triage | Sandbox integration |
| **CyberSentry** | Unsupervised ML for anomalies | Network monitoring |
| **Threat Intelligence** | AI-accelerated analysis | TI platform |

### AI Detection Challenges

| Challenge | Mitigation |
|-----------|------------|
| **Explainability** | Use interpretable models, explain alerts |
| **Adversarial ML** | Model robustness testing, ensemble |
| **Data Quality** | Clean, labeled training data |
| **Drift** | Continuous model retraining |
| **False Positives** | Human-in-the-loop validation |

### AI-Enabled SOC Model

```
+------------------+     +------------------+     +------------------+
|  Data Sources    | --> |  AI Platform     | --> |  Analyst Tier    |
|  (Logs, Network, |     |  - ML Detection  |     |  - Validation    |
|   Endpoints)     |     |  - Correlation   |     |  - Investigation |
+------------------+     |  - Prioritization|     |  - Escalation    |
                         +------------------+     +------------------+
                                |                        |
                                v                        v
                         +------------------+     +------------------+
                         |  Automated       |     |  Human Decision  |
                         |  Response        |     |  (Complex Cases) |
                         +------------------+     +------------------+
```

---

## Integration Architecture

### Detection Ecosystem Integration

```
                    +-------------------+
                    |   Threat Intel    |
                    |   Platform        |
                    +--------+----------+
                             |
                             v
+----------+  +----------+  +----------+  +----------+
|   SIEM   |--|   XDR    |--|   NDR    |--|   UEBA   |
+----------+  +----------+  +----------+  +----------+
     |             |             |             |
     +-------------+-------------+-------------+
                         |
                         v
                +------------------+
                |   SOAR Platform  |
                |   (Orchestration)|
                +------------------+
                         |
                         v
                +------------------+
                |   Case Mgmt /    |
                |   Ticketing      |
                +------------------+
```

### Integration Standards

| Standard | Purpose | Usage |
|----------|---------|-------|
| **STIX/TAXII** | Threat intelligence exchange | TI feeds |
| **CEF/LEEF** | Log format standardization | SIEM ingestion |
| **OCSF** | Open Cybersecurity Schema | Cross-platform |
| **REST APIs** | Platform integration | Automation |
| **Webhooks** | Real-time notifications | Alerting |

### Key Integrations

| Integration | Direction | Data Flow |
|-------------|-----------|-----------|
| **EDR to SIEM** | EDR --> SIEM | Telemetry, alerts |
| **SIEM to SOAR** | SIEM --> SOAR | Alerts for automation |
| **NDR to XDR** | NDR --> XDR | Network context |
| **TI to All** | TIP --> All | IOCs, TTPs |
| **All to Ticketing** | All --> Ticket | Cases, incidents |

---

## Vendor Landscape

### Comprehensive Vendor Matrix

#### SIEM Vendors

| Vendor | Licensing | Cloud/On-Prem | Singapore DC | Government Use |
|--------|-----------|---------------|--------------|----------------|
| **Microsoft Sentinel** | Consumption | Cloud | Azure SG | Common |
| **Splunk Enterprise** | Data volume | Both | Partner | Common |
| **Elastic Security** | Nodes/capacity | Both | AWS/Self | Growing |
| **IBM QRadar** | EPS | Both | Partner | Legacy common |
| **Chronicle** | Unlimited | Cloud | Google SG | Limited |

#### EDR/XDR Vendors

| Vendor | Licensing | Deployment | Government Certifications |
|--------|-----------|------------|---------------------------|
| **CrowdStrike** | Per endpoint | Cloud | FedRAMP, multiple |
| **Microsoft Defender** | M365/Standalone | Cloud | Multiple |
| **SentinelOne** | Per endpoint | Cloud/Hybrid | FedRAMP, SOC2 |
| **Palo Alto Cortex** | Per endpoint | Cloud | Multiple |
| **VMware Carbon Black** | Per endpoint | Both | Multiple |

#### NDR Vendors

| Vendor | Focus | OT Capability | AI/ML |
|--------|-------|---------------|-------|
| **Vectra AI** | Enterprise IT | Limited | Strong |
| **Darktrace** | Self-learning | Good | Industry leading |
| **ExtraHop** | Performance | Limited | Strong |
| **Claroty** | OT/ICS | Excellent | Good |
| **Nozomi Networks** | OT/IoT | Excellent | Good |

### Singapore-Based Partners

| Partner | Services | Specialization |
|---------|----------|----------------|
| **Ensign InfoSecurity** | MSSP, SOC, TI | Full spectrum |
| **Singtel Trustwave** | MSSP, MDR | Enterprise |
| **StarHub Cybersecurity** | MSSP, managed | Telco integration |
| **Horangi** | Cloud security | AWS/Azure |

---

## Implementation Roadmap

### Phase 1: Foundation (Months 1-3)

| Activity | Deliverable | Resources |
|----------|-------------|-----------|
| Requirements gathering | Detection requirements doc | Stakeholders |
| Vendor evaluation | Shortlist, POC plan | Procurement |
| Architecture design | Technical design | Architecture team |
| Quick wins | Critical use cases | Security team |

### Phase 2: Core Deployment (Months 4-9)

| Activity | Deliverable | Resources |
|----------|-------------|-----------|
| SIEM deployment | Operational SIEM | Vendor, IT |
| EDR/XDR rollout | Endpoint coverage | Endpoint team |
| Integration | Connected platforms | Integration team |
| Use case development | Detection content | Detection engineers |

### Phase 3: Enhancement (Months 10-18)

| Activity | Deliverable | Resources |
|----------|-------------|-----------|
| NDR deployment | Network visibility | Network team |
| AI/ML enablement | Advanced detection | Data science |
| Threat hunting | Hunting program | Senior analysts |
| Optimization | Tuned environment | SOC team |

### Phase 4: Maturity (Ongoing)

| Activity | Deliverable | Resources |
|----------|-------------|-----------|
| Continuous improvement | Detection KPIs | SOC leadership |
| Red team validation | Coverage reports | Red team |
| Threat intel integration | Enriched detection | TI team |
| Automation expansion | Efficiency gains | Automation team |

---

## Success Metrics

### Detection KPIs

| Metric | Target | Measurement |
|--------|--------|-------------|
| **Mean Time to Detect (MTTD)** | <1 hour | SIEM/XDR |
| **Detection Coverage** | >80% ATT&CK techniques | Coverage mapping |
| **True Positive Rate** | >80% | Alert analysis |
| **False Positive Rate** | <20% | Alert analysis |
| **Log Source Coverage** | 100% critical assets | Inventory |
| **Threat Intel Integration** | >90% relevant feeds | TIP metrics |

### Operational Metrics

| Metric | Target | Measurement |
|--------|--------|-------------|
| **Alert Volume** | Manageable (<500/day) | SIEM |
| **Analyst Efficiency** | >10 cases/analyst/day | Ticketing |
| **Threat Hunt Frequency** | Weekly | Hunt calendar |
| **Detection Rule Updates** | Monthly minimum | Change log |

---

## References

- [NIST SP 800-61r3](https://csrc.nist.gov/publications/detail/sp/800-61/rev-3/final) - Incident Response Recommendations
- [MITRE ATT&CK](https://attack.mitre.org/) - Detection Strategies (v18)
- [CISA AI Use Cases](https://www.dhs.gov/ai/use-case-inventory/cisa) - Government AI Detection
- [CSA Singapore Cyber Landscape 2024/2025](https://www.csa.gov.sg/resources/publications/singapore-cyber-landscape-2024-2025/)
- [CIS Controls v8.1](https://www.cisecurity.org/controls) - Controls 8, 13

---

*For response capabilities, see [03-response-recovery.md](./03-response-recovery.md)*
