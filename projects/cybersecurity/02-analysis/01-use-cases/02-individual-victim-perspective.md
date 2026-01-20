# Individual Victim Perspective

> Understanding how individuals are targeted, attacked, and impacted by cyber threats
>
> Last Updated: January 2026

---

## Table of Contents

1. [Individual Threat Landscape](#individual-threat-landscape)
2. [Phishing and Social Engineering Scenarios](#phishing-and-social-engineering-scenarios)
3. [Identity Theft Use-Cases](#identity-theft-use-cases)
4. [Financial Fraud Scenarios](#financial-fraud-scenarios)
5. [Online Scam Scenarios](#online-scam-scenarios)
6. [Privacy Violation Use-Cases](#privacy-violation-use-cases)
7. [Impact Assessment for Individuals](#impact-assessment-for-individuals)
8. [Consumer Protection Challenges](#consumer-protection-challenges)
9. [Singapore Individual Context](#singapore-individual-context)

---

## Individual Threat Landscape

### Personal Cyber Threat Statistics (2024-2025)

| Threat Category | Global Scale | Singapore Context |
|-----------------|--------------|-------------------|
| **Phishing Attempts** | 1.13M per quarter | 6,100+ cases reported |
| **Identity Theft** | 65% of dark web crime | Primary concern |
| **Online Scams** | $10B+ annual losses globally | S$1.1B losses |
| **Credential Theft** | 15B credentials on dark web | Significant exposure |
| **Deepfake Fraud** | 62% organizations targeted | Emerging consumer threat |

### Who Gets Targeted?

**High-Risk Individual Profiles**:

| Profile | Risk Level | Primary Threats | Attack Vectors |
|---------|------------|-----------------|----------------|
| **Seniors (65+)** | Very High | Romance scams, tech support fraud | Phone, social media |
| **Young Professionals** | High | Job scams, investment fraud | LinkedIn, messaging apps |
| **Active Social Media Users** | High | Phishing, account takeover | Social platforms |
| **Online Shoppers** | Medium-High | E-commerce fraud, card theft | Fake sites, phishing |
| **Remote Workers** | Medium-High | Phishing, credential theft | Email, VPN |
| **Cryptocurrency Users** | High | Investment scams, wallet theft | DeFi platforms, social |

---

## Phishing and Social Engineering Scenarios

### Use-Case P1: Banking Credential Phishing

**Scenario Profile**:
- **Target**: Banking customers (mass targeting)
- **Threat Actor**: Cybercriminal group
- **Attack Vector**: SMS phishing (smishing)
- **Objective**: Online banking credential theft

**Attack Flow**:

```
SMS Received
"Dear customer, your DBS account has been suspended due to
unusual activity. Verify now: https://dbs-secure.sg-verify.com"
      │
      ▼
Victim Clicks Link
├── Professional-looking login page
├── Bank branding copied exactly
├── SSL certificate (appears "secure")
└── Mobile-optimized design
      │
      ▼
Credentials Entered
├── Username/NRIC captured
├── Password captured
├── Redirected to real bank site
└── Victim may not notice
      │
      ▼
Account Takeover
├── Attacker logs into real account
├── Money transferred to mule accounts
├── OTP interception (if SIM swapped)
└── Account drained within minutes
```

**Why This Works**:
- Bank branding creates trust
- Urgency ("suspended") triggers emotional response
- SMS feels more legitimate than email
- Link uses convincing domain name
- Mobile screens hide full URL

**Singapore Banking Phishing Statistics (2024)**:
- Banking sector: 63% of all phishing attempts
- SMS-based phishing (smishing) increasing
- Average time from credential theft to fraud: <30 minutes

---

### Use-Case P2: AI-Enhanced Personalized Phishing

**Scenario Profile**:
- **Target**: Specific individual (spear-phishing)
- **Threat Actor**: Sophisticated criminal group
- **Attack Vector**: Email + AI personalization
- **Objective**: High-value credential theft or malware installation

**AI Enhancement Elements**:

```
Target Reconnaissance (AI-Assisted)
├── Social media profile analysis
├── Professional connections mapped
├── Writing style analyzed
├── Interests and activities catalogued
└── Timing patterns identified

Message Generation (LLM-Powered)
├── Perfectly grammatically correct
├── Contextually relevant content
├── Mimics known contact's style
├── References real events/projects
└── Includes personalized details

Attack Execution
├── Email appears from known colleague
├── Discusses real ongoing project
├── Includes malicious attachment or link
├── Follow-up messages if needed
└── Real-time adaptation based on responses
```

**Example Attack Email**:

```
Subject: Re: Q4 Budget Review - Action Required

Hi Sarah,

Following up on our discussion at the team meeting yesterday -
I've attached the updated budget projections you asked about.
Can you review and sign off before Friday? John mentioned
he needs this before the board meeting.

Also, saw your post about the marathon - impressive time!
Hope the knee is feeling better.

Thanks,
Mike

[Budget_Q4_Final_v3.xlsx] (malicious)
```

**Why Traditional Defenses Fail**:
- No spelling/grammar errors to detect
- Context matches victim's real work
- Sender relationship appears legitimate
- Personal details increase trust
- Attachment type appears business-normal

---

### Use-Case P3: Voice Phishing (Vishing)

**Scenario Profile**:
- **Target**: Individual, often elderly
- **Threat Actor**: Scam call center
- **Attack Vector**: Phone call impersonating authority
- **Objective**: Financial theft or credential disclosure

**Common Vishing Scenarios**:

| Scenario | Pretext | Tactics |
|----------|---------|---------|
| **Police Impersonation** | "Your identity was used in crime" | Fear, urgency, authority |
| **Bank Security** | "Suspicious transaction detected" | Concern, verification pretense |
| **Tax Authority** | "Outstanding tax debt, arrest warrant" | Fear, intimidation |
| **Tech Support** | "Your computer has virus" | Technical confusion, trust |
| **Relative in Trouble** | "Grandson arrested, needs bail" | Emotion, urgency |

**Singapore Police Impersonation Attack Flow**:

```
Initial Call
"This is Officer Tan from Singapore Police Force.
Your NRIC was used to open fraudulent bank accounts.
We need to verify your identity."
      │
      ▼
Authority Establishment
├── Badge number provided
├── Case reference number given
├── Threats of arrest/investigation
└── Transfer to "senior officer"
      │
      ▼
Fear and Compliance
├── Victim isolated (told not to tell anyone)
├── Extended call duration (hours)
├── Psychological pressure applied
└── Victim's judgment impaired
      │
      ▼
Financial Extraction
├── "Verify" accounts by transferring money
├── "Temporary" transfer to "safe account"
├── Multiple transactions over time
└── Funds moved through mule network
```

**Victim Psychology**:
- Authority figures command compliance
- Fear overrides rational thinking
- Social isolation prevents outside verification
- Extended duration creates psychological exhaustion
- Gradual escalation normalizes each step

---

### Use-Case P4: QR Code Phishing (Quishing)

**Scenario Profile**:
- **Target**: General public
- **Threat Actor**: Opportunistic criminals
- **Attack Vector**: Malicious QR codes in physical/digital spaces
- **Objective**: Credential theft or payment fraud

**Attack Scenarios**:

```
Physical QR Code Placement
├── Overlay on legitimate payment QR codes
├── Fake parking payment QR codes
├── Restaurant table QR codes replaced
├── Public poster QR codes hijacked
└── Fake delivery notification QR codes

Digital QR Code Attacks
├── QR codes in phishing emails
├── QR codes in text messages
├── QR codes in social media posts
└── QR codes in online advertisements

Victim Scans QR Code
      │
      ▼
Redirected to Malicious Site
├── Credential harvesting page
├── Malware download
├── Payment redirect
└── Account linking scam
```

**Singapore Context**:
- High QR code adoption (payments, check-in, menus)
- PayNow and SGQR widespread usage
- Physical QR code tampering reported
- Public awareness campaigns ongoing

---

## Identity Theft Use-Cases

### Use-Case I1: Full Identity Takeover

**Scenario Profile**:
- **Target**: Individual with good credit history
- **Threat Actor**: Identity theft network
- **Attack Vector**: Data breach + social engineering
- **Objective**: Financial fraud using victim's identity

**Identity Theft Progression**:

```
Data Collection
├── Personal details from breaches
├── NRIC from phishing
├── Address from public records
├── Employment from LinkedIn
└── Family details from social media

Identity Package Assembly
├── Fake IC created
├── Supporting documents forged
├── Credit profile analyzed
└── Target institutions identified

Fraudulent Activity
├── New credit cards opened
├── Loans applied for
├── Mobile phone contracts
├── Bank accounts opened
└── Online accounts created

Discovery (Often Delayed)
├── Credit check reveals unknown accounts
├── Debt collection contacts
├── Unable to open legitimate accounts
└── Investigation reveals fraud
```

**Impact Timeline**:

| Phase | Duration | Victim Experience |
|-------|----------|-------------------|
| **Theft to Use** | Days to weeks | Unaware |
| **Active Fraud** | Weeks to months | Possibly unaware |
| **Discovery** | Months later | Unexpected contacts, denials |
| **Resolution** | 6-18 months | Ongoing stress, effort |
| **Long-term** | Years | Credit impact, vigilance required |

---

### Use-Case I2: SIM Swapping Attack

**Scenario Profile**:
- **Target**: High-value individual (crypto holder, executive)
- **Threat Actor**: Sophisticated criminal / insider
- **Attack Vector**: Telecom social engineering or insider compromise
- **Objective**: Bypass 2FA for account takeover

**Attack Methodology**:

```
Target Selection
├── Crypto wallet activity identified
├── Social media research
├── Phone number identified
└── Mobile carrier determined

SIM Swap Execution
├── Call to carrier's customer service
├── Social engineering with personal details
├── OR insider accomplice at carrier
├── SIM card ported to attacker's device
└── Victim's phone loses service

Account Takeover
├── Password reset initiated
├── 2FA SMS received by attacker
├── Account access gained
├── Cryptocurrency transferred
└── Email access for persistence
```

**Singapore Telecom Protections**:
- SingPass 2FA less reliant on SMS
- Carrier verification procedures improved
- But social engineering still effective
- Insider threat remains

---

### Use-Case I3: Synthetic Identity Fraud

**Scenario Profile**:
- **Target**: Credit system / not a specific individual
- **Threat Actor**: Fraud rings
- **Attack Vector**: Combining real and fake identity elements
- **Objective**: Create "new" identity for fraud

**Synthetic Identity Construction**:

```
Element Gathering
├── Real NRIC (stolen from minor, elderly, deceased)
├── Fake name generated
├── Legitimate address (rented mailbox)
└── Fabricated employment history

Credit Building
├── Authorized user on existing accounts
├── Secured credit card obtained
├── Small credit line managed well
├── Credit score built over months/years

Bust-Out
├── Credit limits increased
├── Multiple accounts maxed out
├── Large purchases made
├── Identity abandoned
└── No real person to pursue
```

**Challenge for Victims**:
- NRIC owners may not know they're victims
- Children's NRICs used (discovered at age 18)
- Deceased persons' identities exploited
- Detection extremely difficult

---

## Financial Fraud Scenarios

### Use-Case F1: Investment Scam

**Scenario Profile**:
- **Target**: Individual seeking investment returns
- **Threat Actor**: Organized scam syndicate
- **Attack Vector**: Social media / dating apps / messaging
- **Objective**: Steal investment funds

**"Pig Butchering" Attack Pattern**:

```
Contact Establishment (Weeks 1-4)
├── "Wrong number" message or dating app match
├── Relationship building (romantic or friendly)
├── Trust developed over time
├── Investment success stories shared casually
└── Victim becomes curious

Investment Introduction (Weeks 4-8)
├── Scammer shows "trading platform" profits
├── Teaches victim to "invest"
├── Small initial investment encouraged
├── Quick "profits" displayed
└── Victim withdrawal processed (builds trust)

Escalation (Weeks 8-16)
├── Larger investments encouraged
├── "Special opportunities" presented
├── Borrowed money invested
├── Family/friends recruited
└── Significant funds committed

Extraction (Final)
├── "Withdrawal problem" - need more funds
├── "Tax payment required"
├── "System error, need deposit"
├── Platform becomes inaccessible
└── Scammer disappears
```

**Singapore Investment Scam Statistics (2024)**:
- Investment scams: Top scam category by amount lost
- Average victim loss: $20,000-$100,000+
- Some victims lose life savings
- Elderly and middle-aged most affected

---

### Use-Case F2: E-commerce Fraud

**Scenario Profile**:
- **Target**: Online shoppers
- **Threat Actor**: Various (fake sellers, payment thieves)
- **Attack Vector**: Fake e-commerce sites / marketplace fraud
- **Objective**: Steal payment information or non-delivery scam

**Fake E-commerce Attack Types**:

| Type | Method | Victim Impact |
|------|--------|---------------|
| **Non-delivery** | Accept payment, never ship | Lose payment amount |
| **Fake Product** | Ship counterfeit/inferior goods | Lose money + receive junk |
| **Card Harvesting** | Collect card details at checkout | Card fraud later |
| **Account Takeover** | Stolen e-commerce account used | Unauthorized purchases |

**Fake Website Indicators** (increasingly difficult to spot):
- Unrealistic prices (too good to be true)
- No physical address or contact
- Payment only by transfer/crypto
- Recently registered domain
- Poor reviews (if any exist)
- Missing HTTPS (but many fake sites now have SSL)

---

### Use-Case F3: Romance Scam

**Scenario Profile**:
- **Target**: Individual seeking companionship
- **Threat Actor**: Scam syndicate (often operating from scam compounds)
- **Attack Vector**: Dating apps, social media
- **Objective**: Emotional manipulation for financial extraction

**Romance Scam Progression**:

```
Phase 1: Love Bombing (Weeks 1-8)
├── Attractive profile (stolen photos)
├── Intense emotional connection
├── Daily communication
├── Future plans discussed
└── Trust and emotional dependency built

Phase 2: Crisis Introduction (Week 8+)
├── Emergency situation arises
├── Can't access own funds
├── Needs temporary help
├── Will "repay immediately"
└── Emotional pressure applied

Phase 3: Ongoing Extraction
├── Crisis after crisis
├── Amounts escalate
├── Excuses for not meeting in person
├── Victim rationalizes continued giving
└── Savings depleted

Phase 4: Discovery
├── Reverse image search reveals stolen photos
├── Friends/family intervention
├── Financial ruin forces acknowledgment
└── Severe emotional trauma
```

**Psychological Impact**:
- Financial loss often secondary to emotional damage
- Shame prevents reporting
- Victims sometimes defend scammer
- Long-term trust issues
- Depression and suicidal ideation reported

---

## Online Scam Scenarios

### Use-Case S1: Job Scam

**Scenario Profile**:
- **Target**: Job seekers
- **Threat Actor**: Scam syndicates
- **Attack Vector**: Job boards, messaging apps, social media
- **Objective**: Steal money, recruit mules, or collect personal data

**Job Scam Variants**:

| Variant | Mechanism | Victim Loss |
|---------|-----------|-------------|
| **Equipment Fee** | Pay for work equipment upfront | Payment amount |
| **Training Fee** | Pay for mandatory training | Fee amount |
| **Task Scam** | Complete tasks, "deposit" required | Escalating deposits |
| **Crypto Task** | "Easy crypto profits", keep investing | Investment amounts |
| **Mule Recruitment** | Legitimate job, actually money laundering | Criminal liability |

**Task/Commission Scam Flow** (Common in Singapore):

```
Recruitment
├── Message on Telegram/WhatsApp
├── Easy money for simple tasks
├── No experience needed
└── Work from home

Initial Tasks
├── Simple tasks (liking videos, reviews)
├── Small commissions paid
├── Trust built
└── Victim engaged

Escalation
├── "Combo tasks" introduced
├── Must invest to unlock higher earnings
├── Deposits required
├── Withdrawals blocked until targets met

Extraction
├── Increasing deposit requirements
├── "System error" blocks withdrawal
├── Admin stops responding
└── Platform disappears
```

---

### Use-Case S2: Technical Support Scam

**Scenario Profile**:
- **Target**: Non-technical users, especially elderly
- **Threat Actor**: Call centers (often overseas)
- **Attack Vector**: Pop-up alerts, cold calls
- **Objective**: Remote access fees, fake software sales

**Tech Support Scam Flow**:

```
Alert Generation
├── Malicious pop-up on browsing
├── "Your computer is infected!"
├── Loud alert sounds
├── Cannot close window easily
└── Phone number to call for "help"

Remote Access
├── Victim calls number
├── Directed to install remote access tool
├── Scammer takes control
├── Fake "diagnostics" run
└── Fake "problems" shown

Payment Extraction
├── Expensive "security software" needed
├── Credit card or gift cards requested
├── Bank account access requested
├── Multiple payments over time
└── Recurring subscription enrolled
```

---

### Use-Case S3: Government Impersonation Scam

**Scenario Profile**:
- **Target**: General public
- **Threat Actor**: Scam syndicates
- **Attack Vector**: Phone calls, SMS, WhatsApp
- **Objective**: Financial extraction through fear

**Common Government Impersonations in Singapore**:

| Agency Impersonated | Pretext | Fear Lever |
|--------------------|---------|------------|
| **Singapore Police** | Criminal investigation | Arrest threat |
| **Ministry of Manpower** | Work permit issues | Deportation (foreigners) |
| **IRAS** | Tax investigation | Financial penalties |
| **SingPost** | Package delivery issue | Package loss |
| **Court** | Outstanding fine/warrant | Legal consequences |

**Attack Elements**:
- Official-sounding language
- Reference to real agencies/laws
- Threats of immediate consequences
- Demand for immediate action
- Transfer to "higher authority"
- Request for money transfer or personal details

---

## Privacy Violation Use-Cases

### Use-Case V1: Doxxing

**Scenario Profile**:
- **Target**: Individual (often public figure or in dispute)
- **Threat Actor**: Malicious individual or group
- **Attack Vector**: Online research + data aggregation
- **Objective**: Harassment through exposure of personal information

**Information Exposed**:
- Home address
- Workplace
- Family members
- Phone numbers
- Daily routines
- Personal photos

**Impact**:
- Physical safety threats
- Harassment of family/employer
- Emotional distress
- Employment consequences
- Need to relocate

---

### Use-Case V2: Non-Consensual Intimate Images (NCII)

**Scenario Profile**:
- **Target**: Individual (often in context of relationship)
- **Threat Actor**: Ex-partner, hacker, or extortionist
- **Attack Vector**: Image theft, relationship abuse
- **Objective**: Revenge, control, extortion

**Scenarios**:
1. **Relationship Revenge**: Ex-partner distributes intimate images
2. **Sextortion**: Threat to release images unless payment made
3. **Account Hack**: Intimate images stolen from cloud storage
4. **Deepfake Creation**: AI-generated fake intimate images

**Singapore Legal Context**:
- Protection from Harassment Act covers NCII
- Criminal penalties for distribution
- Can seek Protection Order
- But removal from internet extremely difficult

---

### Use-Case V3: Stalking via Technology

**Scenario Profile**:
- **Target**: Individual (often in domestic context)
- **Threat Actor**: Stalker (often known to victim)
- **Attack Vector**: Spyware, account access, location tracking
- **Objective**: Monitoring and control

**Technology-Enabled Stalking Methods**:

| Method | Implementation | Detection Difficulty |
|--------|----------------|---------------------|
| **Stalkerware** | Spyware installed on victim's phone | Hard without technical knowledge |
| **Account Access** | Access to victim's email/social media | May appear as normal activity |
| **Location Sharing** | Hidden tracking or shared accounts | Can be disguised |
| **AirTag/Tracking** | Hidden tracking device | Requires physical search |
| **Social Media Monitoring** | Fake accounts following victim | Difficult to identify |

---

## Impact Assessment for Individuals

### Financial Impact

| Impact Level | Loss Range | Recovery Likelihood |
|--------------|------------|-------------------|
| **Catastrophic** | Life savings, $100K+ | Very Low |
| **Severe** | $10K-$100K | Low |
| **Significant** | $1K-$10K | Medium |
| **Moderate** | $100-$1K | High |
| **Minor** | <$100 | High |

### Non-Financial Impacts

| Impact Category | Effects | Duration |
|-----------------|---------|----------|
| **Emotional** | Shame, anxiety, depression, PTSD | Months to years |
| **Social** | Relationship strain, isolation | Months to years |
| **Professional** | Job loss, reputation damage | Variable |
| **Physical** | Stress-related health issues | Variable |
| **Time** | Hours to months dealing with aftermath | Weeks to years |

---

## Consumer Protection Challenges

### Why Individuals Are Vulnerable

| Challenge | Explanation |
|-----------|-------------|
| **Asymmetric Information** | Attackers know more than victims |
| **Psychological Manipulation** | Attacks exploit human psychology |
| **Technical Complexity** | Hard to distinguish legitimate from fraudulent |
| **Always-On Connectivity** | Constant exposure to attack vectors |
| **Trust in Digital Services** | Legitimate services look like scams and vice versa |
| **Shame and Silence** | Victims don't report or seek help |

### Barriers to Protection

1. **Security Friction vs Usability**: Strong security often inconvenient
2. **Individual Responsibility Limits**: Can't protect against all organizational breaches
3. **Global Attackers, Local Victims**: Jurisdictional challenges
4. **Rapid Evolution**: Attacks evolve faster than awareness
5. **Resource Imbalance**: Individuals vs organized crime

---

## Singapore Individual Context

### Scam Statistics (2024)

| Metric | Value | Change |
|--------|-------|--------|
| **Total Scam Losses** | S$1.1 billion | Persistent |
| **Net Losses (after recovery)** | ~S$930 million | - |
| **Cybercrime % of All Crime** | 43% | Increasing |
| **Phishing Cases** | 6,100+ | +49% YoY |

### Top Scam Types in Singapore

1. **Investment Scams** - Highest amount lost
2. **Job Scams** - High volume
3. **E-commerce Scams** - Persistent
4. **Phishing** - Most common entry point
5. **Love Scams** - Highest emotional impact

### Government Protection Initiatives

| Initiative | Description | Status |
|------------|-------------|--------|
| **ScamShield** | Call/SMS blocking app | Active, expanded |
| **Anti-Scam Centre (ASC)** | Police unit for scam response | Active |
| **Money Lock** | Bank feature to lock funds | Implemented |
| **Project FRONTIER** | Bank-telco cooperation | Active |
| **IDCARE Singapore** | Identity theft support | Partnership active |

### What Individuals Can Do

**Immediate Actions**:
1. Enable ScamShield app
2. Activate Money Lock for savings
3. Use strong unique passwords
4. Enable 2FA (not SMS where possible)
5. Verify before acting on urgent requests

**Ongoing Vigilance**:
1. Verify sender identity independently
2. Don't click suspicious links
3. Research investment opportunities
4. Trust your instincts (if it feels wrong, stop)
5. Report scams (even unsuccessful ones)

**If Victimized**:
1. Contact bank immediately (fraud line)
2. Report to Police (file report)
3. Report to Anti-Scam Centre
4. Change compromised credentials
5. Monitor credit reports

---

## Reporting Resources (Singapore)

| Resource | Contact | Purpose |
|----------|---------|---------|
| **Police Report** | 1800-255-0000 | Criminal report |
| **Anti-Scam Hotline** | 1800-722-6688 | Scam reporting |
| **ScamShield Bot** | 9288 9288 | Report suspicious messages |
| **PDPC** | pdpc.gov.sg | Data breach reports |
| **NCPC** | ncpc.org.sg | Crime prevention resources |

---

*Return to [README.md](./README.md) for navigation*
