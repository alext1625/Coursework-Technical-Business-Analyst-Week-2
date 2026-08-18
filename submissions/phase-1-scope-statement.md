# Phase 1: Scope Statement 

## ADKAR Assessments

An ADKAR assessment was ran for multiple stakeholder groups in order to surface adoption risks early, and predict likely issues. The stakeholder groups were as follows:

- Collections team
- Customers
- Managers/team leaders 

---

### Collections Team

Collections agents are accustomed to manual workarounds across legacy databases and personal spreadsheets. Their primary risk is bypassing the portal if it adds administrative overhead or feels unreliable.

| ADKAR Element | Current Assessment | Adoption Risk Level | Specific Challenge |
| :--- | :--- | :---: | :--- |
| **Awareness** | They understand that current legacy systems and spreadsheets are slow, but are likely unaware of how automated routing works. | **Medium** | Agents may view the portal as a "management surveillance tool" rather than a tool to aid workflow. |
| **Desire** | High desire to reduce tedious manual note-taking, but fear that automated portals may mishandle fragile accounts. | **High** | Fear that portal errors will create additional customer issues that will land back on agents to fix manually. |
| **Knowledge** | Low understanding of the new digital self-service capabilities and rules-based routing logic. | **Medium** | Lack of clarity on when to let the portal handle a customer or when to intervene manually. |
| **Ability** | High capability to adapt, assuming the agent interface is simpler than the original legacy system's. | **Low** | If there is a lack of proper training with the new system, agents may struggle to use the portal effectively at first. |
| **Reinforcement** | Currently measured on handle times and call volumes rather than digital portal adoption. | **High** | Agents will default to old habits if performance metrics continue to reward manual call volume as opposed to digital portal adoption. |

---

### Customers

Delinquent customers face high emotional stress and varied financial literacy. Their primary risk is abandoning the portal if the interface is not user-friendly, or fails to offer flexible resolutions.

| ADKAR Element | Current Assessment | Adoption Risk Level | Specific Challenge |
| :--- | :--- | :---: | :--- |
| **Awareness** | They are currently unaware that self-service options exist, and instead are accustomed to letters or phone calls. | **High** | Customers ignore outreach emails/SMS if they are generic demands rather than actionable portal links. |
| **Desire** | Strong desire to resolve debt privately without speaking to an agent, assuming terms are clear and non-judgmental. | **Medium** | Skepticism about bank transparency or fear that logging in will trigger immediate legal/collection enforcement. |
| **Knowledge** | Varies widely, they are likely to have limited understanding of financial terminology. | **High** | Customers abandon the journey if options are worded in confusing banking terminology, as they are likely to grow frustrated. |
| **Ability** | Requires fairly high digital literacy/usage skill, but brittle login or rigid payment terms could cause immediate abandonment. | **High** | Complex authentication using banking details may cause drop-offs, driving inbound call spikes. |
| **Reinforcement** | Currently receive no immediate confirmation when completing transactions using the current system. | **Medium** | Lack of instant digital receipts or confirmation will leave customers uncertain of the outcome of a process. |

---

### Managers/Team Leaders

Team leaders are accountable for performance targets and compliance boundaries. Their primary risk is a lack of operational visibility into automated queues, leading to fear of lost cases.

| ADKAR Element | Current Assessment | Adoption Risk Level | Specific Challenge |
| :--- | :--- | :---: | :--- |
| **Awareness** | Fully aware of operational bottlenecks, missed callbacks, and agent capacity constraints. | **Low** | Already aligned on the need for change based on discovery data. |
| **Desire** | Highly motivated to enforce callbacks, but conscious of team capacity and vulnerability compliance. | **Medium** | Resistance if automated routing dumps complex cases back into general queues without appropriate context/information. |
| **Knowledge** | Clear on operational goals, but limited visibility or knowledge about backend routing rules and automated callback timers. | **Medium** | Uncertainty on how to audit automated decisions or track customer drop-off points in real time. |
| **Ability** | Despite leadership capability, they lack reporting dashboards to monitor portal vs agent workload. | **High** | Inability to track work movement leads to blind spots and a need for manual spreadsheet monitoring. |
| **Reinforcement** | Operational incentives focus on total recovery volume rather than SLA compliance and queue conditions. | **Medium** | Risk of management shifting focus back to manual phone outreach if they are unable to monitor initial portal metrics. |

---

## Change Risks and Mitigation Actions

Following these ADKAR assessments, the following risks were identified, alongside subsequent mitigation actions to minimise these risks.

### Risk 1: Brittle Authentication Causes Customer Abandonment (Customer Ability Risk)
- **Risk:** Customers may forget account numbers or credentials. If the portal authentication is overly rigid, they are likely to abandon the portal and opt to phone in, increasing agent workload and handling times.
- **Mitigation Action:** Implement a two-factor SMS/email link authentication mechanism tied directly to the customer's registered mobile number, eliminating the need to remember legacy account numbers.

### Risk 2: Agent Workaround & Dual-Data Entry (Agent Desire & Ability Risk)
- **Risk:** Agents may lack confidence in automated records and continue maintaining shadow spreadsheets, doubling administrative waste.
- **Mitigation Action:** Build automated status syncing between the portal and the legacy collections database. Enforce a single source of truth by deprecating legacy spreadsheet imports.

### Risk 3: Automated Routing Creates Manager Blind Spots (Manager Ability Risk)
- **Risk:** Team leaders cannot see where automated cases are sitting, leading to fears that complex or vulnerable accounts are being neglected.
- **Mitigation Action:** Embed operational observability directly into Phase 1. Provide managers with a real-time queue status dashboard showing portal throughput, automated callback SLA countdowns, and exception hand-offs.

### Risk 4: Confusing Terminology Triggers Drop-Offs (Customer Knowledge Risk)
- **Risk:** Financial terminology may confuse customers, leading to hesitation, frustration and non-completion.
- **Mitigation Action:** Use clear, easy to understand language across the portal, include clear progress trackers and indicators as helpful visual aids.

### Risk 5: Escalated Cases Missing Important Context (Agent Knowledge & Desire Risk)
- **Risk:** When a customer transitions from the portal to an agent due to case complexity, the agent receives no portal history, forcing the customer to repeat themselves, and increasing handling time.
- **Mitigation Action:** Build an "Agent Context Card" within the routing logic. When a case escalates, the agent automatically receives a summary of the customer's portal activity, selected options, and triggered risk flags before taking the call, giving them a better understanding of the case before-hand.

---

## Phase 1 Scope Definition 

The following section defines the scope of Phase 1, including what is in-scope and out-of-scope for the initial implementation, based on the previous ROI ranking and ADKAR risks.

--- 

### In-Scope

The following features have been identified as in-scope for Phase 1, in order to establish automation for straightforward cases, and to provide operational oversight for managers and team leaders:

#### Identity Verification 
- **Description:** Frictionless SMS/email two-factor authentication link system that verifies customers without requiring account numbers or manual intervention.
- **Justification:** Improves financial value by eliminating authentication drop-offs. By tying verification to mobile numbers as opposed to old account credentials, this feature mitigates the Customer Ability Risk, preventing increasing call volumes.

#### Account Summary & Eligible Actions:
- **Description:** Read-only dashboard showing account summary including total balance, overdue arrears, payment due date, etc.
- **Justification:** ROI calculations show this feature will result in a net benefit of £1.29M, with a projected 12-day payback period, cutting average handling time by 8 minutes per straightforward case. Inclusion of simple terminology also mitigates Customer Knowledge Risk.

#### Digital Promise-to-Pay Capture:
- **Description:** Allow customer selection of a payment date within an approved 30-day window, alongside instant digital receipt confirmation and automated SLA callback countdown timers.
- **Justification:** ROI calculations show this feature will result in a net benefit of £2.86M. Automates manual note-taking and callback scheduling, mitigating Agent Desire and Reinforcement Risks. Digital receipts also mitigate Customer Reinforcement Risk.

#### Keyword-Based Routing to Agents:
- **Description:** Uses a simplified keyword/self-identification approach to detect vulnerability, hardship, or dispute triggers and routes them to the relevant specialist agent queues. This is then followed by a short manual review of unflagged cases, for compliance reasons.
- **Justification:** ROI calculations show this feature will result in a net benefit of £583k. Protects agent capacity by ensuring vulnerable, hardship, or disputed accounts are immediately triaged away from self-service flows to specialist human teams, mitigating Agent Desire and Knowledge Risks.

#### Agent Context Card:
- **Description:** Automated summary that is sent to an agent when a customer escalates out of the portal, displaying customer portal actions, selected options, and triggered risk flags.
- **Justification:** Reduces agent handling time when cases are escalated from the portal, mitigating Agent Desire and Knowledge Risks. 

#### Portal Outcome Reporting & Audit Trail:
- **Description:** Full audit logging of all portal interactions, alongside a real-time queue status dashboard for managers to assess portal performance and team activity.
- **Justification:** Governance layer that protects against regulatory compliance audit failures. Mitigates the Manager Ability risk by replacing blind spots with real-time dashboards.

---

### Out-of-Scope

The following features have been excluded from the Phase 1 scope, in order to maintain delivery discipline and eliminate execution risk: 

#### Eligible Payment Plan Selection
- **Description:** Multi-month repayment schedule calculations, dynamic interest recalculation rules, and live payment gateway interactions.
- **Justification:** Despite offering high upside, requires dynamic interest recalculation rules, affordability assessment algorithms, and complex payment gateway integrations. Customers can't safely execute legally binding debt schedules until identity verification and screening rules are proven stable in production. Deferring this avoids delivery bottlenecks and eliminates compliance risks.

#### Hardship Assessment and Repayment Negotiation
- **Description:** Automated self-resolution of financial distress of legal dispute cases.
- **Justification:** High regulatory and ethical risk. Vulnerable customers and complex disputes should be redirected directly to human specialist agents, and attempting to automate this creates severe compliance risks.

#### Self-Serve Contact Detail Updates
- **Description:** Self-serve update of address and phone details.
- **Justification:** ROI calculations show this feature will result in a lower net benefit of £289k compared to other features listed above. Requires secondary verification workflows, and represents a secondary administrative efficiency that can remain in the backlog without impacting Phase 1 ROI.

#### Live Payment Processing
- **Description:** Live debit/credit card settlement engines.
- **Justification:** Ensuring compliance and third-party merchant processor integration add significant security testing overhead. Digital promise-to-pay capture already captures the majority of operational value without the security complexity of handling live card transactions.

#### Major Core Platform Replacement 
- **Description:** Modernising, refactoring, or replacing the underlying legacy database.
- **Justification:** High risk and significant resource requirement. Modernising or replacing the core platform introduces potential downtime, data migration challenges, and extensive testing needs. Deferring this ensures Phase 1 delivery focus and mitigates operational risks.

---  

### Dependencies and Ownership

To ensure realistic delivery estimation and avoid mid-sprint blockers, every Phase 1 feature/capability has been mapped to its underlying technical dependencies/external system integrations, and owners.

| Feature / Capability | Technical Dependency / System Integration | Owner |
| :--- | :--- | :---: |
| Identity Verification (SMS/Email 2FA links) | Third-Party Telephony API, central customer contact database | SecOps and Central Infrastructure Team |
| Self-Serve Account Summary | Read-Only Database Connector | Legacy Platform Maintenance Team |
| Digital Promise-to-Pay Capture | SLA Timer Engine to monitor P2P dates and trigger alerts | Product Engineering and Collections Ops |
| Keyword-Based Case Screening | Keyword Dictionary and Manual queue setup | Compliance Team and Gareth Evans |
| Agent Context Card | Bi-Directional Database Write-Back, API event triggers into legacy database to attach portal session notes to agent ticket | Core Systems IT Team, Gareth Evans |
| Portal Outcome Reporting and Audit Trail | Event Logger and Dashboard | Data Analytics and Business Intelligence team  |

### Trade-offs Accepted

**Rules-Based Case Routing** was changed from an automated approach based on defined parameters to a simpler, key-word flagging system. After speaking to Gareth about the current case complexity definition parameters, he mentioned that they exist but are heavily inconsistent, and flagged that they currently result in approximately a 60% capture rate, which is a major compliance issue. This would mean that new parameters would have to be defined from scratch, which would significantly increase the size and dependencies of the Phase 1 scope. 

As a result of this, a simpler, key-word based flagging approach, followed by a manual checking of non-flagged cases will be adopted for Phase 1, with full automation and defined parameters being deferred to Phase 2. 

---

## Deliverable Planning

The following section outlines the deliverables for Phase 1, including predicted timelines, estimated time required and potential blockers, as well as any required justifications. 

| Deliverable | Predicted Completion Day | Estimated Time Required | Potential Blockers | Justification |
| :--- | :--- | :---: | :--- | :--- |
| ADKAR Assessments | Day 1 | 2-3 hours | Aligning risks with operational incentives | Somewhat familiar and straightforward process. |
| Phase 1 Scope Definition | Day 1 | 3-4 hours | Push-back from stakeholders | Requires careful consideration of ROI, ADKAR risks, and stakeholder input. | 
| To-Be Process Mapping | Day 2 | 4-6 hours | Unfamiliar concept | Requires input from multiple stakeholders and consideration of current processes, as well as work from last week. |
| Jira Backlog Creation | Day 3 | 6-8 hours | Unfamiliar concept and technology | Requires careful consideration of user needs, and referral to high-level discovery. |
| Rapid Prototyping | Day 4 | 6-8 hours | Unfamiliar concept | Requires careful consideration of customer journey, and alignment with backlog requirements. |
| Slide Deck Creation | Day 5 | 4-6 hours | Unfamiliar concept | Requires careful consideration of compliance, and preparation of defensive arguments for any potential push-back or scrutiny. |