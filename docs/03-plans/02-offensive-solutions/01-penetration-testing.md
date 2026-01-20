# Penetration Testing Platforms

> Comprehensive documentation of penetration testing tools, platforms, and methodologies for authorized security testing operations.

**Last Updated**: January 2026

---

## Table of Contents

1. [Automated Penetration Testing](#automated-penetration-testing)
2. [Vulnerability Scanning Solutions](#vulnerability-scanning-solutions)
3. [Web Application Testing](#web-application-testing)
4. [Network Penetration Testing](#network-penetration-testing)
5. [Mobile and IoT Testing](#mobile-and-iot-testing)
6. [AI-Enhanced Testing Tools](#ai-enhanced-testing-tools)
7. [Testing Methodology](#testing-methodology)
8. [Platform Selection Guide](#platform-selection-guide)

---

## Automated Penetration Testing

### Overview

Automated penetration testing platforms provide continuous, scalable security assessment capabilities. These tools reduce manual effort while increasing testing coverage and consistency.

### Enterprise Platforms

#### Pentera (Automated Security Validation)

**Description**: Automated Security Validation platform that safely emulates real-world attacks.

| Aspect | Details |
|--------|---------|
| **Capabilities** | Network attacks, credential attacks, lateral movement, ransomware simulation |
| **Deployment** | On-premises or cloud |
| **MITRE ATT&CK Coverage** | Comprehensive TTP mapping |
| **Automation Level** | Fully automated with safe exploitation |
| **Reporting** | Executive and technical reports, remediation guidance |

**Strengths**:
- Safe, production-environment testing
- Continuous validation capability
- No agents required
- Detailed remediation prioritization

**Considerations**:
- Enterprise pricing
- Requires network access configuration
- May require tuning for OT environments

**Government Use Case**: Continuous validation of CII sector defenses, IM8 compliance testing.

---

#### Picus Security

**Description**: Security Control Validation platform using attack simulation.

| Aspect | Details |
|--------|---------|
| **Capabilities** | Attack simulation, security control validation, threat exposure |
| **Integration** | SIEM, SOAR, EDR integration |
| **Coverage** | Network, endpoint, email, web security controls |
| **Automation** | Continuous automated testing |

**Strengths**:
- Validates existing security investments
- Maps to MITRE ATT&CK
- Integration with security stack

**Considerations**:
- Requires sensor deployment
- Dependent on integration quality

**Government Use Case**: Validating CSA guidelines implementation, measuring control effectiveness.

---

#### Horizon3.ai (NodeZero)

**Description**: Autonomous penetration testing platform with AI-driven attack paths.

| Aspect | Details |
|--------|---------|
| **Capabilities** | Autonomous attack path discovery, credential verification, Active Directory attacks |
| **Deployment** | SaaS-based |
| **Frequency** | On-demand or scheduled continuous testing |
| **Coverage** | Internal and external networks |

**Strengths**:
- True autonomous operation
- Discovers real attack paths
- Validates actual exploitability
- No false positives (only verified attacks)

**Considerations**:
- Cloud-based (data sovereignty considerations)
- May trigger security alerts

**Government Use Case**: Validating actual exploitability versus theoretical vulnerabilities.

---

#### AttackIQ

**Description**: Breach and Attack Simulation (BAS) platform aligned with MITRE ATT&CK.

| Aspect | Details |
|--------|---------|
| **Capabilities** | Attack simulation, control validation, purple team automation |
| **Framework Alignment** | MITRE ATT&CK primary focus |
| **Integration** | Extensive security stack integration |
| **Reporting** | Risk-based prioritization |

**Strengths**:
- Deep MITRE ATT&CK integration
- Purple team automation
- Threat-informed defense validation

**Considerations**:
- Requires strategic deployment planning
- Training investment for full utilization

**Government Use Case**: MITRE ATT&CK coverage mapping, Exercise Cyber Star preparation.

---

### Comparison Matrix

| Platform | Automation Level | MITRE Coverage | OT Support | Singapore Data Residency |
|----------|-----------------|----------------|------------|-------------------------|
| Pentera | Full | Comprehensive | Limited | On-premises option |
| Picus | Full | Comprehensive | Limited | Agent-based |
| Horizon3 NodeZero | Full | High | Limited | Cloud (US-based) |
| AttackIQ | Configurable | Primary focus | Limited | Agent-based |

---

## Vulnerability Scanning Solutions

### Network Vulnerability Scanners

#### Tenable Nessus / Tenable.io

**Description**: Industry-standard vulnerability scanner with extensive plugin library.

| Aspect | Details |
|--------|---------|
| **Coverage** | 80,000+ plugins, continuous updates |
| **Deployment** | On-premises (Nessus Pro) or Cloud (Tenable.io) |
| **Compliance** | PCI DSS, HIPAA, CIS benchmarks |
| **Credentials** | Authenticated and unauthenticated scanning |

**Strengths**:
- Largest vulnerability coverage
- Compliance-focused scanning profiles
- Well-established in government sector
- Active community and research

**Considerations**:
- License costs scale with assets
- Requires tuning to reduce false positives

**Government Use Case**: IM8 compliance scanning, CII vulnerability assessment.

---

#### Qualys VMDR

**Description**: Vulnerability Management, Detection, and Response platform.

| Aspect | Details |
|--------|---------|
| **Capabilities** | VM, asset inventory, patch management, threat prioritization |
| **Deployment** | Cloud-native platform |
| **Coverage** | IT, OT, containers, cloud |
| **Prioritization** | Threat intelligence-driven CVSS enhancement |

**Strengths**:
- Unified platform approach
- Cloud-native architecture
- OT scanning capabilities
- Real-time threat context

**Considerations**:
- Cloud dependency
- Module-based pricing complexity

**Government Use Case**: Cross-sector vulnerability management, OT/IT convergence visibility.

---

#### Rapid7 InsightVM

**Description**: Vulnerability management with live monitoring and remediation tracking.

| Aspect | Details |
|--------|---------|
| **Capabilities** | Live vulnerability monitoring, container scanning, cloud assessment |
| **Dashboard** | Real-time visibility and trending |
| **Integration** | SIEM, ticketing, orchestration |
| **Risk Scoring** | Real Risk Score (combines CVSS with threat intelligence) |

**Strengths**:
- Live dashboard and alerting
- Strong integration ecosystem
- Remediation project tracking
- Container security

**Considerations**:
- Console performance at scale
- Learning curve for advanced features

**Government Use Case**: Real-time vulnerability posture monitoring, patch validation.

---

### Specialized Scanners

#### Nuclei (ProjectDiscovery)

**Description**: Fast, customizable vulnerability scanner based on YAML templates.

| Aspect | Details |
|--------|---------|
| **Type** | Open source |
| **Templates** | 8,000+ community templates |
| **Speed** | Highly parallelized scanning |
| **Customization** | YAML-based template creation |

**Strengths**:
- Extremely fast
- Highly customizable
- Active community
- Free and open source

**Considerations**:
- Requires template management
- May need tuning for accuracy

**Government Use Case**: Custom vulnerability checks, rapid assessment of emerging threats.

---

#### OpenVAS (Greenbone)

**Description**: Open-source vulnerability assessment system.

| Aspect | Details |
|--------|---------|
| **Type** | Open source (community) / Commercial (Greenbone) |
| **Coverage** | 100,000+ Network Vulnerability Tests (NVTs) |
| **Deployment** | On-premises |
| **Compliance** | PCI DSS, ISO 27001 support |

**Strengths**:
- Open source flexibility
- Large test database
- On-premises control
- No licensing costs (community version)

**Considerations**:
- Higher maintenance burden
- Performance optimization required
- Community support only (free version)

**Government Use Case**: Cost-effective scanning, air-gapped environment support.

---

## Web Application Testing

### Dynamic Application Security Testing (DAST)

#### Burp Suite Professional

**Description**: Industry-standard web application security testing toolkit.

| Aspect | Details |
|--------|---------|
| **Capabilities** | Automated scanning, manual testing, API testing |
| **Extensibility** | BApp Store with extensive extensions |
| **Collaboration** | Burp Collaborator for out-of-band testing |
| **Coverage** | OWASP Top 10, advanced vulnerabilities |

**OWASP Top 10:2025 Coverage**:

| OWASP 2025 | Burp Detection Capability |
|------------|--------------------------|
| A01: Broken Access Control | Strong (BOLA, IDOR, privilege escalation) |
| A02: Security Misconfiguration | Strong |
| A03: Supply Chain Failures | Limited (dependency scanning separate) |
| A04: Cryptographic Failures | Moderate |
| A05: Injection | Strong (SQLi, XSS, command injection) |
| A06: Insecure Design | Manual testing required |
| A07: Authentication Failures | Strong |
| A08: Software/Data Integrity | Moderate |
| A09: Logging Failures | Limited |
| A10: Exceptional Conditions | Moderate |

**Strengths**:
- Gold standard for web testing
- Excellent manual testing support
- Extensive extension ecosystem
- Active research and updates

**Considerations**:
- Per-user licensing
- Steep learning curve for advanced features
- Enterprise features require separate product

**Government Use Case**: Web application assessment, GBBP preparation, IM8 compliance.

---

#### OWASP ZAP (Zed Attack Proxy)

**Description**: Free, open-source web application security scanner.

| Aspect | Details |
|--------|---------|
| **Type** | Open source |
| **Capabilities** | Automated scanning, active/passive scanning, API testing |
| **Automation** | CI/CD integration, command-line operation |
| **Community** | Large active community |

**Strengths**:
- Free and open source
- CI/CD friendly
- Active development
- Excellent for automation

**Considerations**:
- Detection rate lower than commercial tools
- Manual testing less polished
- Enterprise features limited

**Government Use Case**: DevSecOps integration, automated pipeline scanning, training.

---

#### Invicti (formerly Netsparker)

**Description**: Enterprise web application security scanner with proof-based scanning.

| Aspect | Details |
|--------|---------|
| **Capabilities** | Automated scanning, proof-based detection, API scanning |
| **False Positives** | Very low due to proof-based approach |
| **Coverage** | Modern frameworks, SPAs, APIs |
| **Reporting** | Compliance mapping, remediation guidance |

**Strengths**:
- Extremely low false positives
- Excellent modern application support
- Proof of exploit for findings
- Strong API coverage

**Considerations**:
- Premium pricing
- May miss some edge cases
- Requires proper configuration

**Government Use Case**: High-accuracy scanning where manual verification is costly.

---

#### Acunetix

**Description**: Automated web vulnerability scanner with network scanning capability.

| Aspect | Details |
|--------|---------|
| **Capabilities** | Web scanning, network perimeter, API testing |
| **Speed** | Fast scanning engine |
| **Coverage** | 7,000+ vulnerability checks |
| **Integration** | WAF, issue trackers, CI/CD |

**Strengths**:
- Fast scanning
- Good detection rate
- Combined web/network
- Reasonable pricing

**Considerations**:
- Some false positives
- Manual testing features limited
- Less extensible than Burp

**Government Use Case**: Rapid web application assessment, continuous monitoring.

---

### Static Application Security Testing (SAST)

#### Checkmarx SAST

**Description**: Enterprise static application security testing platform.

| Aspect | Details |
|--------|---------|
| **Languages** | 25+ programming languages |
| **Integration** | IDE, CI/CD, repositories |
| **Coverage** | OWASP Top 10, SANS 25, CWE |
| **Remediation** | Best fix location, developer guidance |

**Strengths**:
- Comprehensive language support
- Strong remediation guidance
- Developer-friendly workflows
- Enterprise scalability

**Considerations**:
- Complex setup
- Tuning required for accuracy
- Premium pricing

---

#### SonarQube (Community/Enterprise)

**Description**: Continuous code quality and security platform.

| Aspect | Details |
|--------|---------|
| **Type** | Open source (Community) / Commercial (Enterprise) |
| **Capabilities** | Code quality, security vulnerabilities, code smells |
| **Integration** | CI/CD native integration |
| **Coverage** | Multiple languages, security hotspots |

**Strengths**:
- Strong code quality integration
- DevOps native
- Good security coverage (Enterprise)
- Developer adoption

**Considerations**:
- Security depth varies by language
- Enterprise features require license

---

### API Security Testing

#### Postman

**Description**: API development and testing platform with security testing capabilities.

| Aspect | Details |
|--------|---------|
| **Capabilities** | API testing, automated tests, security checks |
| **Collaboration** | Team workspaces, shared collections |
| **Automation** | Newman CLI, CI/CD integration |

**Strengths**:
- Developer-friendly
- Excellent collaboration
- Wide adoption
- Free tier available

**Considerations**:
- Security testing not primary focus
- Requires manual security test creation

---

#### OWASP API Security Testing Guide

Reference for API security testing coverage:

| OWASP API Top 10 2023 | Testing Approach |
|----------------------|------------------|
| API1: Broken Object Level Authorization | BOLA testing, IDOR enumeration |
| API2: Broken Authentication | Token analysis, session management |
| API3: Broken Object Property Level Authorization | Mass assignment testing |
| API4: Unrestricted Resource Consumption | Rate limiting, DoS testing |
| API5: Broken Function Level Authorization | Privilege escalation testing |
| API6: Unrestricted Access to Sensitive Business Flows | Business logic testing |
| API7: Server-Side Request Forgery | SSRF exploitation |
| API8: Security Misconfiguration | Configuration review |
| API9: Improper Inventory Management | API discovery, shadow APIs |
| API10: Unsafe Consumption of APIs | Third-party API security |

---

## Network Penetration Testing

### Core Testing Frameworks

#### Metasploit Framework

**Description**: Industry-standard penetration testing framework.

| Aspect | Details |
|--------|---------|
| **Type** | Open source (Community) / Commercial (Pro) |
| **Modules** | 2,000+ exploits, 1,000+ auxiliary modules |
| **Post-Exploitation** | Meterpreter, credential harvesting, pivoting |
| **Reporting** | Automated reporting (Pro) |

**Strengths**:
- Comprehensive exploit database
- Strong post-exploitation
- Active community
- Industry standard

**Considerations**:
- Detectable by most security tools
- Pro version required for automation
- Requires skilled operators

**Government Use Case**: Exploitation validation, post-exploitation testing, training.

---

#### Cobalt Strike

**Description**: Adversary simulation and red team operations platform.

| Aspect | Details |
|--------|---------|
| **Capabilities** | Beacon payload, C2 infrastructure, post-exploitation |
| **Malleable C2** | Customizable traffic profiles |
| **Teamserver** | Multi-operator collaboration |
| **Reporting** | Comprehensive engagement reporting |

**Strengths**:
- Industry-leading red team tool
- Highly customizable
- Excellent collaboration features
- Mature operational features

**Considerations**:
- Premium pricing
- Heavily targeted by EDR vendors
- Requires expertise to evade detection

**Government Use Case**: Advanced red team operations, APT emulation.

---

#### Nmap

**Description**: Network discovery and security auditing tool.

| Aspect | Details |
|--------|---------|
| **Type** | Open source |
| **Capabilities** | Port scanning, service detection, OS fingerprinting |
| **Scripting** | NSE (Nmap Scripting Engine) |
| **Speed** | Highly optimized scanning |

**Strengths**:
- Essential reconnaissance tool
- Extremely versatile
- Active development
- Comprehensive documentation

**Considerations**:
- Aggressive scans may cause issues
- Requires interpretation skill

**Government Use Case**: Network reconnaissance, asset discovery, service enumeration.

---

### Active Directory Testing

#### BloodHound

**Description**: Active Directory attack path analysis tool.

| Aspect | Details |
|--------|---------|
| **Type** | Open source (Community) / Commercial (Enterprise) |
| **Capabilities** | Attack path visualization, privilege escalation paths |
| **Collection** | SharpHound, AzureHound collectors |
| **Analysis** | Graph-based relationship analysis |

**Strengths**:
- Visual attack path identification
- Identifies non-obvious paths
- Azure AD support
- Essential for AD testing

**Considerations**:
- Collection may be detected
- Requires AD access
- Graph database management

**Government Use Case**: Active Directory security assessment, privilege escalation testing.

---

#### Impacket

**Description**: Collection of Python classes for working with network protocols.

| Aspect | Details |
|--------|---------|
| **Type** | Open source |
| **Protocols** | SMB, MSRPC, Kerberos, LDAP, MSSQL |
| **Tools** | secretsdump, psexec, wmiexec, etc. |
| **Integration** | Commonly used with other tools |

**Strengths**:
- Protocol implementation reference
- Powerful toolset
- Scriptable
- Active development

**Considerations**:
- Command-line only
- Requires networking knowledge
- May trigger alerts

**Government Use Case**: Windows network attacks, credential extraction, lateral movement.

---

### Wireless Testing

#### Aircrack-ng Suite

**Description**: Complete suite of tools for WiFi security assessment.

| Aspect | Details |
|--------|---------|
| **Capabilities** | Monitoring, attacking, testing, cracking |
| **Protocols** | WEP, WPA/WPA2/WPA3, 802.1x |
| **Hardware** | Requires compatible wireless adapters |

**Strengths**:
- Comprehensive wireless toolkit
- Well-documented
- Active community
- Free and open source

**Considerations**:
- Hardware dependent
- Legal restrictions in many jurisdictions
- Requires physical proximity

**Government Use Case**: Wireless security assessment, rogue AP detection.

---

## Mobile and IoT Testing

### Mobile Application Testing

#### MobSF (Mobile Security Framework)

**Description**: Automated mobile application security testing framework.

| Aspect | Details |
|--------|---------|
| **Type** | Open source |
| **Platforms** | Android, iOS, Windows Mobile |
| **Testing** | Static analysis, dynamic analysis |
| **Coverage** | OWASP Mobile Top 10 |

**Strengths**:
- Automated analysis
- Comprehensive reports
- Both static and dynamic
- Free and open source

**Considerations**:
- Setup complexity
- Dynamic analysis requires device/emulator
- May miss complex vulnerabilities

**Government Use Case**: Government app security assessment, SingPass app validation.

---

#### Frida

**Description**: Dynamic instrumentation toolkit for mobile and desktop apps.

| Aspect | Details |
|--------|---------|
| **Type** | Open source |
| **Platforms** | Android, iOS, Windows, macOS, Linux |
| **Capabilities** | Runtime instrumentation, hooking, tracing |
| **Scripting** | JavaScript-based |

**Strengths**:
- Extremely powerful
- Cross-platform
- Active development
- Scriptable

**Considerations**:
- Steep learning curve
- Requires rooted/jailbroken devices
- Detection mechanisms exist

**Government Use Case**: Deep mobile app analysis, runtime manipulation testing.

---

### IoT Testing

#### IoT Testing Methodology (OWASP IoT)

Key testing areas aligned with OWASP IoT Top 10:

| OWASP IoT Top 10 | Testing Approach |
|------------------|------------------|
| I1: Weak/Hardcoded Passwords | Credential testing, default password checks |
| I2: Insecure Network Services | Network scanning, service enumeration |
| I3: Insecure Ecosystem Interfaces | API testing, cloud interface review |
| I4: Lack of Secure Update | Firmware analysis, update mechanism testing |
| I5: Insecure/Outdated Components | Component analysis, CVE mapping |
| I6: Insufficient Privacy Protection | Data flow analysis, storage review |
| I7: Insecure Data Transfer | Protocol analysis, encryption testing |
| I8: Lack of Device Management | Management interface assessment |
| I9: Insecure Default Settings | Configuration review |
| I10: Lack of Physical Hardening | Physical security testing |

---

#### IoT Testing Tools

| Tool | Purpose | Type |
|------|---------|------|
| **Binwalk** | Firmware analysis | Open source |
| **Firmwalker** | Firmware file system analysis | Open source |
| **EMBA** | Embedded firmware analyzer | Open source |
| **RouterSploit** | Router exploitation | Open source |
| **Expliot** | IoT exploitation framework | Open source |

**Government Use Case**: Smart Nation device assessment, CSA IoT labelling validation.

---

## AI-Enhanced Testing Tools

### Overview

AI and LLM integration is transforming penetration testing capabilities. These tools leverage machine learning to automate complex tasks, improve accuracy, and scale testing operations.

### AI-Powered Platforms

#### Hexstrike AI

**Description**: AI-driven platform bridging LLMs with offensive security tools.

| Aspect | Details |
|--------|---------|
| **Capabilities** | Autonomous tool orchestration, 150+ security tools |
| **AI Integration** | MCP Agents connecting LLMs to security tools |
| **Automation** | Tasks completing in minutes vs. hours/days |
| **Scale** | Thousands of IPs simultaneously |

**Reference**: Research documented in [AI Offensive Use](/docs/01-research/04-ai-impact/01-ai-offensive-use.md#hexstrike-ai)

**Considerations**:
- Emerging technology
- Requires oversight
- May produce unexpected results

---

#### XBOW

**Description**: AI-powered autonomous penetration testing platform.

| Aspect | Details |
|--------|---------|
| **Capabilities** | Vulnerability discovery, validation, exploitation |
| **Automation** | Hundreds of parallel AI agents |
| **Operation** | Minimal human intervention |
| **Validation** | Automated exploit confirmation |

**Considerations**:
- Cutting-edge technology
- Requires careful scoping
- Results validation still important

---

#### PenTest++

**Description**: AI-augmented security testing system with generative AI integration.

| Aspect | Details |
|--------|---------|
| **Capabilities** | Reconnaissance, scanning, enumeration, exploitation |
| **Automation** | Ethical hacking workflow automation |
| **Documentation** | Automated report generation |

---

### AI Integration Strategies

| Strategy | Application | Benefit |
|----------|-------------|---------|
| **Reconnaissance Automation** | OSINT gathering, target profiling | Scale and speed |
| **Vulnerability Correlation** | Cross-referencing findings | Reduced false positives |
| **Exploit Suggestion** | Attack path recommendation | Efficiency |
| **Report Generation** | Documentation automation | Time savings |
| **Pattern Recognition** | Anomaly detection in responses | Coverage |

### Ethical Considerations for AI Tools

1. **Oversight Required**: Human review of AI actions and findings
2. **Scope Enforcement**: Ensure AI stays within authorized boundaries
3. **Output Validation**: Verify AI-generated exploits before use
4. **Attribution**: Clear logging of AI-assisted activities
5. **Responsible Use**: Align with CSA AI security guidelines

---

## Testing Methodology

### Penetration Testing Execution Standard (PTES)

Recommended methodology aligned with industry standards:

#### Phase 1: Pre-Engagement

| Activity | Deliverable |
|----------|-------------|
| Scope definition | Written scope document |
| Rules of engagement | Signed RoE |
| Authorization | Legal authorization documentation |
| Emergency contacts | Contact list |
| Timeline agreement | Schedule |

#### Phase 2: Intelligence Gathering

| Activity | Tools/Techniques |
|----------|------------------|
| OSINT | TheHarvester, Maltego, Shodan |
| DNS enumeration | Amass, DNSRecon |
| Network mapping | Nmap, Masscan |
| Technology fingerprinting | Wappalyzer, BuiltWith |

#### Phase 3: Threat Modeling

| Activity | Output |
|----------|--------|
| Attack surface mapping | Asset inventory |
| Threat identification | Potential attack vectors |
| Risk prioritization | Testing priority list |

#### Phase 4: Vulnerability Analysis

| Activity | Tools |
|----------|-------|
| Automated scanning | Nessus, Qualys |
| Manual verification | Burp Suite, manual testing |
| Configuration review | CIS benchmarks |

#### Phase 5: Exploitation

| Activity | Considerations |
|----------|---------------|
| Exploit selection | Reliability, safety |
| Exploitation attempt | Documented methodology |
| Evidence collection | Screenshots, logs |

#### Phase 6: Post-Exploitation

| Activity | Purpose |
|----------|---------|
| Privilege escalation | Assess further access |
| Lateral movement | Test network segmentation |
| Data access | Validate data protection |
| Persistence | Test detection capabilities |

#### Phase 7: Reporting

| Component | Content |
|-----------|---------|
| Executive summary | Business impact, key findings |
| Technical findings | Detailed vulnerability descriptions |
| Evidence | Screenshots, logs, PoC |
| Recommendations | Prioritized remediation |
| Risk ratings | CVSS, business context |

---

## Platform Selection Guide

### Selection Criteria

| Criterion | Weight | Considerations |
|-----------|--------|----------------|
| **Capability Coverage** | High | Does it meet testing requirements? |
| **Singapore Data Residency** | High | Can data stay in Singapore? |
| **Integration** | Medium | Works with existing tools? |
| **Automation** | Medium | Supports continuous testing? |
| **Licensing Cost** | Medium | Budget alignment? |
| **Support Quality** | Medium | Vendor responsiveness? |
| **OT Capability** | Varies | OT sector requirements? |

### Recommended Stack by Use Case

#### Standard IT Penetration Testing

| Layer | Recommended Tools |
|-------|-------------------|
| Vulnerability Scanning | Tenable.io or Qualys |
| Web Application | Burp Suite Professional + Invicti |
| Network Testing | Nmap + Metasploit + BloodHound |
| Automation | Nuclei + Custom scripts |

#### Continuous Security Validation

| Layer | Recommended Tools |
|-------|-------------------|
| BAS Platform | Pentera or AttackIQ |
| Vulnerability Management | Tenable.io or Rapid7 |
| Web Continuous | Invicti + OWASP ZAP (CI/CD) |

#### Red Team Operations

| Layer | Recommended Tools |
|-------|-------------------|
| C2 Framework | Cobalt Strike or Mythic |
| Exploitation | Custom + Metasploit |
| AD Attacks | BloodHound + Impacket |
| Evasion | Custom tooling |

#### OT/ICS Testing

| Layer | Recommended Tools |
|-------|-------------------|
| Asset Discovery | Specialized OT scanners |
| Vulnerability Assessment | Dragos, Claroty (OT-specific) |
| Protocol Testing | Custom + Metasploit ICS modules |

---

## Procurement Considerations

### Licensing Models

| Model | Platforms | Considerations |
|-------|-----------|----------------|
| Per-asset | Tenable, Qualys | Scales with environment |
| Per-user | Burp Suite, Cobalt Strike | Team size dependent |
| Subscription | Most SaaS platforms | Annual commitment |
| Perpetual | Some on-premises tools | Upfront cost |

### Government Procurement Alignment

- **GeBIZ compliance**: Verify vendor registration
- **Data residency**: Confirm Singapore data storage options
- **Support hours**: Ensure Singapore timezone support
- **Security clearance**: Verify vendor personnel clearance if required

---

## Sources

- [PTES - Penetration Testing Execution Standard](http://www.pentest-standard.org/)
- [OWASP Top 10:2025](https://owasp.org/Top10/)
- [OWASP API Security Top 10](https://owasp.org/API-Security/)
- [OWASP Mobile Security Testing Guide](https://owasp.org/www-project-mobile-security-testing-guide/)
- [MITRE ATT&CK v18](https://attack.mitre.org/)
- [CIS Benchmarks](https://www.cisecurity.org/cis-benchmarks)
- [AI Offensive Use Research](/docs/01-research/04-ai-impact/01-ai-offensive-use.md)

---

*Return to [Offensive Solutions Overview](./README.md)*
