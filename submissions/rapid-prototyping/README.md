# Smart-Recovery Customer Self-Service Portal — Phase 1 MVP Prototype

## 1. Executive Prototype Overview & Architecture

This prototype demonstrates the end-to-end customer self-service journey defined in Phase 1 scope: from SMS-based identity verification through to Promise-to-Pay (P2P) commitment, digital receipt, and exception hand-off to a human agent.

- **Format:** A single, self-contained `index.html` file — no build step, backend, or external dependencies (fonts, icon libraries, or CDNs). It runs directly in any modern browser by double-clicking the file, which keeps the prototype portable for stakeholder review and click-through testing.
- **Architecture pattern:** Client-side single-page application (SPA). All eight screens are authored as `<section class="screen">` elements in one document; a small vanilla JavaScript state machine toggles visibility (`showScreen(id)`) rather than performing page navigation, giving instant, app-like transitions.
- **State management:** A single in-memory `state` object tracks OTP attempt count, lockout/keyword exception reason, and form values (P2P date, checkbox). State is reset whenever the customer reaches a terminal screen and chooses "Done" or "Return to Prototype Start", simulating a fresh session.
- **Data:** All customer and account data (name, account number, balances, dates) is static/hard-coded for demo purposes, standing in for the real-time legacy database fetch described in US-03.
- **Design system:** Deep navy/teal banking palette, accessible colour contrast, rounded card components, mobile-first responsive layout (single-column ~560px max width, scales cleanly to desktop), visible focus states, and `prefers-reduced-motion` support for the shake/timer animations.
- **Top bar:** Present on every screen — bank brand header (Legacy Trust Bank logo + "Smart Recovery Portal" tagline) and a security badge ("Secure session · 256-bit encrypted") to reinforce trust throughout the journey.
- **Out of scope (by design):** Live card payment processing, real SMS/email dispatch, PDF generation, and backend/API integration are all simulated or placeholder-only, consistent with Phase 1 MVP scope.

---

## 2. Screen Inventory & Annotation Table

| Screen Name | User Story ID(s) | Key Data Shown | Business Rules / Validation | Next Step Outcome |
|---|---|---|---|---|
| **1. Landing Page (Access)** | US-01 | Bank brand header, security badge, greeting, editable "Email or mobile number" input field | Field must be non-empty and pass light format validation (valid email pattern, or a value with a leading `+`/digit and at least 7 digits for a phone number). Invalid input blocks submission with an inline error. | "Send Security Code" → Screen 2 (Identity Verification), destination is masked and carried forward for display |
| **2. Identity Verification (2FA)** | US-01, US-02 | 6-digit OTP boxes, masked destination (e.g. `j***@email.com` or `+44 7*** ***123`), 10-minute countdown timer, attempt counter badge ("Attempt X of 3") | Code `123456` = valid (happy path). Any other value = invalid attempt, increments counter, clears boxes with shake feedback. On the 3rd consecutive failure, session is marked `AUTH_LOCKOUT` and OTP timer stops. | Correct code → Screen 3 (Account Summary). 3 failed attempts → auto-routes to Screen 7 in **lockout** mode (Exception Path E-01) |
| **3. Account Summary Dashboard (OP-01)** | US-03, US-04, US-07 | Customer name (John Doe), account `***88291`, Total Balance `£1,250.00`, Overdue Arrears `£450.00`, Current Due Date, itemised plain-language charge breakdown (Missed Payments, Accrued Interest, Late Fees) in an accordion with inline tooltips | Read-only; accordion is collapsed by default to reduce cognitive load per US-04 | "Review Payment Options" → Screen 4 (Choose Next Action) |
| **4. Choose Next Action** | US-05, US-07 | 3 action cards: Set a Repayment Date, Pay Overdue Balance in Full Now, Financial hardship / dispute | Card selection is the only interaction; routing logic is deterministic per card | Card 1 → Screen 5 (P2P Flow). Card 2 → Pay-in-Full placeholder screen. Card 3 → Screen 7 in **keyword-flagged** mode (Exception Path E-02) |
| **4b. Pay in Full (Placeholder)** | US-05 (scope boundary) | Static message: "Live Payment Processing deferred to Phase 2" | None — informational placeholder only, no payment fields rendered | "Back to Options" → returns to Screen 4 |
| **5. Promise-to-Pay (P2P) Flow (OP-02)** | US-05 | Overdue balance badge `£450.00`, date picker constrained to today → +30 days, legal confirmation checkbox | Submit is blocked with an inline error if: (a) no date selected, (b) selected date falls outside the +30-day window, or (c) the confirmation checkbox is unchecked. Both the `min`/`max` date attributes and JS validation enforce the 30-day rule. | Valid submission → Screen 6 (Confirmation), reference `P2P-98421` generated |
| **6. Confirmation Page** | US-06, US-11 | Green success mark, Reference ID `P2P-98421`, confirmed payment date, confirmed amount `£450.00`, banner confirming instant SMS/Email digital receipt dispatch | Reference ID and amount are fixed for demo purposes; confirmed date reflects the customer's actual P2P selection | "Download Summary PDF" → simulated toast confirmation (no file generated in prototype). "Done" → resets all state and returns to Screen 1 |
| **7. Routed to Agent / Exception Outcome** | US-02, US-07, US-08, US-10 | Empathetic customer-facing message (copy varies by trigger reason), automated Callback SLA countdown timer (starts at `00:29:45`) | Two trigger variants share one template: **Lockout** (from 3× failed OTP) shows security-lockout messaging; **Keyword-flagged** (from hardship/dispute card) shows compliance-routing messaging. Timer counts down live and halts at `00:00:00`. | "Return to Prototype Start" → resets all state and returns to Screen 1 |

---

## 3. Stakeholder Click-Through Testing Guide

Open `index.html` directly in a browser (Chrome, Edge, or Safari recommended). Each guide below is scoped to the areas most relevant to that stakeholder's review focus.

### 3.1 Daniel Okoye — Compliance

Focus: authentication controls, lockout enforcement, keyword-based routing, and the legal confirmation step.

1. On the **Landing** screen, click **Send Security Code** without entering anything into the email/mobile field and confirm an inline validation error is shown. Then enter a valid value (e.g. `07123456789` or `daniel.okoye@email.com`) and click **Send Security Code** again.
2. On the **Identity Verification** screen, confirm the masked version of the value you entered is displayed, then enter any incorrect 6-digit code (e.g. `000000`) and click **Verify Code**. Confirm the attempt badge increments to "Attempt 1 of 3" and the boxes shake and clear.
3. Repeat step 2 twice more with incorrect codes. Confirm that after the 3rd failure, you are automatically routed to the **Routed to Agent** screen, displaying the security-lockout message and a live SLA countdown timer.
4. Click **Return to Prototype Start** to reset the session.
5. Re-enter the flow (Landing → Send Security Code), this time enter `123456` and click **Verify Code** to reach **Account Summary**.
6. Click **Review Payment Options**, then click the **"I'm experiencing financial hardship or dispute this balance"** card. Confirm this immediately routes to the **Routed to Agent** screen with the keyword-flagged compliance message (distinct wording from the lockout variant in step 3).
7. Return to start, repeat steps 5–6 but select **Set a Repayment Date** instead. On the P2P screen, attempt to click **Confirm Payment Date** without ticking the legal checkbox — confirm the inline validation error blocks submission. Then attempt to select a date outside the 30-day window and confirm it is also blocked.

### 3.2 Gareth Evans — Operations

Focus: SLA countdown behaviour, agent hand-off framing, and session reset consistency.

1. From **Landing**, enter a valid email or mobile number and proceed through OTP with `123456` to reach **Account Summary**.
2. Click **Review Payment Options** → select **Pay Overdue Balance in Full Now**. Confirm the placeholder screen clearly states "Live Payment Processing deferred to Phase 2" and that **Back to Options** returns you to the action cards without losing session state.
3. From **Choose Next Action**, select the hardship/dispute card and confirm the **Routed to Agent** screen shows the SLA countdown timer starting at `00:29:45` and counting down in real time (watch for a few seconds).
4. Click **Return to Prototype Start** and confirm all state resets — the attempt badge, OTP boxes, and any prior form entries should be cleared if you navigate the flow again.
5. Repeat the OTP lockout path (3× wrong codes) from the Compliance guide above and confirm the SLA timer resets to `00:29:45` fresh each time a new exception is triggered (it should not continue from a previous countdown).

### 3.3 Priya Nair — Product

Focus: full happy-path journey, plain-language content, and the confirmation/receipt experience.

1. From **Landing**, enter a valid email or mobile number, click **Send Security Code**, enter `123456`, and click **Verify Code**.
2. On **Account Summary**, expand **"View itemised charge breakdown"** and confirm the plain-language line items (Missed Payments, Accrued Interest, Late Payment Fees) sum correctly to the Overdue Arrears figure, and that hovering the ⓘ icons shows explanatory tooltips.
3. Click **Review Payment Options**, then select **Set a Repayment Date (Promise to Pay)**.
4. Select a valid date within the next 30 days, tick the legal confirmation checkbox, and click **Confirm Payment Date**.
5. On the **Confirmation** screen, verify the green success mark, reference ID `P2P-98421`, the payment date matches your selection, the amount reads `£450.00`, and the SMS/Email digital receipt banner is visible.
6. Click **Download Summary PDF** and confirm a toast notification appears confirming the simulated download.
7. Click **Done** and confirm the app returns cleanly to the **Landing** screen, ready for a fresh walkthrough.
