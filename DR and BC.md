<div align="center">

# IT Helpdesk Portfolio
### Disaster Recovery & Business Continuity — Tier 3 Ticket Documentation

![Category](https://img.shields.io/badge/Category-Disaster%20Recovery%20%26%20Business%20Continuity-9B2C2C?style=for-the-badge)
![Tickets](https://img.shields.io/badge/Tickets-4-success?style=for-the-badge)
![Platform](https://img.shields.io/badge/Platform-ServiceNow%20Style-informational?style=for-the-badge)
![Environment](https://img.shields.io/badge/Environment-DR%20Failover%20%7C%20Backup%20%7C%20BCP-blueviolet?style=for-the-badge)

</div>

---

## About This Portfolio

This collection showcases four representative engagements spanning the most common **Disaster Recovery & Business Continuity** issues an enterprise Tier 3 team encounters.

Each ticket follows a standard **ServiceNow-style incident format**:

> `Reported Symptom` → `Diagnostic Steps` → `Root Cause` → `Resolution` → `User Communication`

> [!NOTE]
> These tickets are **representative scenarios** documenting the type of Tier 3 engagements handled in enterprise support roles. Ticket numbers and environment details are presented in standard ITSM format for professional documentation; company names and other client-identifying details have been generalized or removed to preserve confidentiality.

---

## Ticket Index

| # | Ticket ID | Title | Priority | Time to Resolve |
|---|-----------|-------|:--------:|:----------------:|
| 1 | [`INC0474152`](#inc0474152--executed-and-validated-a-full-dr-failover-for-a-critical-business-system-during-an-actual-disaster) | Executed and validated a full DR failover for a critical business system during an actual disaster | P1 | 7h 45m |
| 2 | [`INC0474530`](#inc0474530--dr-runbook-found-significantly-outdated-mid-recovery-requiring-real-time-redesign) | DR runbook found significantly outdated mid-recovery, requiring real-time redesign | P1 | 10h 20m |
| 3 | [`INC0474918`](#inc0474918--reconstructed-critical-data-recovery-around-a-corrupted-link-in-the-backup-chain) | Reconstructed critical data recovery around a corrupted link in the backup chain | P1 | 1d 9h |
| 4 | [`INC0475301`](#inc0475301--business-continuity-architecture-review-launched-after-a-near-miss-exposes-a-single-point-of-failure) | Business continuity architecture review launched after a near-miss exposes a single point of failure | P2 | 2w 3d (project) |

---

<br>

## `INC0474152` — Executed and validated a full DR failover for a critical business system during an actual disaster

<table>
<tr><td><b>Environment</b></td><td>Critical business system, real unplanned regional infrastructure disruption</td></tr>
<tr><td><b>Priority</b></td><td>P1 — Critical</td></tr>
<tr><td><b>Category</b></td><td>Disaster Recovery & Business Continuity > Full DR Failover Execution</td></tr>
<tr><td><b>Time to Resolve</b></td><td>7h 45m</td></tr>
</table>

**Reported Symptom**
A genuine, unplanned regional infrastructure disruption took the primary hosting location for a critical business system offline with no defined recovery time, requiring real-time execution of a disaster recovery plan under conditions no drill had fully replicated.

<details>
<summary><b>Diagnostic Steps</b></summary>

1. Made the failover decision based on predefined criteria. Referenced the organization's predefined disaster declaration criteria, agreed upon well in advance, to make the initial decision on objective criteria rather than under real-time pressure.
2. Assumed technical command and communicated the decision immediately. Took ownership of executing the failover, notified executive leadership and every dependent business team immediately, and established a single status update channel.
3. Executed the documented sequence while actively validating each step. Followed the documented failover runbook step by step, treating each step's expected outcome as something to actively verify against real system state.
4. Managed in-flight data at the moment of failure deliberately. Identified transactions in progress at the exact moment of primary site failure and made a documented decision on handling that data, prioritizing integrity over speed for that subset.
5. Validated full data integrity and functional correctness before declaring completion. Conducted a structured validation pass covering data consistency, critical function availability, and integration health before treating the failover as complete.
6. Maintained heightened monitoring and a ready rollback capability. Kept the environment under closer-than-normal monitoring for the full duration of operating from the secondary site, with a validated rollback plan maintained throughout.

</details>

**Root Cause**
The event itself was an external infrastructure disruption outside organizational control; the engineering challenge was that real data-in-flight, real concurrent user load, and the pressure of an irreversible decision all introduced variables no scheduled drill fully replicates.

**Resolution**
Conducted a structured validation pass covering data consistency, critical function availability, and integration health before treating the failover as complete. Kept the environment under closer-than-normal monitoring for the full duration of operating from the secondary site, with a validated rollback plan maintained throughout.

> **User Communication (Ticket Notes)**
> *Confirmed with the affected user/team that service was fully restored before closing the ticket. Logged the preventive follow-up action identified during this incident for the team's process documentation.*

<div align="right"><a href="#ticket-index">back to top</a></div>

---

## `INC0474530` — DR runbook found significantly outdated mid-recovery, requiring real-time redesign

<table>
<tr><td><b>Environment</b></td><td>Production recovery event, environment materially changed since the runbook was last reviewed</td></tr>
<tr><td><b>Priority</b></td><td>P1 — Critical</td></tr>
<tr><td><b>Category</b></td><td>Disaster Recovery & Business Continuity > Outdated Runbook / Real-Time Redesign</td></tr>
<tr><td><b>Time to Resolve</b></td><td>10h 20m</td></tr>
</table>

**Reported Symptom**
In the middle of executing a documented disaster recovery runbook during an actual outage, the runbook was found to be significantly out of date — referencing servers that no longer existed and a topology since redesigned — while the business outage continued.

<details>
<summary><b>Diagnostic Steps</b></summary>

1. Recognized the runbook's failure as a signal to stop following it literally. Shifted explicitly to real-time recovery design grounded in current, actual system state the moment the documented steps stopped matching reality.
2. Rapidly established accurate current-state understanding. Pulled current infrastructure inventory and network topology documentation to establish an accurate picture of the environment as it actually existed.
3. Preserved the runbook's still-valid intent while rebuilding execution steps live. Identified which parts of the original runbook's recovery objectives remained valid and reconstructed the actual technical steps needed against the real, current environment.
4. Communicated the situation transparently to stakeholders. Informed leadership in real time that the documented procedure was significantly out of date and the team was executing a live redesign of the recovery approach.
5. Applied elevated verification to each improvised step. Applied a higher level of verification than would have been necessary with a previously tested runbook, given the absence of prior validation.
6. Rewrote the runbook and made currency a structural requirement. Fully rewrote the DR runbook to reflect the actual environment and implemented a mandatory DR documentation review gate in the infrastructure change management process.

</details>

**Root Cause**
The runbook had been accurate when written, but the production environment had undergone several rounds of infrastructure change since, with no process requiring the runbook to be reviewed as part of any of those change initiatives.

**Resolution**
Applied a higher level of verification than would have been necessary with a previously tested runbook, given the absence of prior validation. Fully rewrote the DR runbook to reflect the actual environment and implemented a mandatory DR documentation review gate in the infrastructure change management process.

> **User Communication (Ticket Notes)**
> *Confirmed with the affected user/team that service was fully restored before closing the ticket. Logged the preventive follow-up action identified during this incident for the team's process documentation.*

<div align="right"><a href="#ticket-index">back to top</a></div>

---

## `INC0474918` — Reconstructed critical data recovery around a corrupted link in the backup chain

<table>
<tr><td><b>Environment</b></td><td>Critical business data recovery, broken standard restore path</td></tr>
<tr><td><b>Priority</b></td><td>P1 — Critical</td></tr>
<tr><td><b>Category</b></td><td>Disaster Recovery & Business Continuity > Backup Chain Corruption Recovery</td></tr>
<tr><td><b>Time to Resolve</b></td><td>1d 9h</td></tr>
</table>

**Reported Symptom**
During an active data recovery effort, a required incremental backup in the middle of the backup chain was discovered to be corrupted and unusable, breaking the standard restore path entirely with a large volume of business-critical data at risk.

<details>
<summary><b>Diagnostic Steps</b></summary>

1. Fully mapped the intact and corrupted portions of the backup chain. Catalogued every available backup in the chain — the base full backup, every incremental, and any other recovery sources — to establish exactly what was and wasn't usable.
2. Determined precisely what data the corrupted link uniquely represented. Analyzed the specific time window the corrupted incremental was meant to capture to understand exactly what would be unrecoverable through the standard path.
3. Identified an alternative combination of intact sources covering the same data. Determined that the last known-good incremental, combined with application-level transaction logs covering an overlapping window, could together reconstruct the corrupted backup's substantive content.
4. Built and validated a non-standard restore procedure in an isolated environment. Constructed the improvised recovery combining the intact incremental and transaction logs in a test environment, validating internal consistency against known reference points.
5. Cross-validated the reconstructed data against every independent source. Compared the reconstructed data against independent corroborating sources to build confidence in the reconstruction's accuracy.
6. Executed the validated reconstruction and closed the verification gap. Applied the validated procedure to complete the production recovery and implemented mandatory backup integrity and restorability testing going forward.

</details>

**Root Cause**
The specific incremental backup had been silently corrupted at the storage layer after being written, a defect undetected because the organization's backup verification process confirmed job completion and file existence but did not include a full integrity or restorability test.

**Resolution**
Compared the reconstructed data against independent corroborating sources to build confidence in the reconstruction's accuracy. Applied the validated procedure to complete the production recovery and implemented mandatory backup integrity and restorability testing going forward.

> **User Communication (Ticket Notes)**
> *Confirmed with the affected user/team that service was fully restored before closing the ticket.*

<div align="right"><a href="#ticket-index">back to top</a></div>

---

## `INC0475301` — Business continuity architecture review launched after a near-miss exposes a single point of failure

<table>
<tr><td><b>Environment</b></td><td>Enterprise-wide continuity posture, no actual outage occurred</td></tr>
<tr><td><b>Priority</b></td><td>P2 — High</td></tr>
<tr><td><b>Category</b></td><td>Disaster Recovery & Business Continuity > Near-Miss Architecture Review</td></tr>
<tr><td><b>Time to Resolve</b></td><td>2w 3d (project)</td></tr>
</table>

**Reported Symptom**
A significant infrastructure component came within a narrow margin of a full failure that would have taken a critical business function offline, averted mainly through prompt manual intervention and fortunate timing rather than architectural resilience.

<details>
<summary><b>Diagnostic Steps</b></summary>

1. Treated the near-miss as a full architectural failure for review purposes. Explicitly resisted treating the event as a minor operational note simply because no actual outage occurred, initiating the same depth of review a genuine outage would have triggered.
2. Reconstructed exactly how close the event came to a full failure. Conducted a detailed technical reconstruction of the timeline, assessing whether the preventing factors were reliable safeguards or largely a matter of fortunate timing.
3. Mapped the full scope of business dependency on the exposed component. Traced every business function and downstream system dependent on the component to build an accurate picture of the true blast radius.
4. Assessed resilience against current, not original, criticality. Evaluated the component's actual redundancy and failover capability against the function's present-day importance, identifying the gap as the true root cause.
5. Designed and prioritized remediation proportional to the actual risk. Developed a specific redundancy remediation and built the business case for prioritization directly around the near-miss's detailed reconstruction.
6. Extended the review methodology into a standing practice. Formalized a requirement that any future near-miss affecting a critical function receive the same depth of review as an actual outage.

</details>

**Root Cause**
A specific component had, over time, become a single point of failure for a business function significantly more critical than the component's original design and criticality classification had accounted for, without a corresponding resilience review as the function's importance grew.

**Resolution**
Developed a specific redundancy remediation and built the business case for prioritization directly around the near-miss's detailed reconstruction. Formalized a requirement that any future near-miss affecting a critical function receive the same depth of review as an actual outage.

> **User Communication (Ticket Notes)**
> *Confirmed with the affected user/team that service was fully restored before closing the ticket. Logged the preventive follow-up action identified during this incident for the team's process documentation.*

<div align="right"><a href="#ticket-index">back to top</a></div>

---

## Portfolio Snapshot

| Metric | Value |
|---|---|
| **Total Tickets Documented** | 4 |
| **Critical (P1) Incidents** | 3 |
| **High Priority (P2) Incidents** | 1 |
| **Average Time to Resolve** | ~4d 19h |
| **Systems Touched** | Predefined Disaster Declaration Criteria · DR Failover Runbook & Live Execution Validation · Incident Command & Unified Stakeholder Communication · In-Flight Data Reconciliation · Post-Failover Data Integrity & Functional Validation · Current Infrastructure Inventory & Topology Documentation · Live Recovery Procedure Redesign · Real-Time Executive & Stakeholder Communication |

## Skills Demonstrated

`Full DR Failover Execution` · `Real-Time Runbook Redesign` · `Backup Chain Reconstruction` · `Near-Miss Architecture Review` · `Business Continuity Planning` · `Incident Command Under Live Disaster`

---

<div align="center">

*Built to demonstrate structured, repeatable troubleshooting methodology across disaster recovery & business continuity — real-world Tier 3 scenarios, documented to enterprise standard.*

</div>
