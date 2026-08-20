# Prioritised Jira Backlog

A link to the Jira backlog can be found [here](https://alextidey-c25.atlassian.net/jira/software/projects/KAN/list?jql=project%20%3D%20KAN%20ORDER%20BY%20cf%5B10019%5D%20ASC)

Alternatively, the backlog items have also been listed below, with prioritisation logic explained in the section below.

---

## Backlog Items

### US-01: SMS/Email 2FA Link

#### User Story
As a customer trying to access the portal, I want to receive a verification passcode via text/email, so I can log-in without needing to remember my legacy account number.

#### Business Value
Eliminates login friction, easier access for customers, reduces potential agent time due to forgotten account numbers.

#### Acceptance Criteria
- When customer clicks link, system prompts for registered mobile number/email.
- When customer enters valid details,  secure 6-digit code is generated and sent to user.
- When customer enters invalid details, an error is displayed suggesting they call customer support due to unrecognised details
- When customer enters valid code, they are directed to the self serve portal.

#### Dependencies
None

#### Priority 
High 

--- 

### US-02: Passcode Validation and Lockout

#### User Story
As a portal security engine, I want to validate the customer’s passcode and enforce lockout after 3 failed attempts , so that only authorised access is allowed.

#### Business Value
Protects system and customer data from unauthorised users, ensures security and compliance.

#### Acceptance Criteria 
- When customer enters valid code, user is granted access to the self serve portal.
- When a user enters an incorrect code, they are denied access and an attempt count is recorded and displayed.
- When a user enters 3 consecutive incorrect passcodes, lockout event is triggered for 15 minutes, and a phone callback request option is displayed.

#### Dependencies
SMS/Email 2FA Link

#### Priority 
High

--- 

### US-03: Real-Time Account Summary Information Fetch

#### User Story
As an authenticated customer, I want to view my balance, overdue arrears and payment due date, so that I have complete visibility of my information and debt status.

#### Business Value
Increased customer satisfaction, £1.29M net benefit from ROI calculations

#### Acceptance Criteria 
- When an authenticated user logs in, the system executes a fetch request to the legacy collections database.
- Interface should display balance, overdue arrears amount and payment due date.
- Cache results to prevent blank screen in case of API timeout.

#### Dependencies
Access and Verification features, Read-Only API connector to Legacy Database.

#### Priority 
High

--- 

### US-04: Plain-Language Display

#### User Story
As a customer in financial distress, with little familiarity with financial terminology, I want to a see a simple breakdown and explanation of all financial information, so that I can understand all relevant information without confusion.

#### Business Value
Mitigates customer knowledge risks, reduces customer abandonment due to frustration.

#### Acceptance Criteria 
- When a customer clicks to view balance details, display a clear, easy to understand breakdown of debt, accrued interest, late fees, etc.
- Ensure that all terminology is simplified as much as possible whilst still conveying the right information.
- Include inline tooltips to assist with explanations.

#### Dependencies
Real-Time Account Summary information Fetch

#### Priority 
Medium

--- 

### US-05: Promise-to-Pay Date Selection

#### User Story
As an eligible customer with debt, I want to be able to select a date within the next 30 days to pay my overdue balance, so that I can resolve my debt without speaking to an agent.

#### Business Value
Net benefit of £2.86M according to ROI calculations, reduced agent handling time.

#### Acceptance Criteria
- When an eligible account, with no keyword flags, tries to access payment journey, an interactive calendar picker set between current date and +30 days is displayed.
- When user selects and submits a date, explicit customer confirmation checkbox is displayed and required to be selected.
- If a date beyond 30 days is selected, submission is prevented and relevant message is displayed.

#### Dependencies
Real-Time Account Summary Information Fetch, Keyword-Based Case Screening 

#### Priority 
High

--- 

### US-06: Digital Receipt and Confirmation

#### User Story
As a customer who has just submitted a P2P commitment, i want to receive an instant digital receipt, so that I have a written reminder and proof of my payment arrangement.

#### Business Value
Builds customer trust, reduces agent time by reducing call-backs.

#### Acceptance Criteria
- When a successful P2P submission is processed, trigger an automated SMS/Email confirmation containing amount, agreed date and unique reference number.
- When a successful P2P submission is processed, display a visual confirmation screen on the portal.
- Write a timestamp of the commitment and reference number to the legacy collections database.

#### Dependencies
Promise-to-Pay date selection.

#### Priority 
High

--- 

### US-07: Keyword-Based Case Screening

#### User Story
As a compliance engine, I want to scan account flags and customer entries against a keyword dictionary, so that complex, vulnerable, or disputed cases are automatically routed to agents.

#### Business Value
Protects agent capacity, servers as a compliance shield 

#### Acceptance Criteria
- When customer session is initialised or forms are submitted, input is scanned for keywords.
- When there is a keyword match, immediately halt self service, flag session as an exception and route case to specialist agent.
- When there are no keyword flags, once verified, all customer to proceed to self service P2P capture.

#### Dependencies
Compliance Keyword Dictionary

#### Priority 
High

--- 

### US-08: Agent Context Card Generation

#### User Story
As a collections agent receiving a case,  want to view a context card showing the customer’s portal actions and triggered keywords before speaking to them, so that I have knowledge of the case and don’t force the customer to repeat themselves.

#### Business Value
Mitigates Agent knowledge risk, reduces agent handling time by speeding up cases, increased customer satisfaction.

#### Acceptance Criteria
- When a case is escalated due to exception, when added to the agent queue, generate and attach an Agent Context Card.
- Card should display customer information, account info, trigger keywords and selected options.
- Card should automatically open with the case on agent’s desktop.

#### Dependencies 
Passcode Validation and Lockout, Keyword-Based Case Screening, Session Abandonment Detection and Follow-Up

#### Priority 
High

--- 

### US-09: Session Abandonment Detection and Follow Up

#### User Story
As an operational queue manager, I want the system to detect when a customer abandons their session, so that an automated follow-up sequence is initiated.

#### Business Value
Prevents process leakage, saves agent time by removing manual follow ups to dropped cases.

#### Acceptance Criteria
- When a customer logs in and views balances, once they are inactive for 10 minutes, mark session as abandoned.
- After 2 hours, automatically send a reminder via SMS to continue with session.
- After 24 hours, route case to agent follow-up queue with agent context card attached.

#### Dependencies
Real-Time Account Summary Information Fetch, Agent Context Card Generation

#### Priority 
Medium

---

### US-10: Automated Callback SLA Countdown Timers

#### User Story
As a team leader, I want automated countdown timers on promised agent callbacks, so that SLA breaches are highlighted before follow-ups are missed.

#### Business Value
Significantly reduces missed follow ups

#### Acceptance Criteria
- When a customer requests an agent callback via portal, attach SLA countdown timer when created.
- Colour code status badges in agent queue based on time remaining.
- If a timer is within 15 minutes of being breached and is unassigned, automatically reassign the ticket to next available active agent.

#### Dependencies
Agent Context Card Generation

#### Priority
High

---

### US-11: Agent Manual Triage Queue

#### User Story
As a collections team leader, I want a dedicated manual triage queue interface for unflagged edge cases, so that agents can manually review ambiguous sessions before assigning them.

#### Business Value
Supports phase 1 scope adjustment (using manual triage fallback whilst deferring automated rules engine to phase 2), ensures complex cases that weren’t originally flagged aren’t missed.

#### Acceptance Criteria
- Dedicated queue view displaying unflagged portal session logs that are unassigned.
- Manual reassignment options for Standard queue, vulnerability queue or dispute queue.
- Log manual agent routing decisions to audit trail.

#### Dependencies
Keyword-Based Case Screening, Agent Context Card Generation.

#### Priority
Medium

--- 

### US-12: Event Audit Logging Service

#### User Story
As a compliance officer, I want every customer portal action to be logged in an audit database, so that full interaction history is available for regulatory audit.

#### Business Value
Protects against FCA compliance breaches and fines.

#### Acceptance Criteria
- System must record time-stamped, append-only JSON event logs for all significant portal actions.
- Every log entry should record customer information, event type, timestamp, device, and outcome.
- Logs should be encrypted and immutable.

#### Dependencies
None

#### Priority
High

--- 

### US-13: Manager Queue Dashboard

#### User Story
As a manager/team leader, I want a real-time dashboard showing portal throughput, callback SLA status, and exception hand-offs, so that I have full visibility over all work movement.

#### Business Value
Mitigates risk of managerial blind spots, eliminates reliance on manual spreadsheets.

#### Acceptance Criteria
- Display live operational metrics such as total active portal sessions, self-service P2P completion rate, SLA breach count, keyword flagging escalation count.
- Include filterable queue behaviour.
- Ensure that dashboard regularly auto-refreshes.

#### Dependencies
Reporting and Audit trail

#### Priority
Medium

--- 

### US-14: Measure Post-Launch Workload Shift

#### User Story
As a manager, I want to compare baseline and post-launch workloads, so that I can confirm whether the implemented changes have reduced admin effort.

#### Business Value
Supports executive confidence

#### Acceptance Criteria
- Baseline and target measures are defined.
- Source of reporting data is agreed.
- Results can be reviewed after the initial rollout.

#### Dependencies
Event Audit Logging Service, Manager Queue Dashboard

#### Priority
Medium

--- 

### US-15: Fail-Safe Handling

#### User Story
As the delivery team, we want key error states to be clearly defined, so that journeys fail safely and predictably.

#### Business Value
Improves system resilience and customer trust.

#### Acceptance Criteria
- Failure states are documented for unavailable data and interrupted steps.
- Fallback path exists for critical journeys.
- User messaging is defined.

#### Dependencies
Real-Time Account Summary Information Fetch, Promise-to-Pay Date Selection

#### Priority
Medium

---

## Prioritisation Logic

### 1. Foundational - Technical prerequisites
Authentication and verification features, API connectors, and audit logging are foundational to the system and must be implemented first to ensure security, compliance, and data integrity.

### 2. Top-ROI drivers - Highest financial value drivers 
Account summary information fetch, promise-to-pay date selection, and digital receipt confirmation are the highest ROI drivers, directly impacting customer satisfaction and operational efficiency. These features depend directly on basic authentication and verification features, and are therefore prioritised after foundational items.

### 3. Risk mitigation - Compliance and adoption risk mitigations 
Keyword screening, agent context card generation, and manager dashboards are prioritised next, as they mitigate compliance and adoption risks, ensuring that the system can handle complex cases and provide visibility to management, as well as protecting agent handling times. These features are dependent on the foundational and top-ROI drivers, and are therefore prioritised after them.