<div align="center">

# IT Helpdesk Portfolio
### Custom Engineering & Automation at Scale — Tier 3 Ticket Documentation

![Category](https://img.shields.io/badge/Category-Custom%20Engineering%20%26%20Automation%20at%20Scale-9B2C2C?style=for-the-badge)
![Tickets](https://img.shields.io/badge/Tickets-4-success?style=for-the-badge)
![Platform](https://img.shields.io/badge/Platform-ServiceNow%20Style-informational?style=for-the-badge)
![Environment](https://img.shields.io/badge/Environment-PowerShell%20%7C%20Python%20%7C%20API-blueviolet?style=for-the-badge)

</div>

---

## About This Portfolio

This collection showcases four representative engagements spanning the most common **Custom Engineering & Automation at Scale** issues an enterprise Tier 3 team encounters.

Each ticket follows a standard **ServiceNow-style incident format**:

> `Reported Symptom` → `Diagnostic Steps` → `Root Cause` → `Resolution` → `User Communication`

> [!NOTE]
> These tickets are **representative scenarios** documenting the type of Tier 3 engagements handled in enterprise support roles. Ticket numbers and environment details are presented in standard ITSM format for professional documentation; company names and other client-identifying details have been generalized or removed to preserve confidentiality.

---

## Ticket Index

| # | Ticket ID | Title | Priority | Time to Resolve |
|---|-----------|-------|:--------:|:----------------:|
| 1 | [`INC0472688`](#inc0472688--built-custom-remediation-tooling-for-a-recurring-security-exposure-with-no-vendor-solution) | Built custom remediation tooling for a recurring security exposure with no vendor solution | P2 | 3w 4d (project) |
| 2 | [`INC0473054`](#inc0473054--root-caused-an-internally-developed-automation-pipeline-that-executed-a-silently-incorrect-remediation) | Root-caused an internally developed automation pipeline that executed a silently incorrect remediation | P1 | 2d 5h |
| 3 | [`INC0473417`](#inc0473417--designed-and-deployed-an-automated-remediation-pipeline-after-a-recurring-manual-fix-pattern) | Designed and deployed an automated remediation pipeline after a recurring manual-fix pattern | P3 | 4w 2d (project) |
| 4 | [`INC0473789`](#inc0473789--api-integration-troubleshooting-required-when-platform-documentation-did-not-match-actual-behavior) | API integration troubleshooting required when platform documentation did not match actual behavior | P1 | 3d 1h |

---

<br>

## `INC0472688` — Built custom remediation tooling for a recurring security exposure with no vendor solution

<table>
<tr><td><b>Environment</b></td><td>Hybrid identity & endpoint fleet, no existing vendor capability for this specific gap</td></tr>
<tr><td><b>Priority</b></td><td>P2 — High</td></tr>
<tr><td><b>Category</b></td><td>Custom Engineering & Automation > Custom Tooling for Unaddressed Gap</td></tr>
<tr><td><b>Time to Resolve</b></td><td>3w 4d (project)</td></tr>
</table>

**Reported Symptom**
A recurring security exposure — stale, unused application permission grants — kept surfacing faster than any existing vendor tool could identify and safely clean them up, with no vendor roadmap item addressing the gap on a usable timeline.

<details>
<summary><b>Diagnostic Steps</b></summary>

1. Defined the actual decision the tooling needed to make before writing code. Worked backward from the specific, defensible question that needed answering for every permission grant, ensuring the tool would solve the real decision rather than automate existing limited visibility.
2. Combined multiple API data sources the vendor's own console never correlated. Used the identity platform's Graph API to pull permission, usage, and ownership data from three separate sources and built the correlation logic the platform had no built-in mechanism to perform.
3. Built the tool with a staged, reversible action model. Designed the tool to first operate in reporting-only mode, progressing to automated revocation only with an explicit approval step and rollback path, given the real risk of incorrectly revoking legitimate access.
4. Validated accuracy against known-good and known-bad cases before any production use. Tested the staleness determination against deliberately constructed test cases, confirming zero false positives on critical integrations before trusting the tool's output.
5. Piloted against a limited scope before fleet-wide use. Ran the tool's reporting mode against a single department's permissions first, manually verifying every flagged candidate before expanding scope organization-wide.
6. Operationalized the tool as a recurring, owned process. Scheduled the tool on a recurring basis with output feeding a defined review workflow, documented thoroughly enough to be maintained by others.

</details>

**Root Cause**
The identity platform's permission model tracked grants but not meaningful usage telemetry at the granularity needed to distinguish safely revocable access from rarely used but legitimate access, and no third-party tool in the vendor ecosystem solved this specific correlation problem at the required safety threshold.

**Resolution**
Ran the tool's reporting mode against a single department's permissions first, manually verifying every flagged candidate before expanding scope organization-wide. Scheduled the tool on a recurring basis with output feeding a defined review workflow, documented thoroughly enough to be maintained by others.

> **User Communication (Ticket Notes)**
> *Confirmed with the affected user/team that service was fully restored before closing the ticket. Logged the preventive follow-up action identified during this incident for the team's process documentation.*

<div align="right"><a href="#ticket-index">back to top</a></div>

---

## `INC0473054` — Root-caused an internally developed automation pipeline that executed a silently incorrect remediation

<table>
<tr><td><b>Environment</b></td><td>Internally built security remediation pipeline, production automation</td></tr>
<tr><td><b>Priority</b></td><td>P1 — Critical</td></tr>
<tr><td><b>Category</b></td><td>Custom Engineering & Automation > Orchestration Bug Root Cause</td></tr>
<tr><td><b>Time to Resolve</b></td><td>2d 5h</td></tr>
</table>

**Reported Symptom**
An internally developed automation pipeline responsible for automatically remediating a well-understood security finding took an unexpected, incorrect action against production systems, with the pipeline's own execution logs showing a series of steps that appeared entirely successful.

<details>
<summary><b>Diagnostic Steps</b></summary>

1. Immediately paused further automated execution. Suspended the pipeline the moment the incorrect action was identified, not trusting its own clean execution status as evidence the underlying logic was sound.
2. Reconstructed the exact decision path for the incorrect action. Traced the pipeline's internal logs and the exact input data received, stepping through the decision logic line by line against that real input.
3. Identified the upstream data change as the actual trigger. Compared the input data structure that led to the incorrect decision against what the pipeline's logic had originally been built against, finding the source tool's recent update had changed the field format.
4. Determined the full scope of exposure. Queried historical pipeline execution logs against the corrected understanding of the timing to identify every other instance of the same silent misexecution.
5. Fixed the immediate logic and added a structural safeguard. Corrected the decision logic for the new field format and added an explicit schema validation step at the pipeline's input boundary to safely halt on any future unexpected data change.
6. Remediated every affected system and rebuilt validation testing. Manually corrected every system affected by the historical incorrect executions and added the specific failure scenario as a permanent regression test case.

</details>

**Root Cause**
The pipeline's decision logic had been validated against its original finding pattern, but a subsequent, unrelated update to the source security tool changed the exact data structure of a field the pipeline relied on, causing it to silently misinterpret the field and choose the wrong remediation — invisible to the pipeline's own error handling since nothing technically constituted an error.

**Resolution**
Corrected the decision logic for the new field format and added an explicit schema validation step at the pipeline's input boundary to safely halt on any future unexpected data change. Manually corrected every system affected by the historical incorrect executions and added the specific failure scenario as a permanent regression test case.

> **User Communication (Ticket Notes)**
> *Confirmed with the affected user/team that service was fully restored before closing the ticket.*

<div align="right"><a href="#ticket-index">back to top</a></div>

---

## `INC0473417` — Designed and deployed an automated remediation pipeline after a recurring manual-fix pattern

<table>
<tr><td><b>Environment</b></td><td>Detection engineering / SOC operations, recurring high-volume finding category</td></tr>
<tr><td><b>Priority</b></td><td>P3 — Medium</td></tr>
<tr><td><b>Category</b></td><td>Custom Engineering & Automation > Automated Remediation Pipeline Design</td></tr>
<tr><td><b>Time to Resolve</b></td><td>4w 2d (project)</td></tr>
</table>

**Reported Symptom**
A specific, well-understood category of security finding had been recurring reliably for months at a volume consuming a disproportionate share of analyst time, with each occurrence requiring the same manual investigation and remediation sequence.

<details>
<summary><b>Diagnostic Steps</b></summary>

1. Studied the actual manual process in detail. Shadowed and reviewed a substantial sample of analysts' actual historical remediation actions, finding several undocumented judgment calls the written procedure didn't fully capture.
2. Explicitly separated the decision tree into automatable and judgment-required branches. Built a complete decision tree classifying each scenario as safe for full automation, safe with mandatory human approval, or requiring full human judgment.
3. Designed the pipeline architecture around the classified decision tree. Architected the pipeline to evaluate incoming findings against the decision tree's criteria and route to the correct handling path rather than a single linear script.
4. Built the pipeline with full auditability from the outset. Ensured every automated decision, action, and supporting context was logged in a structured, reviewable format from the first version.
5. Ran the pipeline in shadow mode before any live action. Operated the pipeline in a parallel, non-acting mode against live findings, comparing its proposed decisions against analysts' actual decisions to refine the decision tree.
6. Cut over incrementally by decision-tree branch. Enabled full automation first only for the highest-confidence branches, expanding to approval-gated branches once a track record was proven, with judgment-required branches permanently routed to analysts.

</details>

**Root Cause**
No automated pathway connected the finding's detection to its correct remediation, and building that pathway properly required first rigorously validating that the analysts' seemingly consistent manual process actually was as consistent and safe to fully automate as it appeared.

**Resolution**
Operated the pipeline in a parallel, non-acting mode against live findings, comparing its proposed decisions against analysts' actual decisions to refine the decision tree. Enabled full automation first only for the highest-confidence branches, expanding to approval-gated branches once a track record was proven, with judgment-required branches permanently routed to analysts.

> **User Communication (Ticket Notes)**
> *Confirmed with the affected user/team that service was fully restored before closing the ticket.*

<div align="right"><a href="#ticket-index">back to top</a></div>

---

## `INC0473789` — API integration troubleshooting required when platform documentation did not match actual behavior

<table>
<tr><td><b>Environment</b></td><td>Business-critical custom integration against a cloud platform API</td></tr>
<tr><td><b>Priority</b></td><td>P1 — Critical</td></tr>
<tr><td><b>Category</b></td><td>Custom Engineering & Automation > API / SDK-Level Troubleshooting</td></tr>
<tr><td><b>Time to Resolve</b></td><td>3d 1h</td></tr>
</table>

**Reported Symptom**
A custom integration built against a cloud platform's published API began failing intermittently in a way that directly contradicted the platform's official documentation, with the vendor's documentation insisting the observed behavior shouldn't be possible.

<details>
<summary><b>Diagnostic Steps</b></summary>

1. Treated the documentation as a hypothesis to test, not a fact to trust. Shifted the investigation entirely to empirically characterizing the platform's true behavior once repeated testing confirmed actual behavior did not match documentation.
2. Built a controlled test harness to characterize the behavior precisely. Constructed a minimal, isolated test script hitting the API directly, systematically varying request volume and payload size to map exactly which combinations triggered the divergence.
3. Captured complete raw request and response evidence. Logged raw HTTP request/response payloads, headers, and timing for every test case rather than relying on the SDK's higher-level abstraction.
4. Identified the specific undocumented condition precisely. Analyzed the complete test matrix and isolated the exact request volume and payload size threshold at which behavior diverged from the documented contract.
5. Engaged the vendor with empirical evidence rather than a documentation dispute. Presented the vendor's developer support team with the raw evidence and precise reproducible triggering condition, framing the engagement around confirmed actual behavior.
6. Engineered the integration to the platform's true behavior while pursuing a documentation fix. Modified the integration's request logic to proactively stay below the empirically identified threshold, ensuring reliable production behavior immediately.

</details>

**Root Cause**
The platform had an undocumented change to its internal rate-limiting and retry behavior under a specific combination of request volume and payload size, silently applying more aggressive throttling than documented and returning a response that appeared successful but had not fully processed the request.

**Resolution**
Presented the vendor's developer support team with the raw evidence and precise reproducible triggering condition, framing the engagement around confirmed actual behavior. Modified the integration's request logic to proactively stay below the empirically identified threshold, ensuring reliable production behavior immediately.

> **User Communication (Ticket Notes)**
> *Confirmed with the affected user/team that service was fully restored before closing the ticket.*

<div align="right"><a href="#ticket-index">back to top</a></div>

---

## Portfolio Snapshot

| Metric | Value |
|---|---|
| **Total Tickets Documented** | 4 |
| **Critical (P1) Incidents** | 2 |
| **High Priority (P2) Incidents** | 1 |
| **Medium Priority (P3) Incidents** | 1 |
| **Average Time to Resolve** | ~2w 1d |
| **Systems Touched** | Microsoft Graph API · PowerShell · Staged Validation · Limited-Scope Pilot Deployment · Scheduled Recurring Execution & Documentation · Pipeline Execution Log Analysis · Source Code · Historical Log Query |

## Skills Demonstrated

`Custom Tooling Development` · `Production Automation Root Cause Analysis` · `Automated Remediation Pipeline Design` · `API / SDK-Level Troubleshooting` · `Staged & Reversible Automation Safety Design` · `Detection-as-Code Engineering`

---

<div align="center">

*Built to demonstrate structured, repeatable troubleshooting methodology across custom engineering & automation at scale — real-world Tier 3 scenarios, documented to enterprise standard.*

</div>