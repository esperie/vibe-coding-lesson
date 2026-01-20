# Red Team Infrastructure

> Comprehensive documentation for establishing and operating red team infrastructure for authorized adversary simulation operations.

**Last Updated**: January 2026

---

## Table of Contents

1. [C2 Framework Considerations](#c2-framework-considerations)
2. [Attack Infrastructure Setup](#attack-infrastructure-setup)
3. [Evasion and Persistence Techniques](#evasion-and-persistence-techniques)
4. [Physical Security Testing](#physical-security-testing)
5. [Social Engineering Platforms](#social-engineering-platforms)
6. [Operational Security](#operational-security)
7. [Legal and Ethical Boundaries](#legal-and-ethical-boundaries)
8. [Infrastructure Lifecycle Management](#infrastructure-lifecycle-management)

---

## C2 Framework Considerations

### Overview

Command and Control (C2) frameworks enable red team operators to maintain communication with compromised systems. Selection and deployment must balance capability with operational security and detection evasion.

### Commercial C2 Frameworks

#### Cobalt Strike

**Description**: Industry-leading adversary simulation and red team operations platform.

| Aspect | Details |
|--------|---------|
| **Developer** | Fortra (formerly HelpSystems) |
| **Licensing** | Commercial, annual subscription |
| **Capabilities** | Beacon payload, Malleable C2, team collaboration |
| **Support** | Professional support, regular updates |

**Core Components**:

| Component | Purpose |
|-----------|---------|
| **Team Server** | Central C2 server, multi-operator support |
| **Beacon** | Payload for compromised systems |
| **Malleable C2** | Customizable traffic profiles |
| **Aggressor Script** | Automation and customization |

**Malleable C2 Profiles**:

Profiles enable customization of:
- HTTP/HTTPS traffic patterns
- DNS communication patterns
- Process injection behavior
- Memory indicators

**Example Profile Considerations**:

| Profile Aspect | Customization |
|----------------|---------------|
| User-Agent | Match legitimate browser traffic |
| URI patterns | Mimic legitimate application endpoints |
| Jitter | Randomize beacon timing |
| Headers | Match expected application headers |

**Strengths**:
- Mature, well-documented platform
- Strong collaboration features
- Extensive customization
- Active community and training

**Considerations**:
- Heavily signatured by EDR vendors
- Requires expertise for evasion
- Premium pricing
- Careful license management required

**Government Use Case**: Professional red team operations, APT emulation, exercise scenarios.

---

#### Nighthawk (MDSec)

**Description**: Advanced C2 framework designed for sophisticated red team operations.

| Aspect | Details |
|--------|---------|
| **Developer** | MDSec |
| **Focus** | Advanced evasion, mature security environments |
| **Capabilities** | Advanced injection, ETW bypass, signature avoidance |

**Strengths**:
- Designed for advanced evasion
- Lower signature profile than Cobalt Strike
- Regular evasion updates

**Considerations**:
- Limited availability
- Premium pricing
- Smaller community

**Government Use Case**: Testing mature security environments, advanced adversary emulation.

---

#### Brute Ratel C4

**Description**: Red team C2 framework with focus on EDR evasion.

| Aspect | Details |
|--------|---------|
| **Developer** | Dark Vortex |
| **Focus** | EDR/XDR evasion |
| **Capabilities** | Syscall-based execution, process hollowing |

**Strengths**:
- Strong EDR evasion capabilities
- Modern architecture
- Active development

**Considerations**:
- Newer platform, less community support
- License vetting required
- Growing signature detection

**Government Use Case**: EDR effectiveness testing, advanced detection validation.

---

### Open Source C2 Frameworks

#### Mythic

**Description**: Cross-platform, modular C2 framework with web-based UI.

| Aspect | Details |
|--------|---------|
| **Type** | Open source |
| **Architecture** | Docker-based, modular agents |
| **Agents** | Apollo (Windows), Poseidon (macOS/Linux), others |
| **UI** | Modern web interface |

**Agent Ecosystem**:

| Agent | Platform | Capabilities |
|-------|----------|--------------|
| Apollo | Windows | Full-featured, C# |
| Poseidon | macOS/Linux | Go-based, cross-platform |
| Medusa | Python | Python implant |
| Athena | Cross-platform | .NET cross-platform |

**Strengths**:
- Free and open source
- Modern architecture
- Active development
- Multi-agent support

**Considerations**:
- Requires operational expertise
- Detection signatures developing
- Self-supported

**Government Use Case**: Flexible red team operations, training, budget-conscious operations.

---

#### Sliver

**Description**: Open-source cross-platform adversary emulation framework.

| Aspect | Details |
|--------|---------|
| **Type** | Open source (BishopFox) |
| **Language** | Go |
| **Implants** | Windows, Linux, macOS |
| **Protocols** | MTLS, WireGuard, HTTP(S), DNS |

**Strengths**:
- Cross-platform implants
- Multiple C2 protocols
- Active development (BishopFox)
- Free

**Considerations**:
- Growing detection signatures
- Less mature than Cobalt Strike
- Limited GUI

**Government Use Case**: Alternative C2, cross-platform testing, training.

---

#### Havoc

**Description**: Modern post-exploitation C2 framework.

| Aspect | Details |
|--------|---------|
| **Type** | Open source |
| **Focus** | Modern Windows environments |
| **Features** | Demon agent, indirect syscalls |

**Strengths**:
- Modern evasion techniques
- Active development
- Free

**Considerations**:
- Newer platform
- Windows-focused
- Smaller community

---

### C2 Framework Comparison

| Framework | Evasion | Collaboration | Cost | Community | Government Suitability |
|-----------|---------|---------------|------|-----------|----------------------|
| Cobalt Strike | High (with tuning) | Excellent | High | Large | Established choice |
| Nighthawk | Very High | Good | High | Small | Advanced operations |
| Brute Ratel | Very High | Good | High | Growing | EDR testing |
| Mythic | Moderate | Good | Free | Growing | Flexible operations |
| Sliver | Moderate | Moderate | Free | Growing | Cross-platform |
| Havoc | Moderate-High | Moderate | Free | Small | Modern testing |

---

## Attack Infrastructure Setup

### Infrastructure Architecture

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    RED TEAM INFRASTRUCTURE ARCHITECTURE                      │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│    ┌───────────────────────────────────────────────────────────────────┐    │
│    │                    TIER 1: REDIRECTORS                            │    │
│    │    (Short-lived, easily burned, no attribution)                   │    │
│    │    ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐            │    │
│    │    │ HTTP    │  │ HTTPS   │  │  DNS    │  │  SMTP   │            │    │
│    │    │Redirector│  │Redirector│  │Redirector│  │Redirector│         │    │
│    │    └────┬────┘  └────┬────┘  └────┬────┘  └────┬────┘            │    │
│    └─────────│───────────│───────────│───────────│──────────────────────┘   │
│              │           │           │           │                          │
│    ┌─────────▼───────────▼───────────▼───────────▼─────────────────────┐    │
│    │                    TIER 2: TEAM SERVERS                           │    │
│    │    (Protected, moderate lifespan, some attribution protection)    │    │
│    │    ┌──────────────────────┐  ┌──────────────────────┐            │    │
│    │    │   Primary Team       │  │   Backup Team        │            │    │
│    │    │   Server             │  │   Server             │            │    │
│    │    └──────────┬───────────┘  └──────────┬───────────┘            │    │
│    └───────────────│──────────────────────────│──────────────────────────┘  │
│                    │                          │                              │
│    ┌───────────────▼──────────────────────────▼─────────────────────────┐   │
│    │                    TIER 3: OPERATIONS                              │   │
│    │    (Long-lived, maximum protection, full attribution protection)   │   │
│    │    ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐  │   │
│    │    │  Payload Dev    │  │   Phishing      │  │   Data Staging  │  │   │
│    │    │  Server         │  │   Server        │  │   Server        │  │   │
│    │    └─────────────────┘  └─────────────────┘  └─────────────────┘  │   │
│    └─────────────────────────────────────────────────────────────────────┘  │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Infrastructure Components

#### Redirectors

**Purpose**: Proxy traffic to hide team server location and enable quick infrastructure rotation.

| Type | Implementation | Use Case |
|------|----------------|----------|
| **HTTP/HTTPS** | Apache mod_rewrite, Nginx | Web C2 traffic |
| **DNS** | dnscat2, DNS redirectors | DNS C2 channels |
| **SMTP** | Mail relay servers | Phishing operations |
| **Domain Fronting** | CDN abuse (where legal) | Evasion (limited availability) |

**Redirector Configuration Considerations**:

| Aspect | Implementation |
|--------|----------------|
| Traffic filtering | Only forward valid C2 traffic |
| Logging | Minimal logs, secure handling |
| Rotation | Plan for rapid replacement |
| Attribution | No links to organization |

---

#### Team Servers

**Purpose**: Central command infrastructure for operator coordination.

| Consideration | Implementation |
|---------------|----------------|
| **Isolation** | Separate network, no direct internet |
| **Access** | VPN-only, MFA required |
| **Backup** | Regular backups, disaster recovery |
| **Monitoring** | Operator activity logging |

---

#### Payload Infrastructure

**Purpose**: Host and serve payloads for initial access.

| Type | Implementation | Notes |
|------|----------------|-------|
| **Web hosting** | Nginx, Apache | Payload delivery |
| **File hosting** | Cloud storage (burned accounts) | Document delivery |
| **Custom domains** | Aged, categorized domains | Trust and reputation |

---

### Domain and Certificate Management

#### Domain Selection Criteria

| Criterion | Rationale |
|-----------|-----------|
| **Age** | Older domains have better reputation |
| **Categorization** | Should match cover story |
| **History** | Clean history, no blocklisting |
| **TLD** | Legitimate TLDs (.com, .net, country-specific) |
| **Registration** | Privacy protection, separate registrar |

#### Certificate Considerations

| Approach | Pros | Cons |
|----------|------|------|
| Let's Encrypt | Free, automatic renewal | Short validity, some detection |
| Paid certificates | Longer validity, EV available | Cost, registration trail |
| Self-signed | Full control | Certificate warnings |

---

### Cloud Infrastructure

#### Provider Considerations

| Provider | Strengths | Considerations |
|----------|-----------|----------------|
| **AWS** | Global presence, services variety | Compliance monitoring |
| **Azure** | Microsoft ecosystem, legitimacy | Compliance monitoring |
| **DigitalOcean** | Simple, affordable | Reputation monitoring |
| **Vultr** | Flexible, affordable | Less enterprise features |
| **OVH** | Privacy-friendly | EU-based |

**Singapore-Specific Notes**:
- Some providers have Singapore data centers
- Consider regional privacy laws
- Local hosting may be required for certain tests

---

## Evasion and Persistence Techniques

### EDR/AV Evasion

#### Detection Categories

| Category | Description | Evasion Approach |
|----------|-------------|------------------|
| **Signature-based** | Known malware patterns | Payload customization, encoding |
| **Behavioral** | Suspicious activity patterns | Process masquerading, legitimate APIs |
| **Heuristic** | Unknown but suspicious | Sandbox evasion, environment awareness |
| **Memory-based** | In-memory detection | Memory obfuscation, unhooking |

#### Evasion Techniques

| Technique | Description | Difficulty |
|-----------|-------------|------------|
| **Payload encryption** | Encrypt payload until runtime | Low |
| **Syscall unhooking** | Remove EDR hooks from ntdll | Medium |
| **Direct syscalls** | Bypass userland hooks | Medium |
| **Process hollowing** | Inject into legitimate processes | Medium |
| **Module stomping** | Overwrite legitimate modules | High |
| **Callback exploitation** | Abuse legitimate callbacks | High |

#### AMSI Bypass

Antimalware Scan Interface bypass considerations:

| Approach | Description | Detection Risk |
|----------|-------------|----------------|
| Patching | Modify AMSI DLL in memory | Moderate |
| String obfuscation | Avoid AMSI-triggering strings | Low |
| Reflection | Use reflection to avoid scanning | Moderate |

**Note**: AMSI bypass techniques are constantly evolving as Microsoft updates detection.

---

### Persistence Mechanisms

#### Windows Persistence

| Technique | MITRE ID | Detection Difficulty |
|-----------|----------|---------------------|
| Registry Run Keys | T1547.001 | Easy |
| Scheduled Tasks | T1053.005 | Moderate |
| Services | T1543.003 | Moderate |
| WMI Subscriptions | T1546.003 | Hard |
| DLL Hijacking | T1574.001 | Hard |
| COM Hijacking | T1546.015 | Hard |
| Bootkit | T1542 | Very Hard |

#### Linux/macOS Persistence

| Technique | Platform | Detection Difficulty |
|-----------|----------|---------------------|
| Cron jobs | Both | Easy |
| Systemd services | Linux | Moderate |
| Launch Agents/Daemons | macOS | Moderate |
| Profile modifications | Both | Moderate |
| Kernel modules | Linux | Hard |

#### Selection Criteria

| Factor | Consideration |
|--------|---------------|
| **Stealth** | How easily detected? |
| **Reliability** | Survives reboots, updates? |
| **Flexibility** | Easy to modify/remove? |
| **Scope** | User vs. system level? |

---

### Credential Access Techniques

| Technique | Target | Tools | Detection Risk |
|-----------|--------|-------|----------------|
| **LSASS dump** | Local credentials | Mimikatz, nanodump | High |
| **SAM database** | Local accounts | secretsdump, reg save | Moderate |
| **DPAPI** | Stored credentials | SharpDPAPI | Moderate |
| **Kerberoasting** | Service accounts | Rubeus, Impacket | Moderate |
| **AS-REP Roasting** | No preauth accounts | Rubeus, Impacket | Low |
| **DCSync** | Domain credentials | Mimikatz, secretsdump | High |

---

## Physical Security Testing

### Overview

Physical security testing validates the effectiveness of physical access controls, often combined with social engineering.

### Scope Considerations

| Test Type | Description | Authorization Level |
|-----------|-------------|-------------------|
| **Passive Reconnaissance** | Observation, photography | Low (public areas) |
| **Active Testing** | Tailgating, lock picking | High (explicit authorization) |
| **Facility Penetration** | Full building access test | Very High (executive approval) |
| **Device Placement** | Rogue device deployment | Very High (specific approval) |

### Testing Techniques

#### Building Access Testing

| Technique | Description | Tools |
|-----------|-------------|-------|
| **Tailgating** | Following authorized personnel | Social skills |
| **Badge cloning** | Duplicate access credentials | Proxmark, flipper |
| **Lock bypass** | Mechanical lock vulnerabilities | Lock picks, bypass tools |
| **Door mechanisms** | Electronic door vulnerabilities | Under-door tools, REX sensors |

#### Device Placement

| Device Type | Purpose | Detection Method |
|-------------|---------|------------------|
| **USB drops** | Payload delivery | Network monitoring |
| **Rogue AP** | Network access | Wireless monitoring |
| **Keyloggers** | Credential capture | Physical inspection |
| **Network taps** | Traffic capture | Network monitoring |

### Physical Testing Ethics

**Critical Requirements**:

1. **Explicit written authorization** from facility owner
2. **Get-out-of-jail letter** from authorizing executive
3. **Emergency contact** available 24/7
4. **No actual theft** or damage to property
5. **Document all access** with timestamps
6. **Coordinate with security** (if not full red team)

---

## Social Engineering Platforms

### Overview

Social engineering tests the human element of security. Singapore has seen a 49% increase in phishing cases, making this testing critical.

### Phishing Platforms

#### Gophish

**Description**: Open-source phishing framework.

| Aspect | Details |
|--------|---------|
| **Type** | Open source |
| **Capabilities** | Email campaigns, landing pages, tracking |
| **Deployment** | Self-hosted |
| **Reporting** | Detailed campaign analytics |

**Features**:
- Campaign management
- Landing page cloning
- Credential capture
- Click tracking
- Detailed reporting

**Strengths**:
- Free and open source
- Active development
- Good reporting
- Easy deployment

**Considerations**:
- Self-hosted only
- Limited template library
- Basic evasion

**Government Use Case**: Awareness testing, phishing resilience measurement.

---

#### King Phisher

**Description**: Phishing campaign toolkit with advanced features.

| Aspect | Details |
|--------|---------|
| **Type** | Open source |
| **Features** | Templates, SPF bypass, tracking |
| **Reporting** | Campaign analytics |

**Strengths**:
- Comprehensive features
- Email authentication support
- Free

---

#### Evilginx2

**Description**: Advanced phishing framework with MFA bypass capability.

| Aspect | Details |
|--------|---------|
| **Type** | Open source |
| **Capability** | Man-in-the-middle phishing, session capture |
| **MFA** | Captures session tokens, bypasses MFA |

**Strengths**:
- MFA bypass testing
- Session capture
- Active development

**Considerations**:
- Advanced technique
- Requires careful scoping
- May capture real credentials

**Government Use Case**: Testing MFA effectiveness, advanced phishing resilience.

---

### Voice Phishing (Vishing)

| Platform | Capability | Notes |
|----------|------------|-------|
| **Custom scripts** | Tailored scenarios | Most effective |
| **VoIP services** | Caller ID spoofing | Legal considerations |
| **AI voice** | Voice cloning | Emerging capability |

**Vishing Considerations**:
- Singapore has seen 1,600%+ increase in vishing (Q1 2025)
- Deepfake voice is now accessible
- Legal restrictions on caller ID spoofing

---

### SMS Phishing (Smishing)

| Consideration | Details |
|---------------|---------|
| **Sender ID** | Regulations on SMS sender ID spoofing |
| **Carrier blocks** | Messages may be filtered |
| **Legal** | Singapore has strict SMS regulations |

---

### Social Engineering Pretext Development

| Pretext Category | Examples | Effectiveness |
|------------------|----------|---------------|
| **IT Support** | Password reset, system update | High |
| **Executive** | CEO request, urgent matter | High |
| **Vendor** | Invoice, delivery notification | Moderate |
| **Government** | IRAS, CPF notification | High (but sensitive) |

**Singapore-Specific Considerations**:
- Government agency impersonation is particularly sensitive
- SingPass-related pretexts require careful authorization
- Banking pretexts should be coordinated with MAS awareness

---

## Operational Security

### Communication Security

| Channel | Use Case | Implementation |
|---------|----------|----------------|
| **Team chat** | Day-to-day coordination | Encrypted (Signal, Matrix) |
| **Voice** | Real-time coordination | End-to-end encrypted |
| **File sharing** | Report drafts, evidence | Encrypted storage |
| **Email** | Formal communication | Encrypted (PGP/S-MIME) |

### Evidence Handling

| Evidence Type | Handling Requirement |
|---------------|---------------------|
| **Screenshots** | Timestamp, context documentation |
| **Logs** | Secure storage, hash verification |
| **Credentials** | Report immediately, do not retain |
| **Data samples** | Minimum necessary, anonymize |

### Attribution Prevention

| Measure | Implementation |
|---------|----------------|
| **Infrastructure separation** | No links to organization |
| **Clean systems** | Dedicated testing systems |
| **Network separation** | Separate internet egress |
| **Identity separation** | Separate accounts, personas |

---

## Legal and Ethical Boundaries

### Authorization Requirements

| Element | Requirement |
|---------|-------------|
| **Written scope** | Specific systems, networks, timeframes |
| **Rules of engagement** | Permitted techniques, boundaries |
| **Emergency contacts** | 24/7 availability |
| **Legal review** | Counsel sign-off |
| **Executive approval** | Senior management authorization |

### Singapore Legal Framework

#### Computer Misuse Act Compliance

| Provision | Requirement |
|-----------|-------------|
| Section 3 | Authorization for access |
| Section 4 | Clear intent documentation |
| Section 5 | Scope must specify modifications |
| Section 6 | Interception authorization |

#### Personal Data Protection Act

| Requirement | Implementation |
|-------------|----------------|
| Data minimization | Capture only necessary data |
| Security | Protect any captured data |
| Disposal | Secure deletion post-engagement |
| Consent | Implied through authorization |

### Ethical Guidelines

1. **Never exceed scope** - Stay within authorized boundaries
2. **Report critical findings immediately** - Don't wait for report
3. **Protect discovered data** - Handle PII with care
4. **No collateral damage** - Avoid impacting non-targets
5. **Document everything** - Maintain complete records
6. **Deconflict** - Coordinate with blue team when appropriate

---

## Infrastructure Lifecycle Management

### Setup Phase

| Step | Duration | Activities |
|------|----------|------------|
| 1 | Week 1 | Acquire domains, let age |
| 2 | Week 2-3 | Provision infrastructure |
| 3 | Week 3-4 | Configure redirectors |
| 4 | Week 4 | Deploy team servers |
| 5 | Pre-engagement | Test infrastructure |

### Operational Phase

| Activity | Frequency | Purpose |
|----------|-----------|---------|
| **Health checks** | Daily | Ensure infrastructure operational |
| **Log review** | Daily | Monitor for issues |
| **Rotation planning** | Weekly | Plan infrastructure changes |
| **Backup** | Daily | Maintain operational continuity |

### Tear-Down Phase

| Step | Activities |
|------|------------|
| 1 | Remove implants from target environment |
| 2 | Collect final evidence and logs |
| 3 | Destroy redirectors |
| 4 | Archive team server data (encrypted) |
| 5 | Release domains (after aging) |
| 6 | Document lessons learned |

### Infrastructure Inventory Template

| Component | Provider | IP/Domain | Purpose | Status | Burn Date |
|-----------|----------|-----------|---------|--------|-----------|
| Redirector 1 | Provider A | x.x.x.x | HTTP C2 | Active | +7 days |
| Redirector 2 | Provider B | x.x.x.x | DNS C2 | Active | +14 days |
| Team Server | Provider C | Internal | Primary | Active | End of engagement |
| Domain 1 | Registrar A | example.com | Phishing | Active | +30 days |

---

## Recommendations for Government Red Team

### Initial Capability Build

| Phase | Duration | Focus |
|-------|----------|-------|
| **Phase 1** | 3-6 months | Core C2 capability (Cobalt Strike/Mythic) |
| **Phase 2** | 6-12 months | Infrastructure automation, phishing platform |
| **Phase 3** | 12-18 months | Advanced evasion, custom tooling |
| **Phase 4** | 18-24 months | APT emulation capability |

### Tool Recommendations by Maturity

| Maturity Level | C2 | Phishing | Infrastructure |
|----------------|-----|----------|----------------|
| **Initial** | Mythic/Sliver | Gophish | Manual setup |
| **Developing** | Cobalt Strike | Gophish + Evilginx | Semi-automated |
| **Advanced** | Cobalt Strike + Custom | Custom platforms | Fully automated |
| **Expert** | Custom + Multiple | Custom | Infrastructure-as-Code |

---

## Sources

- [MITRE ATT&CK Techniques](https://attack.mitre.org/)
- [Cobalt Strike Documentation](https://www.cobaltstrike.com/documentation)
- [Mythic Documentation](https://docs.mythic-c2.net/)
- [Sliver Wiki](https://github.com/BishopFox/sliver/wiki)
- [Singapore Computer Misuse Act](https://sso.agc.gov.sg/Act/CMA1993)
- [Singapore PDPA](https://www.pdpc.gov.sg/overview-of-pdpa)
- [Red Team Infrastructure Wiki](https://github.com/bluscreenofjeff/Red-Team-Infrastructure-Wiki)

---

*Return to [Offensive Solutions Overview](./README.md)*
