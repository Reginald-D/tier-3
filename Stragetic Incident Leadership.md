<div align="center">

# IT Helpdesk Portfolio
### Cross-Functional & Strategic Incident Leadership — Tier 3 Ticket Documentation

![Category](https://img.shields.io/badge/Category-Cross--Functional%20%26%20Strategic%20Incident%20Leadership-9B2C2C?style=for-the-badge)
![Tickets](https://img.shields.io/badge/Tickets-4-success?style=for-the-badge)
![Platform](https://img.shields.io/badge/Platform-ServiceNow%20Style-informational?style=for-the-badge)
![Environment](https://img.shields.io/badge/Environment-Incident%20Command%20%7C%20Executive%20Reporting-blueviolet?style=for-the-badge)

</div>

---

## About This Portfolio

This collection showcases four representative engagements spanning the most common **Cross-Functional & Strategic Incident Leadership** issues an enterprise Tier 3 team encounters.

Each ticket follows a standard **ServiceNow-style incident format**:

> `Reported Symptom` → `Diagnostic Steps` → `Root Cause` → `Resolution` → `User Communication`

> [!NOTE]
> These tickets are **representative scenarios** documenting the type of Tier 3 engagements handled in enterprise support roles. Ticket numbers and environment details are presented in standard ITSM format for professional documentation; company names and other client-identifying details have been generalized or removed to preserve confidentiality.

---

## Ticket Index

| # | Ticket ID | Title | Priority | Time to Resolve |
|---|-----------|-------|:--------:|:----------------:|
| 1 | [`INC0475689`](#inc0475689--served-as-technical-incident-commander-across-a-major-outage-spanning-six-teams) | Served as technical incident commander across a major outage spanning six teams | P1 | 6h 10m |
| 2 | [`INC0476044`](#inc0476044--delivered-a-root-cause-postmortem-and-funded-remediation-roadmap-to-executive-leadership) | Delivered a root-cause postmortem and funded remediation roadmap to executive leadership | P2 | 5d 0h |
| 3 | [`INC0476418`](#inc0476418--arbitrated-a-cross-team-architecture-decision-during-a-merger-system-integration) | Arbitrated a cross-team architecture decision during a merger system integration | P2 | 3w 2d (project) |
| 4 | [`INC0476792`](#inc0476792--engineered-a-systemic-fix-that-eliminated-an-entire-recurring-category-of-tier-12-access-tickets) | Engineered a systemic fix that eliminated an entire recurring category of Tier 1/2 access tickets | P3 | 3w 0d (project) |

---

<br>

## `INC0475689` — Served as technical incident commander across a major outage spanning six teams

<table>
<tr><td><b>Environment</b></td><td>Major multi-system production outage, six technical teams involved</td></tr>
<tr><td><b>Priority</b></td><td>P1 — Critical</td></tr>
<tr><td><b>Category</b></td><td>Strategic Incident Leadership > Technical Incident Command</td></tr>
<tr><td><b>Time to Resolve</b></td><td>6h 10m</td></tr>
</table>

**Reported Symptom**
A major outage began affecting several interdependent production systems simultaneously, with six different technical teams each independently investigating their own piece of the problem, duplicating effort and occasionally taking conflicting remediation actions.

<details>
<summary><b>Diagnostic Steps</b></summary>

1. Assumed technical incident command explicitly. Stepped into the commander role at the first sign the outage spanned multiple teams without coordination, and communicated that assumption immediately to all teams and leadership.
2. Established a single shared operating picture. Required every team to report findings and actions into one shared incident channel and timeline before making any further coordination decisions.
3. Resolved a direct conflict between two teams' remediation plans. Recognized two teams' independently proposed remediations would interact badly if both executed simultaneously, and made the explicit sequencing call.
4. Delegated investigation while retaining authority over shared-system actions. Allowed each team to investigate within their own domain at full speed while requiring any action affecting shared systems to go through a go/no-go decision first.
5. Owned executive communication directly. Became the single source of status updates to leadership, eliminating the inconsistent, fragmented updates reaching them earlier in the event.
6. Directed a coordinated, sequenced recovery once the root cause was visible. Identified the failed network configuration change as the common cause and directed a specific recovery sequence across all affected teams in correct dependency order.

</details>

**Root Cause**
The technical root cause was a single failed network configuration change cascading across dependent systems; the response itself was struggling due to the absence of a single point of coordination translating six teams' fragmented investigations into one coherent picture.

**Resolution**
Became the single source of status updates to leadership, eliminating the inconsistent, fragmented updates reaching them earlier in the event. Identified the failed network configuration change as the common cause and directed a specific recovery sequence across all affected teams in correct dependency order.

> **User Communication (Ticket Notes)**
> *Confirmed with the affected user/team that service was fully restored before closing the ticket.*

<div align="right"><a href="#ticket-index">back to top</a></div>

---

## `INC0476044` — Delivered a root-cause postmortem and funded remediation roadmap to executive leadership

<table>
<tr><td><b>Environment</b></td><td>Executive / board-level reporting, following a significant business-impacting outage</td></tr>
<tr><td><b>Priority</b></td><td>P2 — High</td></tr>
<tr><td><b>Category</b></td><td>Strategic Incident Leadership > Executive Postmortem</td></tr>
<tr><td><b>Time to Resolve</b></td><td>5d 0h</td></tr>
</table>

**Reported Symptom**
Following a significant outage, executive leadership requested a full account of what happened, why, and what would prevent recurrence — requiring a presentation that gave non-technical decision-makers genuine understanding and resulted in approved investment.

<details>
<summary><b>Diagnostic Steps</b></summary>

1. Structured the presentation around the decision leadership needed to make. Organized the postmortem around business impact and cost, a plain-language explanation of cause, and a specific investment request rather than the technical investigation's chronology.
2. Translated the technical root cause into business-relevant terms. Reframed the architectural single point of failure into business risk and consequence language while preserving full technical accuracy underneath.
3. Presented process gaps factually rather than as individual blame. Framed contributing process observations systemically rather than attributing fault to individuals, preserving a psychologically safe reporting culture.
4. Quantified the incident's cost alongside the investment request. Presented the remediation ask against a clear accounting of the incident's own cost and the projected cost of recurrence without investment.
5. Brought a phased, prioritized roadmap rather than one large ask. Structured the roadmap into phases with independent value, allowing leadership to approve an initial phase with a clear near-term return.
6. Built in a scheduled follow-up commitment. Concluded with a specific commitment to report progress at defined milestones, keeping the roadmap a tracked commitment rather than a one-time presentation.

</details>

**Root Cause**
The outage's technical root cause was already identified by this stage; the challenge being solved was translating a technically accurate finding into a narrative leadership could evaluate and act on without oversimplifying the risk or burying the decision in technical detail.

**Resolution**
Structured the roadmap into phases with independent value, allowing leadership to approve an initial phase with a clear near-term return. Concluded with a specific commitment to report progress at defined milestones, keeping the roadmap a tracked commitment rather than a one-time presentation.

> **User Communication (Ticket Notes)**
> *Confirmed with the affected user/team that service was fully restored before closing the ticket. Logged the preventive follow-up action identified during this incident for the team's process documentation.*

<div align="right"><a href="#ticket-index">back to top</a></div>

---

## `INC0476418` — Arbitrated a cross-team architecture decision during a merger system integration

<table>
<tr><td><b>Environment</b></td><td>Merger & acquisition system integration, two combined technical teams</td></tr>
<tr><td><b>Priority</b></td><td>P2 — High</td></tr>
<tr><td><b>Category</b></td><td>Strategic Incident Leadership > Architecture Arbitration (M&A)</td></tr>
<tr><td><b>Time to Resolve</b></td><td>3w 2d (project)</td></tr>
</table>

**Reported Symptom**
During a post-merger system integration, the two organizations' technical teams each arrived with a fully developed, internally successful identity architecture and each advocated for their own system to become the combined standard, stalling the integration timeline.

<details>
<summary><b>Diagnostic Steps</b></summary>

1. Reframed the decision around the combined organization's actual needs. Redirected both teams from defending their existing systems toward jointly defining the requirements and constraints of the combined organization going forward.
2. Established an objective, jointly agreed evaluation framework first. Worked with representatives from both teams to agree on evaluation criteria — scalability, security posture, integration complexity, total cost of ownership — before evaluating either architecture against them.
3. Conducted a joint, transparent technical evaluation. Ran the evaluation with senior engineers from both original teams directly involved, rather than as an independent assessment handed down from a single authority.
4. Reached a decision based on the evaluation's actual findings. Adopted one team's core platform as the foundation while incorporating a specific capability from the other team's system that the evaluation showed was genuinely stronger.
5. Communicated and documented the decision transparently. Shared the complete evaluation findings and rationale with both teams, ensuring the outcome was understood as evidence-based rather than imposed.
6. Reused the framework for subsequent integration decisions. Retained the evaluation methodology as the standard approach for the several other architecture decisions the broader merger integration still had ahead.

</details>

**Root Cause**
There was no purely technical basis for declaring one architecture objectively superior; each had been reasonably designed for its original organization's context, and the disagreement reflected an absence of an agreed, neutral decision framework rather than a genuine technical dispute.

**Resolution**
Shared the complete evaluation findings and rationale with both teams, ensuring the outcome was understood as evidence-based rather than imposed. Retained the evaluation methodology as the standard approach for the several other architecture decisions the broader merger integration still had ahead.

> **User Communication (Ticket Notes)**
> *Confirmed with the affected user/team that service was fully restored before closing the ticket.*

<div align="right"><a href="#ticket-index">back to top</a></div>

---

## `INC0476792` — Engineered a systemic fix that eliminated an entire recurring category of Tier 1/2 access tickets

<table>
<tr><td><b>Environment</b></td><td>Enterprise helpdesk / Tier 1-2 support operations, recurring high-volume ticket category</td></tr>
<tr><td><b>Priority</b></td><td>P3 — Medium</td></tr>
<tr><td><b>Category</b></td><td>Strategic Incident Leadership > Systemic Ticket-Class Elimination</td></tr>
<tr><td><b>Time to Resolve</b></td><td>3w 0d (project)</td></tr>
</table>

**Reported Symptom**
A specific, well-defined category of account access ticket had recurred at a steady, significant volume for an extended period, consuming disproportionate Tier 1/2 support capacity despite each individual occurrence being quick to resolve.

<details>
<summary><b>Diagnostic Steps</b></summary>

1. Quantified the pattern's true scale and cost. Pulled historical ticket data for the category over an extended period, building an evidence-based case for why individual resolution was not an adequate long-term response.
2. Traced every occurrence back to the same originating trigger. Analyzed a substantial sample of historical tickets and confirmed they all traced to the same role-transition scenario failing to auto-update the correct system.
3. Designed detection and remediation targeting the actual trigger. Designed a solution detecting the specific role-transition event at its source and automatically applying the correct access change at that moment, preventing the ticket from ever occurring.
4. Built the automation with production-grade safety discipline. Designed the remediation with staged validation — alert-only for human confirmation before graduating to full automated correction.
5. Validated against real historical trigger events before deployment. Tested detection and remediation logic against a reconstructed set of historical trigger events, confirming correct, safe prevention of every one.
6. Measured and reported the systemic impact. Tracked the ticket category's volume post-deployment and reported the near-complete elimination back to support leadership as a measurable capacity gain.

</details>

**Root Cause**
The recurring tickets traced to a predictable gap in the account lifecycle process: a routine role-transition scenario was not automatically reflected in the identity system, with no detection or automated remediation existing to catch the resulting misalignment before it generated a support ticket.

**Resolution**
Tested detection and remediation logic against a reconstructed set of historical trigger events, confirming correct, safe prevention of every one. Tracked the ticket category's volume post-deployment and reported the near-complete elimination back to support leadership as a measurable capacity gain.

> **User Communication (Ticket Notes)**
> *Confirmed with the affected user/team that service was fully restored before closing the ticket.*

<div align="right"><a href="#ticket-index">back to top</a></div>

---

## Portfolio Snapshot

| Metric | Value |
|---|---|
| **Total Tickets Documented** | 4 |
| **Critical (P1) Incidents** | 1 |
| **High Priority (P2) Incidents** | 2 |
| **Medium Priority (P3) Incidents** | 1 |
| **Average Time to Resolve** | ~1w 5d |
| **Systems Touched** | Technical Incident Command Structure · Unified Incident Channel & Shared Timeline · Cross-Team Remediation Conflict Resolution · Centralized Executive Communication · Dependency-Ordered Recovery Sequencing · Executive Communication & Presentation Design · Business Impact & Cost Quantification · Blameless Postmortem Methodology |

## Skills Demonstrated

`Technical Incident Command` · `Executive Postmortem & Roadmap Presentation` · `M&A Architecture Arbitration` · `Systemic Ticket-Class Elimination` · `Cross-Team Facilitation` · `Blameless Postmortem Methodology`

---

<div align="center">

*Built to demonstrate structured, repeatable troubleshooting methodology across cross-functional & strategic incident leadership — real-world Tier 3 scenarios, documented to enterprise standard.*

</div>