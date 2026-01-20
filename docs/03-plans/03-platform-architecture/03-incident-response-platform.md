# Incident Response Platform Design

> Comprehensive incident response platform architecture for structured government cybersecurity incident management.
>
> Last Updated: January 2026

## Table of Contents

1. [Executive Summary](#executive-summary)
2. [IR Platform Architecture](#ir-platform-architecture)
3. [Case Management](#case-management)
4. [Forensics Integration](#forensics-integration)
5. [Communication Workflows](#communication-workflows)
6. [Playbook Management](#playbook-management)
7. [Post-Incident Analysis](#post-incident-analysis)
8. [Implementation Considerations](#implementation-considerations)

---

## Executive Summary

### Purpose

This document provides a detailed architectural design for an Incident Response (IR) Platform suitable for government cybersecurity operations. The platform enables structured, efficient, and compliant handling of security incidents from detection through resolution and lessons learned, with particular emphasis on meeting Singapore's regulatory reporting requirements.

### Key Design Objectives

| Objective | Description |
|-----------|-------------|
| **Structured Response** | Consistent, documented incident handling |
| **Regulatory Compliance** | Meet 2-hour CII reporting requirements |
| **Evidence Preservation** | Forensically sound evidence management |
| **Efficient Coordination** | Streamlined communication and escalation |
| **Continuous Improvement** | Learning from incidents to improve posture |

### Regulatory Context

| Requirement | Source | Implication |
|-------------|--------|-------------|
| 2-hour incident notification | Cybersecurity Act (2024) | Automated alerting required |
| 14-day root cause analysis | Cybersecurity Act (2024) | Structured investigation process |
| APT reporting | Cybersecurity Act (2024) | Enhanced tracking capabilities |
| Evidence retention | Legal/Compliance | 7-year minimum for critical |
| Chain of custody | Legal/Forensic | Documented evidence handling |

---

## IR Platform Architecture

### Functional Architecture

```
+------------------------------------------------------------------+
|                        REPORTING LAYER                            |
|  Executive Reports | Regulatory Submissions | Metrics | Dashboards|
+------------------------------------------------------------------+
                                |
+------------------------------------------------------------------+
|                       COORDINATION LAYER                          |
|  Communication | Escalation | Stakeholder Management | War Room  |
+------------------------------------------------------------------+
                                |
+------------------------------------------------------------------+
|                       INVESTIGATION LAYER                         |
|  Timeline Analysis | Forensics | Threat Intel | Root Cause       |
+------------------------------------------------------------------+
                                |
+------------------------------------------------------------------+
|                       CASE MANAGEMENT LAYER                       |
|  Incident Tracking | Evidence Mgmt | Playbook Execution | Tasks  |
+------------------------------------------------------------------+
                                |
+------------------------------------------------------------------+
|                        INTEGRATION LAYER                          |
|  SOC Platform | TIP | Forensic Tools | Communication Systems     |
+------------------------------------------------------------------+
```

### Incident Response Lifecycle

```
         +-------------+
         | Preparation |  <-- Plans, training, tools
         +------+------+
                |
                v
+------+--------+--------+------+
|      | Detection &     |      |
|      | Analysis        |      |
|      +--------+--------+      |
|               |               |
|               v               |
|      +--------+--------+      |
|      | Containment     |      |
|      +--------+--------+      |
|               |               |
|               v               |
|      +--------+--------+      |
|      | Eradication     |      |
|      +--------+--------+      |
|               |               |
|               v               |
|      +--------+--------+      |
|      | Recovery        |      |
|      +--------+--------+      |
+------+--------+--------+------+
                |
                v
         +------+------+
         | Post-Incident|  <-- Lessons learned
         | Activity     |
         +-------------+
```

### Platform Components

#### 1. Incident Case Management System

**Primary Function**: Central tracking and coordination of incidents

| Component | Recommended Options | Considerations |
|-----------|---------------------|----------------|
| **Enterprise ITSM** | ServiceNow SecOps, Jira Service Management | Workflow, reporting |
| **Dedicated IR Platform** | TheHive, DFIR IRIS, Swimlane | IR-specific features |
| **Integrated SOAR** | Palo Alto XSOAR, Splunk SOAR | Automation, playbooks |

**Key Requirements**:
- Customizable incident taxonomy
- Role-based access control
- Audit trail for all actions
- Integration with SIEM/SOAR
- Regulatory reporting templates
- Mobile access for responders

#### 2. Forensic Workstation and Tools

**Primary Function**: Evidence collection, analysis, and preservation

| Component | Recommended Options |
|-----------|---------------------|
| **Disk Forensics** | EnCase, FTK, X-Ways |
| **Memory Forensics** | Volatility, Rekall |
| **Network Forensics** | Wireshark, NetworkMiner |
| **Malware Analysis** | IDA Pro, Ghidra, ANY.RUN |
| **Mobile Forensics** | Cellebrite, AXIOM |
| **Cloud Forensics** | Custom tools, Cado Security |

#### 3. Communication Platform

**Primary Function**: Secure incident communication and coordination

| Component | Purpose |
|-----------|---------|
| **Secure Chat** | Real-time team communication |
| **Video Conferencing** | War room and stakeholder briefings |
| **Notification System** | Automated alerts and escalations |
| **External Portal** | Stakeholder updates (if needed) |

#### 4. Documentation and Reporting

**Primary Function**: Structured documentation and regulatory reporting

| Component | Purpose |
|-----------|---------|
| **Template System** | Standardized reports and forms |
| **Wiki/Knowledge Base** | Runbooks, procedures, lessons learned |
| **Report Generator** | Automated report creation |
| **Compliance Tracking** | Regulatory submission management |

### Architecture Diagram

```
                    +------------------+
                    |  External        |
                    |  Stakeholders    |
                    |                  |
                    |  - CSA/SingCERT  |
                    |  - Leadership    |
                    |  - Legal         |
                    +--------+---------+
                             |
                             | Notifications & Reports
                             v
+------------------------------------------------------------------+
|                    IR Platform Core                               |
|                                                                   |
|  +----------------+  +----------------+  +----------------+       |
|  | Case Mgmt      |  | Communication  |  | Reporting      |       |
|  | System         |  | Hub            |  | Engine         |       |
|  +-------+--------+  +-------+--------+  +-------+--------+       |
|          |                   |                   |                |
|          +-------------------+-------------------+                |
|                              |                                    |
|  +----------------+  +-------+--------+  +----------------+       |
|  | Playbook       |  | Investigation  |  | Evidence       |       |
|  | Engine         |  | Workspace      |  | Repository     |       |
|  +----------------+  +----------------+  +----------------+       |
|                                                                   |
+------------------------------------------------------------------+
            |                    |                    |
            v                    v                    v
+------------------+  +------------------+  +------------------+
|   SOC Platform   |  | Threat Intel     |  | Forensic Tools   |
|   (SIEM/EDR)     |  | Platform         |  | (Lab)            |
+------------------+  +------------------+  +------------------+
```

---

## Case Management

### Incident Classification

#### Severity Levels

| Level | Name | Definition | SLA (Initial Response) | SLA (Update Frequency) |
|-------|------|------------|------------------------|------------------------|
| **P1** | Critical | Active breach, data exfiltration, ransomware, CII impact | 15 minutes | Every 30 minutes |
| **P2** | High | Confirmed compromise, significant threat, potential CII | 30 minutes | Every 2 hours |
| **P3** | Medium | Suspected compromise, contained threat, investigation needed | 2 hours | Every 8 hours |
| **P4** | Low | Minor incidents, policy violations, false positives | 8 hours | Daily |

#### Incident Categories

| Category | Sub-Categories | Example |
|----------|----------------|---------|
| **Malware** | Ransomware, Trojan, Worm, Botnet | Emotet infection |
| **Unauthorized Access** | Account compromise, lateral movement, privilege escalation | Stolen credentials used |
| **Data Breach** | Exfiltration, exposure, loss | Customer data leaked |
| **Denial of Service** | DDoS, resource exhaustion | Website unavailable |
| **Insider Threat** | Malicious, negligent, compromised | Employee data theft |
| **Phishing** | Credential harvest, malware delivery, BEC | Spear-phishing attack |
| **Vulnerability Exploitation** | Zero-day, known CVE | Log4j exploitation |
| **Policy Violation** | Acceptable use, data handling | Unauthorized cloud storage |

#### CII-Specific Classification

| CII Flag | Trigger | Additional Requirements |
|----------|---------|------------------------|
| **CII Involved** | Incident affects designated CII | 2-hour notification to CSA |
| **APT Suspected** | Indicators of nation-state activity | Enhanced tracking, attribution |
| **Cross-Sector** | Multiple CII sectors affected | Coordinated response |
| **STCC** | Temporary critical system | Time-limited enhanced monitoring |

### Case Workflow

#### Standard Incident Workflow

```
[Detection/Report]
       |
       v
[Triage & Classification]
       |
       +---> P1/P2: Immediate Escalation
       |
       v
[Case Creation]
       |
       v
[Investigation]
       |
       +---> [Containment] (if active threat)
       |
       v
[Analysis]
       |
       v
[Remediation]
       |
       v
[Recovery]
       |
       v
[Closure]
       |
       v
[Post-Incident Review]
```

#### CII Incident Workflow (Enhanced)

```
[Detection/Report]
       |
       v
[Initial Triage: CII Check]
       |
       +---> CII Confirmed: Start 2-Hour Timer
       |
       v
[Case Creation with CII Flag]
       |
       v
[Immediate Actions]
       |
       +---> [Containment]
       +---> [CSA Notification (< 2 hours)]
       +---> [Leadership Notification]
       |
       v
[Enhanced Investigation]
       |
       +---> [Root Cause Analysis]
       +---> [APT Assessment]
       |
       v
[Remediation with Approval]
       |
       v
[Recovery with Verification]
       |
       v
[CSA Report (< 14 days)]
       |
       v
[Closure with Regulatory Sign-off]
```

### Case Data Model

```
Incident
├── case_id (unique identifier)
├── title (descriptive name)
├── description (detailed narrative)
├── status (new, in_progress, contained, resolved, closed)
├── severity (P1, P2, P3, P4)
├── category (malware, unauthorized_access, etc.)
├── cii_involved (boolean)
├── apt_suspected (boolean)
├── created_at (timestamp)
├── detected_at (timestamp)
├── contained_at (timestamp)
├── resolved_at (timestamp)
├── closed_at (timestamp)
├── assigned_to (responder)
├── escalation_path (chain)
├── affected_assets (array)
├── affected_users (array)
├── related_cases (array)
├── observables (IOCs)
├── tasks (sub-tasks)
├── timeline (events log)
├── evidence (references)
├── communications (log)
├── regulatory_submissions (references)
└── lessons_learned (post-incident)
```

### Escalation Matrix

| Condition | Escalation Target | Time Limit |
|-----------|-------------------|------------|
| P1 declared | SOC Manager + IR Lead + CISO | Immediate |
| CII confirmed | CSA Liaison + Sector Lead | 30 minutes |
| APT suspected | Threat Intel Lead + CISO | 1 hour |
| Data breach confirmed | Legal + Privacy + CISO | 1 hour |
| Regulatory deadline | Compliance Officer | 1 hour before |
| Unresolved > SLA | Next management level | SLA breach |

---

## Forensics Integration

### Forensic Capabilities Framework

#### Evidence Types

| Evidence Type | Collection Method | Tools | Priority |
|---------------|-------------------|-------|----------|
| **Memory** | Live acquisition | Volatility, Magnet RAM | Critical (volatile) |
| **Disk Images** | Forensic imaging | FTK Imager, EnCase | High |
| **Network Captures** | PCAP collection | Wireshark, tcpdump | High (if ongoing) |
| **Logs** | Export/collection | Native + SIEM | Critical |
| **Cloud Artifacts** | API/Console export | Cloud-native + custom | High |
| **Malware Samples** | Quarantine collection | EDR, manual | High |
| **Configuration** | Snapshot/export | Native tools | Medium |

#### Evidence Collection Workflow

```
[Evidence Identified]
       |
       v
[Volatility Assessment]
       |
       +---> High: Collect immediately (memory, active connections)
       |
       v
[Documentation: Pre-Collection]
       |
       +---> Hash original (if possible)
       +---> Photograph physical evidence
       +---> Document system state
       |
       v
[Collection Using Approved Tools]
       |
       +---> Use write blockers
       +---> Forensic imaging
       +---> Proper packaging
       |
       v
[Hash Verification]
       |
       v
[Chain of Custody Documentation]
       |
       v
[Secure Storage]
```

### Chain of Custody Management

#### Chain of Custody Form

```
EVIDENCE CHAIN OF CUSTODY FORM

Case ID: ________________
Evidence ID: ________________
Description: ________________

COLLECTION
Collected by: ________________
Date/Time: ________________
Location: ________________
Method: ________________
Hash (Original): ________________

TRANSFERS
| Date/Time | From | To | Purpose | Signature |
|-----------|------|-----|---------|-----------|
|           |      |     |         |           |
|           |      |     |         |           |

STORAGE
Location: ________________
Access Log: ________________

ANALYSIS
Analyst: ________________
Date/Time: ________________
Working Copy Hash: ________________

DISPOSITION
Final Status: ________________
Disposition Date: ________________
Authorization: ________________
```

#### Evidence Repository Structure

```
/evidence
├── /active_cases
│   └── /[case_id]
│       ├── /disk_images
│       ├── /memory_dumps
│       ├── /network_captures
│       ├── /logs
│       ├── /malware_samples
│       ├── /documents
│       └── chain_of_custody.json
├── /archived_cases
│   └── /[year]/[case_id]
└── /reference
    ├── /tools
    └── /known_good
```

### Forensic Analysis Integration

#### Analysis Workflow

```
[Case Assigned to Forensics]
       |
       v
[Scope Definition]
       |
       +---> What questions need answering?
       +---> What evidence is available?
       |
       v
[Evidence Preparation]
       |
       +---> Create working copies
       +---> Verify hashes
       |
       v
[Analysis Execution]
       |
       +---> Timeline creation
       +---> Artifact extraction
       +---> Malware analysis
       +---> Network analysis
       |
       v
[Findings Documentation]
       |
       v
[Report Generation]
       |
       v
[Case Integration]
```

#### Forensic Findings Template

```markdown
## Forensic Analysis Report

### Case Information
- Case ID: [ID]
- Analyst: [Name]
- Date Range: [Start] to [End]

### Evidence Analyzed
| Item | Type | Hash | Source |
|------|------|------|--------|

### Analysis Questions
1. [Question 1]
2. [Question 2]

### Timeline of Events
| Timestamp | Event | Source | Confidence |
|-----------|-------|--------|------------|

### Key Findings
1. [Finding 1]
2. [Finding 2]

### Indicators of Compromise
| Type | Value | Context |
|------|-------|---------|

### Attribution Assessment
[Assessment with confidence level]

### Conclusions
[Summary]

### Recommendations
1. [Recommendation 1]
2. [Recommendation 2]
```

### Forensic Lab Requirements

#### Hardware Requirements

| Component | Specification | Purpose |
|-----------|---------------|---------|
| **Workstations** | High-spec, isolated | Analysis work |
| **Write Blockers** | Hardware + software | Evidence protection |
| **Evidence Storage** | Encrypted, access-controlled | Secure repository |
| **Malware Lab** | Air-gapped or sandbox | Safe malware analysis |
| **Imaging Devices** | Hardware imagers | Disk acquisition |

#### Network Requirements

| Zone | Connectivity | Purpose |
|------|--------------|---------|
| **Analysis Zone** | Isolated from production | General forensics |
| **Malware Zone** | Air-gapped | Malware detonation |
| **Case Management** | Connected (secure) | Collaboration |

---

## Communication Workflows

### Internal Communication

#### Notification Matrix

| Event | Notify Immediately | Notify Within 1 Hour | Notify Within 24 Hours |
|-------|-------------------|---------------------|------------------------|
| **P1 Incident** | IR Lead, SOC Mgr, CISO | CIO, Legal, Business Owner | All stakeholders |
| **P2 Incident** | IR Lead, SOC Mgr | CISO (summary) | Business Owner |
| **CII Incident** | CSA Liaison, Sector Lead, CISO | Legal, Compliance | As required |
| **Data Breach** | CISO, Legal, Privacy Officer | CEO (if significant) | PDPA notification |
| **APT Suspected** | CISO, Threat Intel Lead | CSA (if confirmed) | As required |

#### Communication Channels by Severity

| Severity | Primary Channel | Secondary Channel | Documentation |
|----------|-----------------|-------------------|---------------|
| **P1** | War Room (voice/video) | Secure chat (real-time) | Continuous log |
| **P2** | Secure chat | Email (summaries) | Hourly updates |
| **P3** | Secure chat | Email | Daily updates |
| **P4** | Email | Ticket system | As closed |

### War Room Protocol

#### War Room Activation Criteria

- P1 incident declared
- CII incident confirmed
- Multiple coordinated attacks
- Executive decision

#### War Room Structure

```
War Room Roles
├── Incident Commander (IC)
│   └── Overall coordination and decisions
├── Technical Lead
│   └── Technical investigation direction
├── Communications Lead
│   └── Internal/external communications
├── Operations Representative
│   └── Business impact and recovery
├── Scribe
│   └── Documentation and timeline
└── Subject Matter Experts (as needed)
    └── Forensics, Malware, Network, etc.
```

#### War Room Cadence

| Time | Activity | Lead |
|------|----------|------|
| T+0 | Initial briefing, roles assigned | IC |
| T+15m | Status update, initial findings | Technical Lead |
| T+30m | Containment decision | IC |
| Every 30m | Status update | Rotating |
| As needed | Stakeholder update | Comms Lead |
| At closure | Final debrief | IC |

### External Communication

#### Regulatory Communication (CSA/SingCERT)

| Communication Type | Timeline | Content | Channel |
|-------------------|----------|---------|---------|
| **Initial Notification** | Within 2 hours | Basic facts, classification | Secure portal/hotline |
| **Update Reports** | As significant developments | Progress, findings | Secure portal |
| **Root Cause Report** | Within 14 days | Full analysis | Secure portal |
| **Closure Report** | At resolution | Final summary, actions | Secure portal |

#### Notification Template (Initial)

```
CYBERSECURITY INCIDENT NOTIFICATION

CLASSIFICATION: [CII/Non-CII]
SEVERITY: [P1/P2/P3/P4]
DATE/TIME DETECTED: [Timestamp]
DATE/TIME OF INCIDENT: [If known]

ORGANIZATION: [Name]
SECTOR: [CII Sector if applicable]

INCIDENT SUMMARY:
[Brief description - 2-3 sentences]

SYSTEMS AFFECTED:
[List affected systems]

CURRENT STATUS:
[Ongoing/Contained/Resolved]

IMMEDIATE ACTIONS TAKEN:
1. [Action 1]
2. [Action 2]

POINT OF CONTACT:
Name: [Name]
Phone: [Number]
Email: [Email]

NEXT UPDATE: [Timestamp]
```

#### Stakeholder Communication Plan

| Stakeholder | Information Needs | Frequency | Format |
|-------------|-------------------|-----------|--------|
| **Executive Leadership** | Impact, timeline, resources | Every 4 hours (P1) | Brief/call |
| **Board/Audit Committee** | Significant incidents | As needed | Formal report |
| **Affected Business Units** | Impact, recovery timeline | Daily | Meeting/email |
| **Legal** | Liability, regulatory | As needed | Meeting |
| **PR/Communications** | If public disclosure | As needed | Coordination |
| **Customers (if affected)** | As required by law/contract | Post-incident | Formal notice |

### Communication Templates

#### Executive Briefing Template

```markdown
## Incident Executive Briefing

**Date/Time**: [Timestamp]
**Briefing #**: [Number]
**Classification**: [Internal/Confidential]

### Status Summary
| Aspect | Status |
|--------|--------|
| Incident Status | [Ongoing/Contained/Resolved] |
| Severity | [P1/P2/P3/P4] |
| Business Impact | [Critical/High/Medium/Low] |

### Key Facts
- Incident detected: [Timestamp]
- Root cause: [Known/Under investigation]
- Systems affected: [Count/List]
- Data affected: [Yes/No/Unknown]

### Current Actions
1. [Action 1] - [Status]
2. [Action 2] - [Status]

### Business Impact
[Description of operational impact]

### Resource Requirements
[Any additional resources needed]

### Timeline to Resolution
[Estimated timeline]

### Next Update
[Timestamp]
```

---

## Playbook Management

### Playbook Framework

#### Playbook Structure

```
Playbook
├── Metadata
│   ├── Name
│   ├── Version
│   ├── Author
│   ├── Last Updated
│   ├── Category (incident type)
│   └── Severity Applicability
├── Trigger Conditions
│   └── When to execute this playbook
├── Initial Response (first 15-30 minutes)
│   ├── Triage steps
│   ├── Initial containment
│   └── Notifications
├── Investigation (hours to days)
│   ├── Data collection
│   ├── Analysis steps
│   └── Documentation
├── Containment (parallel with investigation)
│   ├── Short-term containment
│   └── Long-term containment
├── Eradication
│   ├── Removal steps
│   └── Verification
├── Recovery
│   ├── Restoration steps
│   └── Validation
├── Post-Incident
│   ├── Documentation
│   └── Lessons learned triggers
└── Appendices
    ├── Tools and commands
    ├── Templates
    └── Contacts
```

### Core Playbooks

#### Playbook 1: Ransomware Response

```markdown
## Ransomware Response Playbook

### Trigger Conditions
- Ransomware executable detected
- File encryption activity observed
- Ransom note discovered
- User reports of inaccessible files

### Initial Response (T+0 to T+30m)

#### Immediate Actions
1. **ISOLATE affected systems** (network disconnect)
   - Do NOT power off (preserve memory/evidence)
   - Disconnect from network (cable or disable interface)

2. **Alert and Escalate**
   - Notify SOC Manager
   - Activate P1 protocol
   - If CII: Start 2-hour notification clock

3. **Preserve Evidence**
   - Memory dump (before isolation if possible)
   - Screenshot ransom note
   - Document encrypted file extensions

4. **Assess Scope**
   - Which systems showing indicators?
   - Any network shares affected?
   - Backup status?

### Investigation (T+30m to T+24h)

#### Determine Attack Vector
- [ ] Phishing email?
- [ ] Exploited vulnerability?
- [ ] Compromised credentials?
- [ ] Supply chain?

#### Identify Ransomware Variant
- [ ] File extension analysis
- [ ] Ransom note text
- [ ] ID Ransomware submission
- [ ] Check for known decryptors

#### Scope Assessment
- [ ] All affected systems identified
- [ ] Patient zero identified
- [ ] Lateral movement mapped
- [ ] Data exfiltration indicators

### Containment

#### Network Containment
- [ ] Isolate affected network segments
- [ ] Block known C2 indicators
- [ ] Disable affected accounts
- [ ] Monitor for spread

#### Backup Protection
- [ ] Verify backup integrity
- [ ] Isolate backup systems
- [ ] Confirm air-gapped copies exist

### Eradication

#### Removal Steps
1. Rebuild or restore from clean backup
2. Patch exploited vulnerabilities
3. Reset compromised credentials
4. Update security controls

### Recovery

#### Restoration Process
1. Prioritize critical systems
2. Restore from verified clean backups
3. Validate system integrity
4. Phased return to production
5. Enhanced monitoring period

### Do NOT
- Do NOT pay ransom (government policy)
- Do NOT negotiate without approval
- Do NOT power off systems (evidence)
- Do NOT restore before understanding scope

### Contacts
- [List relevant contacts]
```

#### Playbook 2: Data Breach Response

```markdown
## Data Breach Response Playbook

### Trigger Conditions
- Data exfiltration detected
- Unauthorized data access confirmed
- External notification of breach
- Data found externally

### Initial Response (T+0 to T+1h)

#### Immediate Actions
1. **Confirm and Classify**
   - Verify breach is real (not false positive)
   - Determine data types affected
   - Estimate records/individuals affected

2. **Alert and Escalate**
   - CISO, Legal, Privacy Officer
   - If personal data: PDPA notification considerations
   - If CII: CSA notification requirements

3. **Contain**
   - Block exfiltration path
   - Revoke compromised access
   - Preserve evidence

### Investigation

#### Determine Scope
- [ ] What data was accessed/taken?
- [ ] How many records/individuals?
- [ ] What sensitivity level?
- [ ] What time period?

#### Attribution
- [ ] Internal or external actor?
- [ ] Authorized access misused?
- [ ] Technical compromise?

### Regulatory Considerations

#### PDPA Notification (if applicable)
- Notify PDPC if significant harm likely
- Notify affected individuals if significant harm likely
- Timeline: As soon as practicable

#### Cybersecurity Act (if CII)
- 2-hour notification to CSA
- 14-day root cause report

### Communication
- [ ] Legal review of communications
- [ ] Prepare customer notification (if needed)
- [ ] Prepare regulatory notification
- [ ] Media response (if public)
```

#### Playbook 3: APT/Advanced Threat Response

```markdown
## APT/Advanced Threat Response Playbook

### Trigger Conditions
- APT indicators detected
- Threat intel match to known APT
- Sophisticated persistence mechanisms
- Multi-stage attack evidence

### Initial Response (T+0 to T+1h)

#### Critical: DO NOT ALERT THE ADVERSARY
- Avoid obvious containment actions initially
- Maintain operational security
- Plan coordinated response

#### Immediate Actions
1. **Assess Silently**
   - Confirm indicators
   - Initial scope assessment
   - Do not modify affected systems

2. **Escalate Appropriately**
   - CISO, Threat Intel Lead
   - CSA notification (suspected APT)
   - Consider law enforcement coordination

3. **Assemble Team**
   - Senior IR personnel only
   - Need-to-know basis
   - Secure communication channel

### Investigation (Extended)

#### Intelligence-Driven Analysis
- [ ] Map to known APT TTPs
- [ ] ATT&CK technique coverage
- [ ] Compare to threat intel
- [ ] Attribution assessment

#### Comprehensive Scoping
- [ ] All entry points identified?
- [ ] All persistence mechanisms?
- [ ] All compromised credentials?
- [ ] Any data accessed/exfiltrated?

#### Evidence Collection
- [ ] Memory from all affected systems
- [ ] Full disk images
- [ ] Network captures
- [ ] All relevant logs

### Containment

#### Coordinated Eviction
- Plan comprehensive removal
- Execute simultaneously across all affected systems
- Block all known indicators
- Reset all potentially compromised credentials

### Post-Incident

#### Enhanced Monitoring
- Extended monitoring period (90 days minimum)
- Hunt for re-entry attempts
- Monitor for related activity

#### Strategic Improvements
- Gap analysis against ATT&CK
- Detection improvements
- Architecture hardening
```

### Playbook Management Lifecycle

```
[Develop] --> [Review] --> [Approve] --> [Publish] --> [Train]
                                              |
    +------------------------------------------+
    |
    v
[Execute] --> [Evaluate] --> [Improve] --> [Update] --> [Review] ...
```

#### Playbook Testing

| Test Type | Frequency | Participants |
|-----------|-----------|--------------|
| Tabletop Exercise | Quarterly | IR Team + Stakeholders |
| Simulation | Semi-annually | Full exercise |
| Live Drill | Annually | Organization-wide |
| Technical Validation | Per playbook update | IR Team |

---

## Post-Incident Analysis

### Post-Incident Review Process

#### Review Timeline

| Activity | When | Duration |
|----------|------|----------|
| Hot wash (immediate debrief) | Within 24 hours of resolution | 30-60 minutes |
| Detailed technical review | Within 1 week | 2-4 hours |
| Lessons learned meeting | Within 2 weeks | 1-2 hours |
| Report finalization | Within 30 days | N/A |
| Implementation tracking | Ongoing | Quarterly review |

#### Hot Wash Questions

1. What happened? (Brief timeline)
2. What went well?
3. What didn't go well?
4. Immediate improvement ideas?
5. Any recognition needed?

#### Detailed Review Meeting Agenda

```markdown
## Post-Incident Review Meeting

### Attendees
[List]

### Agenda

1. **Incident Summary** (10 min)
   - What happened
   - Timeline overview
   - Final scope and impact

2. **Response Timeline Review** (20 min)
   - Walk through detailed timeline
   - Identify decision points
   - Note delays or gaps

3. **What Worked Well** (15 min)
   - Effective actions
   - Tool/process successes
   - Team coordination wins

4. **What Needs Improvement** (20 min)
   - Detection gaps
   - Response delays
   - Communication issues
   - Tool limitations
   - Process gaps

5. **Root Cause Analysis** (15 min)
   - Technical root cause
   - Process/people factors
   - Environmental factors

6. **Action Items** (10 min)
   - Specific improvements
   - Owners assigned
   - Deadlines set

7. **Wrap-up** (5 min)
```

### Root Cause Analysis

#### 5 Whys Methodology

```
Incident: Ransomware spread to 50 systems

Why 1: Ransomware was able to spread laterally
       -> Because credentials were reused across systems

Why 2: Why were credentials reused?
       -> Because local admin passwords were identical

Why 3: Why were passwords identical?
       -> Because LAPS was not implemented

Why 4: Why wasn't LAPS implemented?
       -> Because it was deprioritized in project backlog

Why 5: Why was it deprioritized?
       -> Because security projects compete with business projects without clear prioritization framework

Root Cause: Lack of security project prioritization framework
Action: Implement security project scoring and executive sponsorship process
```

#### Fault Tree Analysis (for complex incidents)

```
                    [Ransomware Outbreak]
                           |
        +------------------+------------------+
        |                  |                  |
   [Initial Entry]   [Lateral Movement]  [Detection Failure]
        |                  |                  |
   [Phishing]         [Credential]       [Alert Not]
                      [Reuse]            [Investigated]
        |                  |                  |
   [Link Clicked]    [No LAPS]           [Alert Fatigue]
```

### Improvement Tracking

#### Action Item Template

| Field | Content |
|-------|---------|
| ID | POSTIR-2026-001-001 |
| Finding | Detection delay of 4 hours |
| Root Cause | EDR rule not enabled for technique |
| Action | Enable and tune EDR rule for T1059.001 |
| Owner | Detection Engineering Lead |
| Deadline | 2026-02-15 |
| Status | In Progress |
| Evidence of Completion | Rule deployed, test results |

#### Improvement Categories

| Category | Examples |
|----------|----------|
| **Detection** | New rules, tuning, coverage gaps |
| **Prevention** | Controls, hardening, patching |
| **Process** | Playbooks, procedures, communication |
| **Technology** | Tool gaps, integration, automation |
| **People** | Training, staffing, skills |
| **Architecture** | Design changes, segmentation |

### Metrics and Reporting

#### Incident Metrics

| Metric | Definition | Target |
|--------|------------|--------|
| MTTD | Time from compromise to detection | < 24 hours |
| MTTR | Time from detection to resolution | < 48 hours (P2) |
| MTTC | Time from detection to containment | < 2 hours (P1) |
| Regulatory Compliance | Reports filed on time | 100% |
| Playbook Coverage | Incidents with applicable playbook | > 90% |
| Improvement Implementation | Actions completed on time | > 80% |

#### Quarterly Incident Report

```markdown
## Quarterly Incident Report

### Period: Q[X] 20XX

### Summary Statistics
| Metric | Q[X] | Q[X-1] | Trend |
|--------|------|--------|-------|
| Total Incidents | XX | XX | +/-% |
| P1 Incidents | XX | XX | +/-% |
| CII Incidents | XX | XX | +/-% |
| Average MTTD | XX hrs | XX hrs | +/-% |
| Average MTTR | XX hrs | XX hrs | +/-% |

### Incident Categories
[Breakdown by type]

### Notable Incidents
[Summary of significant incidents]

### Improvement Actions
| Status | Count |
|--------|-------|
| Completed | XX |
| In Progress | XX |
| Overdue | XX |

### Recommendations
[Strategic recommendations]
```

---

## Implementation Considerations

### Deployment Phases

#### Phase 1: Foundation (Months 1-3)

| Activity | Duration | Deliverables |
|----------|----------|--------------|
| Case management deployment | 6 weeks | Platform operational |
| Playbook development (core) | 4 weeks | 5 core playbooks |
| Communication setup | 2 weeks | Channels configured |
| Team training | 2 weeks | IR team certified |

#### Phase 2: Enhancement (Months 4-6)

| Activity | Duration | Deliverables |
|----------|----------|--------------|
| Forensic lab setup | 6 weeks | Lab operational |
| Integration with SOC/TIP | 4 weeks | Connected platforms |
| Additional playbooks | 4 weeks | 10+ playbooks |
| Tabletop exercises | 2 weeks | Exercises conducted |

#### Phase 3: Optimization (Months 7-12)

| Activity | Duration | Deliverables |
|----------|----------|--------------|
| Automation integration | 8 weeks | SOAR integration |
| Advanced forensics | Ongoing | Full capability |
| Metrics and reporting | 4 weeks | Dashboards live |
| Continuous improvement | Ongoing | Regular reviews |

### Staffing Requirements

| Role | FTE | Responsibilities |
|------|-----|------------------|
| IR Manager | 1 | Team leadership, escalation |
| Senior IR Analyst | 2 | Complex investigations, mentoring |
| IR Analyst | 3 | Incident handling, analysis |
| Forensic Analyst | 2 | Evidence collection, forensics |
| **Total** | **8** | |

### Success Metrics

| Metric | Target | Timeframe |
|--------|--------|-----------|
| Regulatory compliance | 100% | Immediate |
| Playbook coverage | 90% | 6 months |
| MTTR improvement | 25% reduction | 12 months |
| Training completion | 100% | Quarterly |
| Post-incident reviews | 100% (P1/P2) | Immediate |

---

## Related Documents

- [01-soc-platform.md](./01-soc-platform.md) - SOC integration
- [02-threat-intelligence-platform.md](./02-threat-intelligence-platform.md) - TI integration
- [04-security-automation.md](./04-security-automation.md) - Automation playbooks
- [05-implementation-roadmap.md](./05-implementation-roadmap.md) - Overall roadmap

---

## References

- [NIST SP 800-61r3](https://csrc.nist.gov/publications/detail/sp/800-61/rev-3/final) - Incident Response Recommendations
- [Singapore Cybersecurity Act](https://www.csa.gov.sg/legislation/cybersecurity-act/) - Regulatory requirements
- [SANS Incident Handler's Handbook](https://www.sans.org/white-papers/33901/) - IR methodology
- [TheHive Project](https://thehive-project.org/) - Open source IR platform

---

*Last Updated: January 2026*
