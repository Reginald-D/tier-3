<div align="center">

# IT Helpdesk Portfolio
### Vendor & Escalation Management — Tier 3 Ticket Documentation

![Category](https://img.shields.io/badge/Category-Vendor%20%26%20Escalation%20Management-9B2C2C?style=for-the-badge)
![Tickets](https://img.shields.io/badge/Tickets-4-success?style=for-the-badge)
![Platform](https://img.shields.io/badge/Platform-ServiceNow%20Style-informational?style=for-the-badge)
![Environment](https://img.shields.io/badge/Environment-Severity--1%20%7C%20Multi--Vendor-blueviolet?style=for-the-badge)

</div>

---

## About This Portfolio

This collection showcases four representative engagements spanning the most common **Vendor & Escalation Management** issues an enterprise Tier 3 team encounters.

Each ticket follows a standard **ServiceNow-style incident format**:

> `Reported Symptom` → `Diagnostic Steps` → `Root Cause` → `Resolution` → `User Communication`

> [!NOTE]
> These tickets are **representative scenarios** documenting the type of Tier 3 engagements handled in enterprise support roles. Ticket numbers and environment details are presented in standard ITSM format for professional documentation; company names and other client-identifying details have been generalized or removed to preserve confidentiality.

---

## Ticket Index

| # | Ticket ID | Title | Priority | Time to Resolve |
|---|-----------|-------|:--------:|:----------------:|
| 1 | [`INC0471172`](#inc0471172--severity-1-identity-platform-bug-escalated-past-standard-support-to-vendor-engineering) | Severity-1 identity platform bug escalated past standard support to vendor engineering | P1 | 3d 6h |
| 2 | [`INC0471549`](#inc0471549--intermittent-network-platform-defect-reproduced-as-a-minimal-case-for-vendor-engineering) | Intermittent network platform defect reproduced as a minimal case for vendor engineering | P2 | 4d 12h |
| 3 | [`INC0471920`](#inc0471920--negotiated-and-deployed-a-private-cloud-platform-hotfix-ahead-of-general-release) | Negotiated and deployed a private cloud platform hotfix ahead of general release | P2 | 6d 0h |
| 4 | [`INC0472305`](#inc0472305--resolved-a-three-vendor-finger-pointing-deadlock-on-an-intermittent-connectivity-defect) | Resolved a three-vendor finger-pointing deadlock on an intermittent connectivity defect | P1 | 9d 8h |

---

<br>

## `INC0471172` — Severity-1 identity platform bug escalated past standard support to vendor engineering

<table>
<tr><td><b>Environment</b></td><td>Cloud identity platform (Microsoft Entra ID), Severity-1 vendor case</td></tr>
<tr><td><b>Priority</b></td><td>P1 — Critical</td></tr>
<tr><td><b>Category</b></td><td>Vendor & Escalation Management > Severity-1 Engineering Escalation</td></tr>
<tr><td><b>Time to Resolve</b></td><td>3d 6h</td></tr>
</table>

**Reported Symptom**
A cloud identity platform began intermittently rejecting valid MFA responses for a subset of users, at a steadily growing rate. Front-line vendor support cycled through initial triage questions across several days without meaningful progress while the affected user count kept climbing.

<details>
<summary><b>Diagnostic Steps</b></summary>

1. Built an evidence package before requesting escalation. Compiled a structured, timestamped log of every confirmed occurrence — affected user, failure time, device, authentication method, and error code — to arrive with data demonstrating a genuine pattern.
2. Escalated formally through the correct organizational channel. Opened the case as a formal Severity-1 through the vendor's enterprise support channel with an explicit business impact statement and a specific request for engineering-level escalation.
3. Established a structured engagement cadence once escalated. Secured a fixed regular update cadence with the vendor's technical account manager and engineering team to prevent the case from stalling in a backlog.
4. Provided ongoing structured evidence throughout the investigation. Continued capturing every new occurrence in the same structured format, supplying updated data on request and proactively flagging new patterns observed.
5. Validated the vendor's proposed root cause independently. Cross-referenced every occurrence in the structured log against the vendor's proposed failure window to independently confirm the theory before accepting it as confirmed.
6. Tracked the fix through to confirmed resolution. Continued monitoring internal authentication logs for a sustained period following the vendor's backend fix to independently confirm the failure pattern had genuinely stopped.

</details>

**Root Cause**
A timing edge case in the vendor's own backend token validation service intermittently rejected a valid MFA response if it arrived within a narrow window of a specific backend synchronization event — a defect entirely inside the vendor's infrastructure, only identifiable with backend telemetry the vendor's engineering team alone had access to.

**Resolution**
Cross-referenced every occurrence in the structured log against the vendor's proposed failure window to independently confirm the theory before accepting it as confirmed. Continued monitoring internal authentication logs for a sustained period following the vendor's backend fix to independently confirm the failure pattern had genuinely stopped.

> **User Communication (Ticket Notes)**
> *Confirmed with the affected user/team that service was fully restored before closing the ticket. Logged the preventive follow-up action identified during this incident for the team's process documentation.*

<div align="right"><a href="#ticket-index">back to top</a></div>

---

## `INC0471549` — Intermittent network platform defect reproduced as a minimal case for vendor engineering

<table>
<tr><td><b>Environment</b></td><td>Network infrastructure platform (Cisco), production and isolated lab topology</td></tr>
<tr><td><b>Priority</b></td><td>P2 — High</td></tr>
<tr><td><b>Category</b></td><td>Vendor & Escalation Management > Bug Reproduction</td></tr>
<tr><td><b>Time to Resolve</b></td><td>4d 12h</td></tr>
</table>

**Reported Symptom**
A specific combination of routing configuration changes intermittently caused a network device platform to silently drop a narrow class of traffic with no logging or alarm, occurring so rarely in production that the vendor's support team could not investigate meaningfully from production evidence alone.

<details>
<summary><b>Diagnostic Steps</b></summary>

1. Treated production occurrences as clues to a pattern, not proof of a mechanism. Compiled every known production occurrence and looked for the narrowest common denominator across configuration state and traffic characteristics.
2. Built an isolated lab environment stripped to only the suspected components. Constructed a minimal lab topology using only the device platform and the narrowest routing elements identified as common across occurrences.
3. Iteratively narrowed the reproduction case through deliberate elimination. Systematically removed configuration elements from the lab reproduction one at a time until arriving at the smallest configuration that still reliably triggered the defect.
4. Confirmed reliable, on-demand reproducibility before engaging the vendor. Validated the minimal case triggered the defect consistently across repeated attempts, ensuring the vendor's own lab could reproduce it using the provided case.
5. Packaged the reproduction case with complete supporting detail. Documented the exact minimal configuration, required traffic pattern, expected versus actual behavior, and relevant diagnostic captures as a self-contained technical package.
6. Escalated with the reproduction case as the centerpiece of the argument. Presented the reliably reproducible case to the vendor's technical escalation team, shifting the conversation from whether a defect existed to how quickly it would be addressed.

</details>

**Root Cause**
A genuine defect in the platform's route processing logic under a specific, narrow combination of routing protocol configuration and traffic pattern — rare enough in production to occur unpredictably, but reliably reproducible once isolated to its essential triggering conditions.

**Resolution**
Documented the exact minimal configuration, required traffic pattern, expected versus actual behavior, and relevant diagnostic captures as a self-contained technical package. Presented the reliably reproducible case to the vendor's technical escalation team, shifting the conversation from whether a defect existed to how quickly it would be addressed.

> **User Communication (Ticket Notes)**
> *Confirmed with the affected user/team that service was fully restored before closing the ticket.*

<div align="right"><a href="#ticket-index">back to top</a></div>

---

## `INC0471920` — Negotiated and deployed a private cloud platform hotfix ahead of general release

<table>
<tr><td><b>Environment</b></td><td>Cloud platform service (AWS), confirmed platform defect</td></tr>
<tr><td><b>Priority</b></td><td>P2 — High</td></tr>
<tr><td><b>Category</b></td><td>Vendor & Escalation Management > Private Hotfix Negotiation</td></tr>
<tr><td><b>Time to Resolve</b></td><td>6d 0h</td></tr>
</table>

**Reported Symptom**
A confirmed platform defect was causing a recurring, business-impacting disruption, and the vendor had acknowledged the issue and begun developing a fix, but the fix sat on a general release timeline weeks away, with continued recurring impact in the interim.

<details>
<summary><b>Diagnostic Steps</b></summary>

1. Quantified the cost of waiting, not just the inconvenience. Built a quantified business impact statement covering the disruption's frequency, duration, and cost projected across the remaining weeks until general release.
2. Understood the vendor's own risk calculus before proposing acceleration. Engaged the vendor's technical account manager to understand why the standard rollout followed its staged timeline, in order to propose a request addressing that actual concern.
3. Proposed a scoped, risk-managed hotfix request. Requested the private hotfix specifically for the organization's own environment, offering to serve as an early, closely monitored validation point rather than requesting a general acceleration.
4. Negotiated explicit terms and a monitoring commitment. Agreed on a specific validation and monitoring plan, a defined rollback plan, and a communication protocol before proceeding.
5. Deployed the private hotfix with heightened validation. Applied the hotfix during a planned maintenance window with more extensive pre- and post-deployment validation than a fully released fix would warrant.
6. Maintained the monitoring commitment and reported results to the vendor. Executed the joint monitoring plan, confirmed the disruption had stopped with no new unexpected behavior, and reported validation results back to the vendor ahead of general release.

</details>

**Root Cause**
The defect had already been root-caused and a fix developed by the vendor; the remaining challenge was entirely negotiation and risk management — securing agreement to apply an unreleased, less broadly validated fix ahead of the vendor's normal staged validation process.

**Resolution**
Applied the hotfix during a planned maintenance window with more extensive pre- and post-deployment validation than a fully released fix would warrant. Executed the joint monitoring plan, confirmed the disruption had stopped with no new unexpected behavior, and reported validation results back to the vendor ahead of general release.

> **User Communication (Ticket Notes)**
> *Confirmed with the affected user/team that service was fully restored before closing the ticket. Logged the preventive follow-up action identified during this incident for the team's process documentation.*

<div align="right"><a href="#ticket-index">back to top</a></div>

---

## `INC0472305` — Resolved a three-vendor finger-pointing deadlock on an intermittent connectivity defect

<table>
<tr><td><b>Environment</b></td><td>Multi-vendor network and cloud integration (network hardware, cloud platform, ISP)</td></tr>
<tr><td><b>Priority</b></td><td>P1 — Critical</td></tr>
<tr><td><b>Category</b></td><td>Vendor & Escalation Management > Multi-Vendor Escalation Ownership</td></tr>
<tr><td><b>Time to Resolve</b></td><td>9d 8h</td></tr>
</table>

**Reported Symptom**
An intermittent connectivity failure affecting traffic between an on-premises environment and a cloud platform involved three separate vendors, each of whom investigated and concluded their portion of the path was functioning correctly, closing with no single vendor accepting ownership.

<details>
<summary><b>Diagnostic Steps</b></summary>

1. Took ownership of the full-path visibility no single vendor had. Accepted that resolving the deadlock required assembling and owning the complete cross-vendor picture rather than waiting for one vendor to investigate beyond their own boundary.
2. Built an end-to-end technical timeline across all three vendors. Collected diagnostic logs and packet captures from internal network devices, the cloud platform's diagnostics, and the ISP's circuit monitoring for the same failure occurrences.
3. Identified the specific technical interaction no single vendor's view could reveal. Analyzed the correlated evidence and identified the MTU mismatch at the boundary between two of the three vendors under a specific packet size and routing combination.
4. Reproduced the triggering condition to make the finding undeniable. Constructed a controlled test deliberately creating the identified packet size and routing combination, reliably triggering the failure on demand.
5. Convened a joint technical call with all three vendors simultaneously. Organized a single session with engineering representation from all three vendors, presenting the correlated evidence and reproducible test case directly, removing the ability to evaluate the issue in isolation.
6. Facilitated and independently validated the joint resolution. Worked with the two implicated vendors to agree on which side would adjust MTU handling, and validated the agreed fix independently through repeated testing of the previously failing condition.

</details>

**Root Cause**
A maximum transmission unit (MTU) mismatch at the boundary between two of the three vendors' systems only manifested under a specific combination of routing path and packet size that occurred intermittently, meaning each vendor's isolated testing genuinely found their own system behaving correctly.

**Resolution**
Organized a single session with engineering representation from all three vendors, presenting the correlated evidence and reproducible test case directly, removing the ability to evaluate the issue in isolation. Worked with the two implicated vendors to agree on which side would adjust MTU handling, and validated the agreed fix independently through repeated testing of the previously failing condition.

> **User Communication (Ticket Notes)**
> *Confirmed with the affected user/team that service was fully restored before closing the ticket.*

<div align="right"><a href="#ticket-index">back to top</a></div>

---

## Portfolio Snapshot

| Metric | Value |
|---|---|
| **Total Tickets Documented** | 4 |
| **Critical (P1) Incidents** | 2 |
| **High Priority (P2) Incidents** | 2 |
| **Average Time to Resolve** | ~5d 19h |
| **Systems Touched** | Structured Incident Logging · Vendor Enterprise Support Escalation Channel · Technical Account Manager & Engineering Engagement Cadence · Independent Root-Cause Validation Against Internal Logs · Post-Fix Independent Monitoring · Production Occurrence Pattern Analysis · Isolated Lab Environment · Iterative Elimination Methodology |

## Skills Demonstrated

`Severity-1 Vendor Engineering Escalation` · `Minimal Reproduction Case Development` · `Private Hotfix Negotiation` · `Multi-Vendor Escalation Ownership` · `Evidence-Based Technical Advocacy` · `Cross-Vendor Diagnostic Correlation`

---

<div align="center">

*Built to demonstrate structured, repeatable troubleshooting methodology across vendor & escalation management — real-world Tier 3 scenarios, documented to enterprise standard.*

</div>