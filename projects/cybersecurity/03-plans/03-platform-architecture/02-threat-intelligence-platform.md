# Threat Intelligence Platform Design

> Comprehensive threat intelligence platform architecture for proactive government cybersecurity defense.
>
> Last Updated: January 2026

## Table of Contents

1. [Executive Summary](#executive-summary)
2. [TI Platform Architecture](#ti-platform-architecture)
3. [Intelligence Sources and Feeds](#intelligence-sources-and-feeds)
4. [IOC Management](#ioc-management)
5. [Threat Hunting Capabilities](#threat-hunting-capabilities)
6. [Intelligence Sharing (STIX/TAXII)](#intelligence-sharing-stixtaxii)
7. [Integration with Defensive Tools](#integration-with-defensive-tools)
8. [Implementation Considerations](#implementation-considerations)

---

## Executive Summary

### Purpose

This document provides a detailed architectural design for a Threat Intelligence Platform (TIP) suitable for government cybersecurity operations. The platform enables proactive threat detection, informed decision-making, and effective defense against sophisticated adversaries, including the Advanced Persistent Threats (APTs) increasingly targeting Singapore's Critical Information Infrastructure.

### Key Design Objectives

| Objective | Description |
|-----------|-------------|
| **Proactive Defense** | Enable anticipatory rather than reactive security |
| **Contextualized Intelligence** | Deliver actionable, relevant intelligence |
| **APT Tracking** | Monitor nation-state and sophisticated threat actors |
| **Automated Dissemination** | Push intelligence to defensive tools automatically |
| **Regional Collaboration** | Support ASEAN and international intelligence sharing |

### Threat Landscape Context

Based on research findings:

| Metric | Value | Implication |
|--------|-------|-------------|
| APT attacks on Singapore | 4x increase (2021-2024) | Enhanced tracking required |
| AI-generated phishing | 82.6% of all phishing | Detection signatures evolving rapidly |
| Dwell time (industry avg) | 277 days | Need proactive hunting |
| Key threat actors | UNC3886, state-sponsored APTs | Require specific tracking |

---

## TI Platform Architecture

### Functional Architecture

```
+------------------------------------------------------------------+
|                        DISSEMINATION LAYER                        |
|  Reports | Alerts | API | Briefings | Dashboards | STIX/TAXII    |
+------------------------------------------------------------------+
                                |
+------------------------------------------------------------------+
|                         ANALYSIS LAYER                            |
|  Correlation | Attribution | Trending | Prediction | Reporting   |
+------------------------------------------------------------------+
                                |
+------------------------------------------------------------------+
|                        PROCESSING LAYER                           |
|  Normalization | Enrichment | Deduplication | Scoring | Tagging  |
+------------------------------------------------------------------+
                                |
+------------------------------------------------------------------+
|                        COLLECTION LAYER                           |
|  Feeds | OSINT | Dark Web | Internal | Partners | Research       |
+------------------------------------------------------------------+
```

### Intelligence Lifecycle

```
         +-------------+
         | Requirements|  <-- Strategic priorities
         +------+------+
                |
                v
         +------+------+
         | Collection  |  <-- Multi-source gathering
         +------+------+
                |
                v
         +------+------+
         | Processing  |  <-- Normalization, enrichment
         +------+------+
                |
                v
         +------+------+
         |  Analysis   |  <-- Context, attribution
         +------+------+
                |
                v
         +------+------+
         |Dissemination|  <-- Stakeholder delivery
         +------+------+
                |
                v
         +------+------+
         |  Feedback   |  <-- Improvement loop
         +------+------+
```

### Platform Components

#### 1. Threat Intelligence Platform (TIP)

**Primary Function**: Central hub for intelligence aggregation, analysis, and distribution

| Component | Recommended Options | Considerations |
|-----------|---------------------|----------------|
| **Commercial TIP** | Anomali ThreatStream, Recorded Future, MISP | Features, cost, integration |
| **Open Source TIP** | MISP, OpenCTI, TheHive | Flexibility, community support |
| **Hybrid Approach** | MISP + Commercial enrichment | Best of both worlds |

**Key Requirements**:
- STIX 2.1 native support
- TAXII 2.x server capabilities
- MITRE ATT&CK mapping
- Multi-tenancy for sector separation
- API-first architecture

#### 2. Intelligence Analysis Workbench

**Primary Function**: Analyst workspace for investigation and analysis

| Component | Purpose |
|-----------|---------|
| **Maltego** | Link analysis, visualization |
| **Analyst1** | Structured intelligence analysis |
| **Palantir** | Large-scale data analysis (if available) |
| **Custom Notebooks** | Jupyter-based analysis workflows |

#### 3. IOC Management System

**Primary Function**: Indicator lifecycle management

| Component | Purpose |
|-----------|---------|
| **IOC Database** | Central repository with versioning |
| **Enrichment Engine** | Automated context addition |
| **Scoring System** | Confidence and severity ratings |
| **Expiration Manager** | Lifecycle and deprecation |

#### 4. Dark Web Monitoring

**Primary Function**: Underground intelligence collection

| Component | Recommended Options |
|-----------|---------------------|
| **Dark Web Monitoring** | Recorded Future, Flashpoint, DarkOwl |
| **Credential Monitoring** | SpyCloud, Have I Been Pwned integration |
| **Paste Site Monitoring** | Automated paste site collection |

### Architecture Diagram

```
+------------------+     +------------------+     +------------------+
|  External Feeds  |     |   Internal       |     |    Partners      |
|                  |     |   Sources        |     |                  |
|  - Commercial    |     |  - SIEM          |     |  - SingCERT      |
|  - OSINT         |     |  - EDR           |     |  - ASEAN CERTs   |
|  - Dark Web      |     |  - Incident Data |     |  - Sector ISACs  |
+--------+---------+     +--------+---------+     +--------+---------+
         |                        |                        |
         v                        v                        v
+------------------------------------------------------------------+
|                    Collection & Ingestion                         |
|          (STIX/TAXII, API, File Import, Manual Entry)            |
+------------------------------------------------------------------+
                                |
                                v
+------------------------------------------------------------------+
|                 Threat Intelligence Platform (TIP)                |
|                                                                   |
|  +------------+  +------------+  +------------+  +------------+  |
|  |    IOC     |  | Analysis   |  |   ATT&CK   |  |   Actor    |  |
|  | Management |  | Workbench  |  |  Mapping   |  |  Tracking  |  |
|  +------------+  +------------+  +------------+  +------------+  |
|                                                                   |
+------------------------------------------------------------------+
                                |
                                v
+------------------------------------------------------------------+
|                        Dissemination                              |
|                                                                   |
|  +----------+  +----------+  +----------+  +----------+          |
|  |   SIEM   |  | Firewall |  |   EDR    |  |  Reports |          |
|  +----------+  +----------+  +----------+  +----------+          |
+------------------------------------------------------------------+
```

---

## Intelligence Sources and Feeds

### Source Categories

#### 1. Commercial Threat Intelligence Feeds

| Provider | Strengths | Use Case |
|----------|-----------|----------|
| **Recorded Future** | Comprehensive coverage, AI-powered | Primary feed, analyst research |
| **Mandiant/Google** | APT tracking, attribution | Nation-state threat intelligence |
| **CrowdStrike** | Actor profiles, adversary intel | Tactical and strategic intelligence |
| **Anomali** | Feed aggregation, TIP integration | Feed management |
| **VirusTotal** | File/URL reputation | IOC enrichment |

#### 2. Government and Partner Sources

| Source | Content | Access Method |
|--------|---------|---------------|
| **SingCERT** | Singapore-specific threats, alerts | Secure portal, STIX/TAXII |
| **CISA** | US government advisories, IOCs | Public feeds, STIX/TAXII |
| **ACSC** | Australia cybersecurity advisories | Partnership sharing |
| **ASEAN CERTs** | Regional threat intelligence | Bilateral sharing |
| **Sector ISACs** | Industry-specific intelligence | Membership participation |

#### 3. Open Source Intelligence (OSINT)

| Source Type | Examples | Collection Method |
|-------------|----------|-------------------|
| **Threat Reports** | Vendor blogs, research papers | RSS, API, manual |
| **Malware Repositories** | MalwareBazaar, ANY.RUN | API integration |
| **IOC Feeds** | AlienVault OTX, Abuse.ch | STIX/TAXII |
| **Social Media** | Twitter/X security community | API, monitoring tools |
| **Technical Sources** | GitHub, Pastebin | Automated collection |

#### 4. Dark Web Sources

| Source Type | Purpose | Collection Considerations |
|-------------|---------|---------------------------|
| **Forums** | Actor chatter, sale announcements | Legal, operational security |
| **Marketplaces** | Credential sales, tool sales | Partnership with specialists |
| **Paste Sites** | Data leaks, IOC discovery | Automated monitoring |
| **Telegram Channels** | Threat actor communication | Real-time monitoring |

#### 5. Internal Sources

| Source | Intelligence Type |
|--------|------------------|
| **SIEM** | Detected threats, anomalies |
| **EDR** | Endpoint-based indicators |
| **Incidents** | Lessons learned, internal IOCs |
| **Honeypots** | Attacker TTPs, new techniques |
| **Threat Hunting** | Discovered threats |

### Feed Management

#### Feed Scoring Framework

| Criterion | Weight | Scoring Factors |
|-----------|--------|-----------------|
| **Relevance** | 30% | Geographic, sector, technology fit |
| **Timeliness** | 25% | Freshness, update frequency |
| **Accuracy** | 25% | Historical false positive rate |
| **Actionability** | 20% | Enrichment, context provided |

#### Feed Lifecycle

```
[Evaluation] --> [Trial (30 days)] --> [Production] --> [Quarterly Review]
                        |                    |                  |
                        v                    v                  v
                 [Reject/Adjust]      [Monitor Quality]  [Renew/Terminate]
```

### Source Prioritization for Singapore Context

| Priority | Source Type | Rationale |
|----------|-------------|-----------|
| 1 | SingCERT, CSA advisories | Singapore-specific, regulatory |
| 2 | APT-focused commercial feeds | Nation-state threat focus |
| 3 | Regional partner sharing | ASEAN threat landscape |
| 4 | Industry ISACs | Sector-specific threats |
| 5 | OSINT and dark web | Emerging threats, research |

---

## IOC Management

### IOC Types and Handling

| IOC Type | Examples | Shelf Life | Handling Priority |
|----------|----------|------------|-------------------|
| **IP Addresses** | C2 servers, scanning hosts | 7-30 days | High |
| **Domains** | Malicious domains, DGA | 30-90 days | High |
| **URLs** | Phishing pages, malware delivery | 7-14 days | High |
| **File Hashes** | Malware samples | 6-12 months | Medium |
| **Email Indicators** | Sender addresses, subjects | 14-30 days | Medium |
| **SSL Certificates** | Malicious cert fingerprints | 30-90 days | Medium |
| **Behavioral** | TTPs, patterns | Persistent | Strategic |

### IOC Lifecycle Management

```
+----------+     +----------+     +----------+     +----------+     +----------+
| Ingest   |---->| Validate |---->| Enrich   |---->| Activate |---->| Retire   |
+----------+     +----------+     +----------+     +----------+     +----------+
     |                |                |                |                |
     v                v                v                v                v
  Sources         Quality           Context          Deploy to       Scheduled
  & Feeds         Checks          Addition           Defenses        Expiration
```

#### Stage 1: Ingestion

| Activity | Process |
|----------|---------|
| Collection | Pull from feeds, manual submission |
| Parsing | Extract indicators from reports |
| Deduplication | Identify existing matches |
| Normalization | Standardize format (STIX 2.1) |

#### Stage 2: Validation

| Check Type | Description |
|------------|-------------|
| Format validation | Syntactic correctness |
| Whitelist check | Known good (CDNs, cloud providers) |
| Reputation check | Cross-reference with reputation services |
| Source validation | Trust level of source |

#### Stage 3: Enrichment

| Enrichment Type | Data Added | Sources |
|-----------------|------------|---------|
| **Geolocation** | Country, ASN, hosting | MaxMind, IP registries |
| **WHOIS** | Registration details | Domain registries |
| **Historical** | First seen, last seen | Internal tracking |
| **Related IOCs** | Associated indicators | Correlation |
| **ATT&CK Mapping** | Techniques, tactics | MITRE mapping |
| **Actor Attribution** | Threat actor linkage | Intel analysis |

#### Stage 4: Scoring

**Confidence Score** (0-100):

| Factor | Weight | Considerations |
|--------|--------|----------------|
| Source reliability | 30% | Track record, vetting |
| Corroboration | 25% | Multiple source confirmation |
| Freshness | 20% | Age of indicator |
| Specificity | 15% | Uniqueness of indicator |
| Context | 10% | Supporting information |

**Severity Score** (Critical, High, Medium, Low):

| Factor | Considerations |
|--------|----------------|
| Threat actor | APT vs. commodity threat |
| Campaign activity | Active vs. historical |
| Target relevance | Singapore-specific vs. generic |
| Impact potential | Based on associated malware/TTPs |

#### Stage 5: Activation

| Confidence Level | Automation Approach |
|------------------|---------------------|
| > 80% | Auto-deploy to blocking |
| 60-80% | Auto-deploy to detection, manual blocking |
| 40-60% | Detection only, analyst review |
| < 40% | Research/watch list only |

#### Stage 6: Retirement

| Condition | Action |
|-----------|--------|
| Time-based expiration | Automatic deactivation |
| False positive confirmed | Immediate removal + whitelist |
| Source retraction | Review and adjust |
| No activity | Move to historical archive |

### IOC Database Schema (Conceptual)

```
IOC
├── id (UUID)
├── type (ip, domain, hash, url, email)
├── value (the indicator itself)
├── confidence_score (0-100)
├── severity (critical, high, medium, low)
├── first_seen (timestamp)
├── last_seen (timestamp)
├── expiration (timestamp)
├── status (active, retired, false_positive)
├── source_id (reference to source)
├── tags (array)
├── mitre_techniques (array)
├── related_actors (array)
├── related_campaigns (array)
├── enrichments (JSON)
└── audit_log (changes history)
```

---

## Threat Hunting Capabilities

### Threat Hunting Framework

#### Hunting Maturity Model

| Level | Description | Capabilities |
|-------|-------------|--------------|
| **HM0** | Initial | Ad-hoc, reactive only |
| **HM1** | Minimal | Basic IOC searching |
| **HM2** | Procedural | Documented hunts, some automation |
| **HM3** | Innovative | Hypothesis-driven, TTP-based |
| **HM4** | Leading | Predictive, automated discovery |

**Target**: HM3 within 12 months, HM4 within 24 months

#### Hunting Types

| Type | Description | Trigger |
|------|-------------|---------|
| **Intelligence-Driven** | Based on threat intelligence | New threat reports, IOCs |
| **Hypothesis-Driven** | Based on assumptions | Analyst intuition, risk assessment |
| **Anomaly-Based** | Based on deviations | UEBA alerts, statistical analysis |
| **ATT&CK-Based** | Based on technique coverage | Coverage gaps, adversary techniques |

### Hunt Methodology

#### Hunt Development Process

```
[Intel Requirement] --> [Hypothesis] --> [Data Sources] --> [Query Design]
                                                                  |
                                                                  v
[Hunt Improvement] <-- [Documentation] <-- [Analysis] <-- [Execution]
```

#### Hypothesis Template

```markdown
## Hunt Hypothesis: [Name]

### Background
- Intel source: [Reference to intelligence]
- Threat actor: [If known]
- ATT&CK technique: [T#### - Name]

### Hypothesis Statement
"Adversary may be [doing X] in our environment because [evidence/reasoning]"

### Data Sources Required
- [ ] Endpoint telemetry (EDR)
- [ ] Network logs (firewall, proxy)
- [ ] Authentication logs (AD, SSO)
- [ ] Other: [specify]

### Detection Logic
[Query or rule logic]

### Success Criteria
- True positive: [What constitutes finding]
- Tuning required: [Adjustment criteria]

### Hunt Results
[To be completed]
```

### ATT&CK-Based Hunting

#### Priority Techniques for Singapore Context

Based on threat landscape research:

| Technique ID | Name | Priority | Rationale |
|--------------|------|----------|-----------|
| T1566 | Phishing | Critical | 82.6% AI-generated phishing |
| T1059 | Command and Scripting | Critical | PowerShell, Python abuse |
| T1078 | Valid Accounts | Critical | Credential-based attacks |
| T1071 | Application Layer Protocol | High | C2 communication |
| T1486 | Data Encrypted for Impact | High | Ransomware threat |
| T1003 | OS Credential Dumping | High | Lateral movement |
| T1021 | Remote Services | High | Lateral movement |
| T1053 | Scheduled Task/Job | Medium | Persistence |
| T1105 | Ingress Tool Transfer | Medium | Malware delivery |
| T1490 | Inhibit System Recovery | Medium | Ransomware |

#### Hunt Coverage Dashboard

Track hunting coverage against ATT&CK matrix:

| Tactic | Techniques Covered | Hunts Executed (Quarterly) |
|--------|-------------------|---------------------------|
| Initial Access | 8/11 (73%) | 12 |
| Execution | 10/13 (77%) | 15 |
| Persistence | 12/19 (63%) | 10 |
| Privilege Escalation | 8/13 (62%) | 8 |
| Defense Evasion | 15/42 (36%) | 12 |
| Credential Access | 9/17 (53%) | 14 |
| Discovery | 12/31 (39%) | 8 |
| Lateral Movement | 7/9 (78%) | 10 |
| Collection | 5/17 (29%) | 6 |
| Exfiltration | 4/9 (44%) | 5 |
| Command and Control | 8/16 (50%) | 8 |
| Impact | 6/14 (43%) | 7 |

### Hunt Automation

#### Automated Hunt Queries

| Hunt Type | Automation Level | Frequency |
|-----------|-----------------|-----------|
| IOC sweeps | Fully automated | Continuous |
| Behavioral patterns | Semi-automated | Daily |
| ATT&CK technique hunts | Scheduled queries | Weekly |
| Hypothesis-driven | Analyst-initiated | As needed |

#### Hunt-to-Detection Pipeline

```
[Successful Hunt] --> [Finding Validation] --> [Rule Development]
                                                       |
                                                       v
                             [Detection Tuning] <-- [Production Deployment]
```

---

## Intelligence Sharing (STIX/TAXII)

### STIX 2.1 Implementation

#### STIX Domain Objects (SDOs) Used

| Object Type | Usage | Example |
|-------------|-------|---------|
| **Attack Pattern** | TTPs | PowerShell execution technique |
| **Campaign** | Coordinated attacks | APT operation tracking |
| **Indicator** | Observable patterns | IOCs with context |
| **Intrusion Set** | Threat actor activity | APT group operations |
| **Malware** | Malicious code | Specific malware families |
| **Threat Actor** | Adversary profiles | Nation-state actors |
| **Tool** | Legitimate tools abused | Cobalt Strike, Mimikatz |
| **Vulnerability** | Exploited CVEs | Zero-days, n-days |

#### STIX Cyber Observable Objects (SCOs)

| Object Type | Usage |
|-------------|-------|
| **IPv4/IPv6 Address** | Network indicators |
| **Domain Name** | Domain indicators |
| **URL** | Web indicators |
| **File** | File hash indicators |
| **Email Message** | Phishing indicators |
| **Windows Registry Key** | Persistence indicators |

#### STIX Relationship Types

| Relationship | Example |
|--------------|---------|
| indicates | Indicator -> Malware |
| uses | Threat Actor -> Attack Pattern |
| attributed-to | Campaign -> Intrusion Set |
| targets | Campaign -> Identity (Sector) |
| related-to | Malware -> Tool |

### TAXII 2.x Server Configuration

#### Collection Structure

```
TAXII Server
├── API Root: /taxii2/
│   ├── Collection: government-intel
│   │   └── Scope: Government-specific intelligence
│   ├── Collection: cii-sectors
│   │   └── Scope: CII sector intelligence (restricted)
│   ├── Collection: singapore-threats
│   │   └── Scope: Singapore-targeted threats
│   ├── Collection: regional-asean
│   │   └── Scope: ASEAN regional sharing
│   └── Collection: general-intel
│       └── Scope: General threat intelligence
```

#### Access Control

| Collection | Access Level | Subscribers |
|------------|--------------|-------------|
| government-intel | Restricted | Government agencies only |
| cii-sectors | Restricted | CII owners, sector regulators |
| singapore-threats | Partners | Trusted partners, MNCs |
| regional-asean | Bilateral | ASEAN CERT partners |
| general-intel | Public | Authenticated subscribers |

### Sharing Relationships

#### Inbound Sharing

| Partner | Content | Mechanism | Frequency |
|---------|---------|-----------|-----------|
| SingCERT | Singapore advisories | TAXII pull | Real-time |
| CISA | US advisories, IOCs | TAXII pull | Real-time |
| Commercial feeds | Various | API, TAXII | Real-time |
| Sector ISACs | Industry intel | TAXII, portal | Daily |
| Research community | OSINT | Various | Continuous |

#### Outbound Sharing

| Partner | Content Shared | Mechanism | Approval |
|---------|---------------|-----------|----------|
| SingCERT | Incidents, IOCs | TAXII push | Auto (sanitized) |
| ASEAN CERTs | Regional threats | TAXII | Manual review |
| Sector CIIs | Sector-specific | TAXII | Auto (filtered) |
| Research partners | Anonymized data | API | Manual review |

### Traffic Light Protocol (TLP)

| TLP Level | Sharing Rules | Use Case |
|-----------|---------------|----------|
| **TLP:RED** | Named recipients only | Sensitive incidents |
| **TLP:AMBER** | Organization + need-to-know | Operational intelligence |
| **TLP:AMBER+STRICT** | Organization only | Internal sharing |
| **TLP:GREEN** | Community sharing | General advisories |
| **TLP:CLEAR** | Public | Published reports |

### Sharing Architecture

```
+------------------+                          +------------------+
|  External TAXII  |      STIX 2.1           |  Internal TIP    |
|     Servers      |<----------------------->|                  |
|                  |                          |  TAXII Server    |
+------------------+                          +--------+---------+
                                                       |
                    +----------------------------------+----------------------------------+
                    |                                  |                                  |
                    v                                  v                                  v
           +----------------+               +------------------+               +------------------+
           | Government     |               | CII Sector       |               | Partner          |
           | Agencies       |               | Organizations    |               | Organizations    |
           +----------------+               +------------------+               +------------------+
```

---

## Integration with Defensive Tools

### Integration Points

#### SIEM Integration

| Integration Type | Implementation | Benefit |
|------------------|----------------|---------|
| **IOC Ingestion** | TAXII feed into SIEM | Automated detection |
| **Alert Enrichment** | TIP API lookup | Context in alerts |
| **Threat Context** | Dashboard widgets | Analyst visibility |
| **Correlation Rules** | TIP-informed rules | Better detection |

**Example Flow**:
```
TIP --> [TAXII/API] --> SIEM --> [Correlation] --> Alert (Enriched)
```

#### EDR Integration

| Integration Type | Implementation | Benefit |
|------------------|----------------|---------|
| **Block Lists** | Push file hashes | Automated blocking |
| **Detection Rules** | YARA rules | Behavioral detection |
| **Hunt Queries** | Pre-built searches | Rapid hunting |
| **Response Actions** | TIP-triggered isolation | Automated response |

#### Firewall/Proxy Integration

| Integration Type | Implementation | Benefit |
|------------------|----------------|---------|
| **Domain Blocklists** | API push to firewall | Perimeter blocking |
| **IP Blocklists** | Feed integration | Network blocking |
| **URL Categories** | Threat URL feeds | Web filtering |
| **SSL Inspection** | Certificate IOCs | Encrypted traffic |

#### Email Security Integration

| Integration Type | Implementation | Benefit |
|------------------|----------------|---------|
| **Sender Blocklists** | Email gateway integration | Phishing blocking |
| **URL Rewriting** | Malicious URL blocking | Link protection |
| **Attachment Analysis** | Hash-based blocking | Malware prevention |
| **Header Analysis** | Spoofing detection | Fraud prevention |

### Automated Response Workflows

#### Workflow 1: IOC-Triggered Blocking

```
[New High-Confidence IOC]
           |
           v
[Validate: Not in Whitelist]
           |
           v
[Enrich: Add Context]
           |
           v
[Deploy to Controls]
     |         |         |
     v         v         v
[Firewall] [EDR]    [Proxy]
     |         |         |
     v         v         v
[Log Deployment Actions]
           |
           v
[Monitor for Hits]
```

#### Workflow 2: Alert Enrichment

```
[SIEM Alert Generated]
           |
           v
[Extract Observables]
     - IPs, domains, hashes
           |
           v
[Query TIP via API]
           |
           v
[Return Enrichment]
     - Threat actor
     - Campaign
     - Related IOCs
     - Recommended actions
           |
           v
[Enhanced Alert to Analyst]
```

#### Workflow 3: Threat Hunt Deployment

```
[New Threat Report Published]
           |
           v
[Extract TTPs and IOCs]
           |
           v
[Generate Hunt Queries]
           |
           v
[Deploy to Hunt Platform]
     |              |
     v              v
[SIEM Queries] [EDR Queries]
     |              |
     v              v
[Collect Results]
           |
           v
[Analyst Review]
```

### Integration API Specifications

#### TIP API Capabilities

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/indicators` | GET, POST | IOC retrieval and submission |
| `/enrichment` | GET | Context lookup for observables |
| `/actors` | GET | Threat actor information |
| `/campaigns` | GET | Campaign details |
| `/reports` | GET | Intelligence reports |
| `/hunt-queries` | GET | Pre-built hunt queries |

#### Sample API Response (Enrichment)

```json
{
  "observable": "192.168.1.100",
  "type": "ipv4-addr",
  "enrichment": {
    "reputation": "malicious",
    "confidence": 85,
    "first_seen": "2025-12-01T00:00:00Z",
    "last_seen": "2026-01-15T00:00:00Z",
    "related_actors": ["UNC3886"],
    "campaigns": ["campaign-001"],
    "mitre_techniques": ["T1071", "T1105"],
    "tags": ["apt", "c2", "singapore-targeted"],
    "recommended_action": "block"
  }
}
```

---

## Implementation Considerations

### Deployment Phases

#### Phase 1: Foundation (Months 1-4)

| Activity | Duration | Deliverables |
|----------|----------|--------------|
| TIP deployment | 6 weeks | Core platform operational |
| Feed integration | 4 weeks | 5+ feeds integrated |
| Basic SIEM integration | 4 weeks | IOC detection enabled |
| Analyst training | 2 weeks | Team operational |

#### Phase 2: Expansion (Months 5-8)

| Activity | Duration | Deliverables |
|----------|----------|--------------|
| Additional feeds | 4 weeks | 10+ feeds integrated |
| STIX/TAXII server | 6 weeks | Sharing infrastructure |
| Full tool integration | 6 weeks | EDR, firewall, proxy connected |
| Hunt program launch | Ongoing | Regular hunts executed |

#### Phase 3: Optimization (Months 9-12)

| Activity | Duration | Deliverables |
|----------|----------|--------------|
| Automation workflows | 8 weeks | 80% auto-dissemination |
| Partner sharing | Ongoing | Active sharing relationships |
| Advanced analytics | 6 weeks | Predictive capabilities |
| Continuous improvement | Ongoing | Metrics-driven optimization |

### Staffing Requirements

| Role | FTE | Responsibilities |
|------|-----|------------------|
| TI Manager | 1 | Strategy, relationships, oversight |
| Senior TI Analyst | 2 | APT tracking, attribution, reports |
| TI Analyst | 2 | Daily analysis, IOC management |
| TI Engineer | 1 | Platform maintenance, integrations |
| **Total** | **6** | |

### Success Metrics

| Metric | Target | Measurement |
|--------|--------|-------------|
| IOC coverage | > 90% of relevant threats | Monthly review |
| Time to disseminate | < 1 hour for critical | Automated tracking |
| False positive rate | < 5% | Feedback analysis |
| Hunt success rate | > 20% yield findings | Quarterly |
| Partner sharing | Active in 5+ relationships | Annual review |

### Budget Considerations

| Category | Estimate | Notes |
|----------|----------|-------|
| TIP platform | S$200K-500K/year | Commercial vs. open source |
| Commercial feeds | S$100K-300K/year | Depends on coverage needs |
| Dark web monitoring | S$50K-150K/year | Specialized capability |
| Infrastructure | S$50K-100K/year | Servers, storage, network |
| Training | S$30K-50K/year | Certifications, courses |
| **Total** | **S$430K-1.1M/year** | Scale dependent |

---

## Related Documents

- [01-soc-platform.md](./01-soc-platform.md) - SOC integration
- [03-incident-response-platform.md](./03-incident-response-platform.md) - IR integration
- [04-security-automation.md](./04-security-automation.md) - Automation details
- [05-implementation-roadmap.md](./05-implementation-roadmap.md) - Overall roadmap

---

## References

- [MITRE ATT&CK](https://attack.mitre.org/) - Technique framework
- [STIX 2.1 Specification](https://oasis-open.github.io/cti-documentation/stix/intro) - Data format
- [TAXII 2.x Specification](https://oasis-open.github.io/cti-documentation/taxii/intro) - Sharing protocol
- [MISP Project](https://www.misp-project.org/) - Open source TIP
- [OpenCTI](https://www.opencti.io/) - Open source CTI platform

---

*Last Updated: January 2026*
