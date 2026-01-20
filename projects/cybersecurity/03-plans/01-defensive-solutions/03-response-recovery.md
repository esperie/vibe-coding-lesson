# Response and Recovery Platforms

> Strategic planning guide for implementing incident response and recovery capabilities in a government cybersecurity environment.

**Last Updated**: January 2026

**NIST CSF 2.0 Alignment**: RESPOND (RS) - Incident Management (RS.MA), Incident Analysis (RS.AN), Incident Mitigation (RS.MI); RECOVER (RC) - Incident Recovery Plan Execution (RC.RP)

---

## Table of Contents

1. [Executive Summary](#executive-summary)
2. [SOAR Platform Considerations](#soar-platform-considerations)
3. [Incident Response Automation](#incident-response-automation)
4. [Digital Forensics Capabilities](#digital-forensics-capabilities)
5. [Business Continuity Planning](#business-continuity-planning)
6. [Disaster Recovery Strategies](#disaster-recovery-strategies)
7. [Incident Response Program](#incident-response-program)
8. [Vendor Landscape](#vendor-landscape)
9. [Implementation Roadmap](#implementation-roadmap)

---

## Executive Summary

### Response Challenges in 2025-2026

Effective incident response is critical given the evolving threat landscape:

| Metric | Singapore Context | Response Implication |
|--------|-------------------|---------------------|
| **APT Dwell Time** | Months for sophisticated attacks | Need proactive hunting |
| **Ransomware Speed** | Encryption within hours | Rapid containment critical |
| **Regulatory Timeline** | 2-hour APT notification (CII) | Automated detection and reporting |
| **Talent Shortage** | 4,000 unfilled positions | Automation essential |

### Response Maturity Model

| Level | Capability | Description |
|-------|------------|-------------|
| **Level 1** | Ad-hoc | Manual, unstructured response |
| **Level 2** | Documented | Playbooks exist, manual execution |
| **Level 3** | Managed | Structured process, some automation |
| **Level 4** | Automated | SOAR-driven, rapid response |
| **Level 5** | Optimized | AI-assisted, continuous improvement |

**Target**: Government cybersecurity units should aim for Level 4-5.

---

## SOAR Platform Considerations

### What is SOAR?

Security Orchestration, Automation, and Response (SOAR) platforms integrate security tools and automate incident response workflows.

### Core SOAR Capabilities

| Capability | Description | Benefit |
|------------|-------------|---------|
| **Orchestration** | Connect disparate security tools | Unified operations |
| **Automation** | Execute repetitive tasks automatically | Efficiency, consistency |
| **Case Management** | Track incidents end-to-end | Accountability, audit trail |
| **Playbooks** | Codified response procedures | Standardized response |
| **Metrics/Reporting** | Performance measurement | Continuous improvement |
| **Collaboration** | Team coordination | Effective response |

### SOAR Architecture

```
                    +------------------+
                    |   Alert Sources  |
                    |   (SIEM, XDR,    |
                    |    Email, etc.)  |
                    +--------+---------+
                             |
                             v
                    +------------------+
                    |   SOAR Platform  |
                    |                  |
                    |  +------------+  |
                    |  | Playbooks  |  |
                    |  +------------+  |
                    |  +------------+  |
                    |  | Case Mgmt  |  |
                    |  +------------+  |
                    |  +------------+  |
                    |  | Automation |  |
                    |  +------------+  |
                    +--------+---------+
                             |
         +-------------------+-------------------+
         |                   |                   |
         v                   v                   v
+----------------+  +----------------+  +----------------+
|   Enrichment   |  |   Containment  |  |   Ticketing    |
|   (TI, CMDB)   |  |   (FW, EDR)    |  |   (ServiceNow) |
+----------------+  +----------------+  +----------------+
```

### SOAR Use Cases

#### Priority Use Cases for Government

| Use Case | Automation Level | Time Savings |
|----------|------------------|--------------|
| **Phishing Triage** | Full automation | 15-30 min/alert |
| **Malware Containment** | Semi-automated | Immediate isolation |
| **Threat Intel Enrichment** | Full automation | 5-10 min/indicator |
| **User Account Compromise** | Semi-automated | Faster lockdown |
| **Vulnerability Response** | Workflow automation | Days to hours |
| **Regulatory Reporting** | Automated generation | Hours to minutes |

### SOAR Playbook Examples

#### Phishing Response Playbook

```
+------------------+
|  Phishing Alert  |
|  Received        |
+--------+---------+
         |
         v
+------------------+
|  Extract IOCs    |  <-- Automated
|  (URLs, hashes,  |
|   senders)       |
+--------+---------+
         |
         v
+------------------+
|  Query Threat    |  <-- Automated
|  Intel Feeds     |
+--------+---------+
         |
    +----+----+
    |         |
    v         v
+-------+  +--------+
|Known  |  |Unknown |
|Threat |  |Threat  |
+---+---+  +---+----+
    |          |
    v          v
+-------+  +--------+
|Block  |  |Sandbox |  <-- Automated
|Sender |  |Analysis|
+---+---+  +---+----+
    |          |
    +----+-----+
         |
         v
+------------------+
|  Search Mailboxes|  <-- Automated
|  for Similar     |
+--------+---------+
         |
         v
+------------------+
|  Remove from     |  <-- Semi-automated (approval)
|  All Mailboxes   |
+--------+---------+
         |
         v
+------------------+
|  Notify Affected |  <-- Automated
|  Users           |
+--------+---------+
         |
         v
+------------------+
|  Update Case     |  <-- Automated
|  Close           |
+------------------+
```

#### Malware Containment Playbook

```
+------------------+
|  EDR Alert:      |
|  Malware         |
+--------+---------+
         |
         v
+------------------+
|  Validate Alert  |  <-- Automated
|  (EDR API)       |
+--------+---------+
         |
    +----+----+
    |         |
    v         v
+-------+  +--------+
|High   |  |Low     |
|Confid.|  |Confid. |
+---+---+  +---+----+
    |          |
    v          v
+-------+  +--------+
|Auto   |  |Manual  |
|Isolate|  |Review  |
+---+---+  +---+----+
    |          |
    v          |
+------------------+
|  Collect         |
|  Forensic Data   |
+--------+---------+
         |
         v
+------------------+
|  Hunt for        |
|  Lateral Movement|
+--------+---------+
         |
         v
+------------------+
|  Create Ticket   |
|  for Remediation |
+------------------+
```

### SOAR Vendor Comparison

| Vendor | Deployment | Strengths | Integration |
|--------|------------|-----------|-------------|
| **Palo Alto XSOAR** | Cloud/On-Prem | Large marketplace, XDR integration | 700+ integrations |
| **Splunk SOAR** | Cloud/On-Prem | SIEM integration, community playbooks | Extensive |
| **IBM QRadar SOAR** | Both | Case management, IBM ecosystem | Good |
| **Microsoft Sentinel** | Cloud | Native Azure, cost model | M365, Azure |
| **Swimlane** | Both | Flexibility, low-code | Growing |
| **Tines** | Cloud | No-code, modern | Growing |

### SOAR Selection Criteria

| Criterion | Weight | Considerations |
|-----------|--------|----------------|
| **Integration Breadth** | High | Number and quality of integrations |
| **Playbook Development** | High | Ease of creation, complexity support |
| **Scalability** | Medium | Alert volume handling |
| **Case Management** | Medium | Workflow, collaboration |
| **Reporting** | Medium | Metrics, compliance |
| **Support/Training** | Medium | Vendor responsiveness |
| **Cost Model** | Medium | Licensing, operational |

---

## Incident Response Automation

### Automation Tiers

| Tier | Automation Level | Human Role | Use Case |
|------|------------------|------------|----------|
| **Tier 0** | Full automation | None (notification only) | Low-risk, high-volume |
| **Tier 1** | Automated analysis | Approval/override | Medium-risk |
| **Tier 2** | Assisted investigation | Decision-making | Complex incidents |
| **Tier 3** | Manual with tools | Full control | Critical, novel |

### Automation Use Cases by Threat Type

#### Phishing (High Automation Potential)

| Step | Automation | Tool |
|------|------------|------|
| Alert ingestion | Full | SOAR |
| IOC extraction | Full | SOAR |
| Threat intel lookup | Full | TI platform |
| Mailbox search | Full | Email platform |
| User notification | Full | SOAR |
| Sender blocking | Full | Email gateway |
| Message removal | Semi (approval) | SOAR + Email |

#### Malware (High Automation Potential)

| Step | Automation | Tool |
|------|------------|------|
| Alert validation | Full | EDR/SOAR |
| Endpoint isolation | Full/Semi | EDR |
| Hash blocking | Full | EDR/NGFW |
| Forensic collection | Full | EDR |
| Lateral hunt | Semi | XDR/SIEM |
| Remediation | Manual | IT Ops |

#### Ransomware (Semi-Automation)

| Step | Automation | Tool |
|------|------------|------|
| Detection | Full | EDR/XDR |
| Isolation | Full (critical) | EDR/NAC |
| Scope assessment | Semi | XDR/SIEM |
| Backup validation | Manual | DR team |
| Negotiation | Manual | IR team/Legal |
| Recovery | Manual | IT Ops |

#### APT/Intrusion (Low Automation)

| Step | Automation | Tool |
|------|------------|------|
| Detection | Semi | XDR/NDR/Hunting |
| Investigation | Manual | Forensics |
| Scope determination | Manual | Hunting |
| Containment | Manual | Multiple |
| Eradication | Manual | Forensics |
| Recovery | Manual | IT Ops |

### Response Metrics

| Metric | Target | Automation Impact |
|--------|--------|-------------------|
| **Mean Time to Detect (MTTD)** | <1 hour | AI detection |
| **Mean Time to Respond (MTTR)** | <4 hours | SOAR automation |
| **Mean Time to Contain (MTTC)** | <1 hour | Automated isolation |
| **Alert Resolution Rate** | >95% | Automated triage |
| **Analyst Efficiency** | 10+ cases/day | Reduced manual work |

---

## Digital Forensics Capabilities

### Forensics Program Components

| Component | Description | Purpose |
|-----------|-------------|---------|
| **Endpoint Forensics** | Disk, memory, artifact collection | System investigation |
| **Network Forensics** | PCAP, flow analysis | Traffic investigation |
| **Cloud Forensics** | Cloud-native artifact collection | Cloud investigation |
| **Mobile Forensics** | Device extraction and analysis | Mobile investigation |
| **Malware Analysis** | Static and dynamic analysis | Threat understanding |

### Forensic Collection Capabilities

#### Endpoint Forensics

| Artifact | Collection Method | Tool Examples |
|----------|-------------------|---------------|
| **Disk Image** | Full/targeted imaging | FTK Imager, X-Ways |
| **Memory Dump** | Live memory capture | WinPMEM, DumpIt |
| **Registry** | Hive extraction | RegRipper |
| **Event Logs** | Log export | Velociraptor |
| **Browser Artifacts** | History, cache | Browser-specific |
| **Process List** | Live enumeration | Volatility |
| **Network Connections** | Connection state | netstat, ss |

#### Remote Forensic Collection

For distributed environments, enable remote collection:

```
+------------------+     +------------------+     +------------------+
|   Remote         | --> |   Collection     | --> |   Forensic       |
|   Endpoint       |     |   Agent          |     |   Server         |
|                  |     |   (Velociraptor/ |     |                  |
|                  |     |    GRR)          |     |                  |
+------------------+     +------------------+     +------------------+
```

### Forensic Lab Requirements

| Requirement | Description | Priority |
|-------------|-------------|----------|
| **Write Blockers** | Preserve evidence integrity | Critical |
| **Imaging Workstations** | High-speed acquisition | Critical |
| **Analysis Workstations** | High-performance analysis | Critical |
| **Malware Lab** | Isolated analysis environment | High |
| **Evidence Storage** | Secure, chain-of-custody | Critical |
| **Network Isolation** | Air-gapped analysis | High |

### Forensic Tools

| Category | Tools | Purpose |
|----------|-------|---------|
| **Disk Forensics** | EnCase, FTK, X-Ways | Image analysis |
| **Memory Forensics** | Volatility, Rekall | Memory analysis |
| **Network Forensics** | Wireshark, NetworkMiner | PCAP analysis |
| **Timeline Analysis** | Plaso, Timeline Explorer | Event correlation |
| **Malware Analysis** | Ghidra, IDA, Cuckoo | Malware understanding |
| **Mobile Forensics** | Cellebrite, Magnet | Mobile device analysis |
| **Remote Collection** | Velociraptor, GRR | Scalable collection |

### Chain of Custody

| Step | Documentation | Verification |
|------|---------------|--------------|
| **Identification** | Asset details, location | Photograph |
| **Collection** | Date, time, method | Hash values |
| **Transfer** | Handoff records | Signatures |
| **Storage** | Location, access log | Physical security |
| **Analysis** | Actions taken | Audit log |
| **Disposal** | Method, authorization | Documentation |

---

## Business Continuity Planning

### BCP Framework

| Component | Description | Owner |
|-----------|-------------|-------|
| **Business Impact Analysis (BIA)** | Critical function identification | Business units |
| **Risk Assessment** | Threat and vulnerability analysis | Security |
| **Recovery Strategies** | Approach for each function | IT/Business |
| **Plan Development** | Documented procedures | BCP team |
| **Testing** | Regular validation | BCP team |
| **Maintenance** | Continuous updates | BCP team |

### Business Impact Analysis

#### Criticality Classification

| Level | Description | RTO | RPO |
|-------|-------------|-----|-----|
| **Critical** | Core operations, revenue | <4 hours | <1 hour |
| **Essential** | Important but can delay | 4-24 hours | 4-8 hours |
| **Necessary** | Required but flexible | 1-3 days | 24 hours |
| **Desirable** | Non-critical | 3-7 days | 72 hours |

#### Singapore Regulatory Requirements

| Sector | RTO Requirement | Source |
|--------|-----------------|--------|
| **Financial (MAS)** | <4 hours for critical systems | MAS TRM Notice |
| **CII Sectors** | As defined per sector | Cybersecurity Act |
| **Healthcare** | Varies by service | Sector guidelines |

### Continuity Strategies

| Strategy | Description | Use Case |
|----------|-------------|----------|
| **Active-Active** | Multi-site, load balanced | Critical services |
| **Active-Passive** | Standby site ready | Essential services |
| **Pilot Light** | Minimal standby, scale on demand | Cost-sensitive |
| **Backup/Restore** | Restore from backup | Non-critical |

### BCP Testing

| Test Type | Frequency | Scope |
|-----------|-----------|-------|
| **Tabletop Exercise** | Quarterly | Scenario walkthrough |
| **Functional Test** | Semi-annually | Component validation |
| **Full DR Test** | Annually | Complete failover |
| **Cyber Exercise** | Annually | Cyber scenario |

---

## Disaster Recovery Strategies

### DR Architecture Options

#### Option 1: On-Premises DR

```
+------------------+     +------------------+
|   Primary DC     |     |   Secondary DC   |
|   (Production)   | <=> |   (DR Site)      |
|                  |     |                  |
|   +----------+   |     |   +----------+   |
|   | Servers  |   |     |   | Servers  |   |
|   +----------+   |     |   +----------+   |
|   +----------+   |     |   +----------+   |
|   | Storage  |   |     |   | Storage  |   |
|   +----------+   |     |   +----------+   |
+------------------+     +------------------+
        |                        |
        +----------+-------------+
                   |
          Replication Link
```

#### Option 2: Cloud-Based DR

```
+------------------+     +------------------+
|   On-Premises    |     |   Cloud DR       |
|   Primary        | --> |   (AWS/Azure/GCP)|
|                  |     |                  |
|   +----------+   |     |   +----------+   |
|   | Workloads|   |     |   | DR VMs   |   |
|   +----------+   |     |   +----------+   |
|   +----------+   |     |   +----------+   |
|   | Data     |   |     |   | Replicated|  |
|   +----------+   |     |   | Data     |   |
+------------------+     +------------------+
```

#### Option 3: Hybrid Multi-Cloud

```
+------------------+     +------------------+     +------------------+
|   Primary Cloud  |     |   Secondary Cloud|     |   Tertiary       |
|   (AWS SG)       | <=> |   (Azure SG)     | <=> |   (On-Prem)      |
+------------------+     +------------------+     +------------------+
```

### Backup Strategies

#### 3-2-1-1-0 Rule

| Component | Description |
|-----------|-------------|
| **3** | At least 3 copies of data |
| **2** | On 2 different media types |
| **1** | 1 copy offsite |
| **1** | 1 copy offline/immutable |
| **0** | 0 errors (verified backups) |

#### Backup Technologies

| Technology | Use Case | RPO Capability |
|------------|----------|----------------|
| **Snapshots** | VM/storage snapshots | Minutes |
| **Replication** | Synchronous/async | Seconds to minutes |
| **Agent-Based** | Application-aware | Hours |
| **Image-Based** | Full system backup | Hours |
| **Cloud Native** | AWS Backup, Azure Backup | Configurable |

### Ransomware-Resistant Recovery

| Control | Description | Protection |
|---------|-------------|------------|
| **Immutable Backups** | Write-once, read-many | Cannot be encrypted |
| **Air-Gapped** | Offline copies | Network isolation |
| **Backup Testing** | Regular restore tests | Verify integrity |
| **Separate Credentials** | Distinct backup accounts | Credential theft protection |
| **Encryption** | Encrypt backup data | Confidentiality |

### DR Vendor Comparison

| Vendor | Strengths | Cloud Support | Use Case |
|--------|-----------|---------------|----------|
| **Veeam** | Comprehensive, enterprise | Multi-cloud | VMware/Hyper-V |
| **Commvault** | Enterprise, data management | Multi-cloud | Large enterprise |
| **Rubrik** | Modern, ransomware focus | Cloud-native | Security-focused |
| **Cohesity** | Data management, simplicity | Multi-cloud | Consolidation |
| **Zerto** | Replication, low RPO | Multi-cloud | Critical workloads |

---

## Incident Response Program

### IR Team Structure

#### SOC Team Model

```
                    +------------------+
                    |   SOC Manager    |
                    +--------+---------+
                             |
         +-------------------+-------------------+
         |                   |                   |
+--------+--------+ +--------+--------+ +--------+--------+
|   Tier 1        | |   Tier 2        | |   Tier 3        |
|   Analysts      | |   Analysts      | |   Senior/Hunt   |
|                 | |                 | |                 |
|   - Alert       | |   - Escalation  | |   - Hunting     |
|     triage      | |   - Investigation| |   - Forensics  |
|   - Initial     | |   - Containment | |   - Malware    |
|     response    | |                 | |     analysis   |
+-----------------+ +-----------------+ +-----------------+
```

#### CSIRT Model (for Government)

| Role | Responsibility | FTE Estimate |
|------|----------------|--------------|
| **CSIRT Manager** | Overall coordination | 1 |
| **Incident Handlers** | Investigation, containment | 4-6 |
| **Forensic Analysts** | Evidence analysis | 2-3 |
| **Threat Intel Analysts** | TI analysis, hunting | 2-3 |
| **Malware Analysts** | Malware reverse engineering | 1-2 |
| **Communications** | Stakeholder communication | 1 |

### Incident Classification

#### Severity Levels

| Level | Description | Response | Notification |
|-------|-------------|----------|--------------|
| **Critical** | Business impact, data breach | Immediate | Executive, regulators |
| **High** | Significant threat, potential impact | <1 hour | Management |
| **Medium** | Confirmed threat, limited impact | <4 hours | Team lead |
| **Low** | Suspicious activity, minimal impact | <24 hours | Log only |

#### Incident Categories

| Category | Examples | Typical Severity |
|----------|----------|------------------|
| **Malware** | Ransomware, trojans | High-Critical |
| **Intrusion** | APT, unauthorized access | High-Critical |
| **Data Breach** | Data theft, exposure | Critical |
| **DDoS** | Service disruption | High |
| **Phishing** | Credential theft attempts | Medium-High |
| **Policy Violation** | Insider misuse | Medium |
| **Vulnerability** | Exploited vulnerability | High |

### Incident Response Process

#### NIST IR Lifecycle (SP 800-61r3)

```
+------------------+     +------------------+     +------------------+
|   Preparation    | --> |   Detection &    | --> |   Containment    |
|                  |     |   Analysis       |     |   Eradication    |
|   - Tools        |     |   - Alert        |     |   - Isolation    |
|   - Training     |     |   - Triage       |     |   - Remove       |
|   - Playbooks    |     |   - Investigation|     |   - Patch        |
+------------------+     +------------------+     +------------------+
                                                          |
         +------------------------------------------------+
         |
         v
+------------------+     +------------------+
|   Recovery       | --> |   Post-Incident  |
|                  |     |   Activity       |
|   - Restore      |     |   - Lessons      |
|   - Monitor      |     |   - Report       |
|   - Validate     |     |   - Improve      |
+------------------+     +------------------+
```

### Regulatory Notification Requirements

#### Singapore Requirements

| Regulation | Notification Timeline | Recipient | Trigger |
|------------|----------------------|-----------|---------|
| **Cybersecurity Act (CII)** | 2 hours (APT-related) | CSA | CII incident |
| **MAS** | 1 hour | MAS | Financial sector |
| **PDPA** | As soon as practicable | PDPC | Data breach |
| **Internal Policy** | Per classification | Management | All incidents |

#### Notification Template

| Element | Content |
|---------|---------|
| **What** | Incident description, affected systems |
| **When** | Discovery time, estimated start time |
| **Impact** | Services affected, data involved |
| **Actions** | Containment steps taken |
| **Status** | Current situation |
| **Next Steps** | Planned actions |

### Retainer Services

#### When to Engage External IR

| Trigger | Reason | Retainer Type |
|---------|--------|---------------|
| **Ransomware** | Negotiation, recovery expertise | IR retainer |
| **APT/Nation-State** | Advanced forensics | IR retainer |
| **Legal Exposure** | Evidence preservation | Legal + IR |
| **Capacity Overflow** | Internal team overwhelmed | Supplemental |
| **Specialized Skills** | Malware analysis, OT forensics | On-demand |

#### Singapore IR Service Providers

| Provider | Services | Specialization |
|----------|----------|----------------|
| **Ensign InfoSecurity** | Full IR, forensics | Local, government experience |
| **CrowdStrike Services** | IR, threat intel | Global, APT expertise |
| **Mandiant** | IR, forensics | Global, nation-state focus |
| **Kroll** | IR, legal support | Investigation, litigation |
| **PwC** | IR, advisory | Regulatory, governance |

---

## Vendor Landscape

### Comprehensive Response/Recovery Vendor Matrix

| Category | Leaders | Challengers | Singapore Focus |
|----------|---------|-------------|-----------------|
| **SOAR** | Palo Alto XSOAR, Splunk | Microsoft, IBM | All present |
| **Forensics** | EnCase, FTK, Cellebrite | X-Ways, Magnet | All present |
| **Backup/DR** | Veeam, Commvault | Rubrik, Cohesity | All present |
| **IR Services** | CrowdStrike, Mandiant | Ensign, Kroll | All present |
| **BCP Software** | Fusion Risk, Archer | ServiceNow | All present |

### Singapore-Based Providers

| Provider | Response/Recovery Services |
|----------|---------------------------|
| **Ensign InfoSecurity** | IR retainer, forensics, SOC |
| **Singtel Trustwave** | IR services, managed SOC |
| **Deloitte** | IR, forensics, advisory |
| **PwC** | IR, cyber advisory |
| **KPMG** | IR, forensics |

---

## Implementation Roadmap

### Phase 1: Foundation (Months 1-3)

| Activity | Deliverable | Priority |
|----------|-------------|----------|
| IR plan development | Documented IR plan | Critical |
| SOAR evaluation | Vendor shortlist | High |
| Forensic capability assessment | Gap analysis | High |
| BCP/DR review | Current state assessment | High |

### Phase 2: Core Deployment (Months 4-9)

| Activity | Deliverable | Priority |
|----------|-------------|----------|
| SOAR deployment | Operational platform | Critical |
| Playbook development | Top 10 playbooks | Critical |
| Forensic tools deployment | Lab capability | High |
| Backup modernization | Immutable backups | High |
| IR retainer engagement | Contract in place | Medium |

### Phase 3: Enhancement (Months 10-18)

| Activity | Deliverable | Priority |
|----------|-------------|----------|
| Automation expansion | 50+ playbooks | High |
| DR testing program | Regular DR tests | High |
| Tabletop exercises | Quarterly exercises | High |
| Threat hunting integration | Hunt-to-response | Medium |
| Metrics program | KPI dashboard | Medium |

### Phase 4: Maturity (Ongoing)

| Activity | Deliverable | Frequency |
|----------|-------------|-----------|
| Playbook updates | Current playbooks | Continuous |
| DR/BCP testing | Validated plans | Per schedule |
| Lessons learned | Improvement actions | Post-incident |
| Training | Skilled team | Continuous |
| Vendor review | Optimized tools | Annually |

---

## Success Metrics

### Response KPIs

| Metric | Target | Measurement |
|--------|--------|-------------|
| **Mean Time to Detect (MTTD)** | <1 hour | SIEM/XDR |
| **Mean Time to Respond (MTTR)** | <4 hours | SOAR |
| **Mean Time to Contain (MTTC)** | <1 hour | SOAR |
| **Mean Time to Recover (MTTRec)** | <RTO | DR metrics |
| **Playbook Coverage** | >80% common incidents | SOAR inventory |
| **Automation Rate** | >50% alerts auto-resolved | SOAR metrics |

### Recovery KPIs

| Metric | Target | Measurement |
|--------|--------|-------------|
| **RTO Achievement** | 100% within RTO | DR tests |
| **RPO Achievement** | 100% within RPO | Backup metrics |
| **Backup Success Rate** | >99% | Backup system |
| **DR Test Success** | 100% pass | Test results |
| **BCP Plan Currency** | 100% current | Plan reviews |

---

## References

- [NIST SP 800-61r3](https://csrc.nist.gov/publications/detail/sp/800-61/rev-3/final) - Incident Response Recommendations (2025)
- [CSA Singapore Cyber Landscape 2024/2025](https://www.csa.gov.sg/resources/publications/singapore-cyber-landscape-2024-2025/)
- [MAS TRM Guidelines](https://www.mas.gov.sg/regulation/guidelines/technology-risk-management-guidelines) - Recovery requirements
- [Cybersecurity Act](https://www.csa.gov.sg/legislation/cybersecurity-act/) - Notification requirements
- [ISO 22301:2019](https://www.iso.org/standard/75106.html) - Business Continuity Management

---

*For detection capabilities, see [01-detection-monitoring.md](./01-detection-monitoring.md)*
*For prevention capabilities, see [02-prevention-protection.md](./02-prevention-protection.md)*
