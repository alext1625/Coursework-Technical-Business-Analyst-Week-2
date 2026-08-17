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

