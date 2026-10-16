<div align="center">

# IT Helpdesk Portfolio
### Enterprise Architecture & Design Failures — Tier 3 Ticket Documentation

![Category](https://img.shields.io/badge/Category-Enterprise%20Architecture%20%26%20Design%20Failures-9B2C2C?style=for-the-badge)
![Tickets](https://img.shields.io/badge/Tickets-5-success?style=for-the-badge)
![Platform](https://img.shields.io/badge/Platform-ServiceNow%20Style-informational?style=for-the-badge)
![Environment](https://img.shields.io/badge/Environment-Multi--Forest%20AD%20%7C%20DR%20%7C%20Federation-blueviolet?style=for-the-badge)

</div>

---

## About This Portfolio

This collection showcases five representative engagements spanning the most common **Enterprise Architecture & Design Failures** issues an enterprise Tier 3 team encounters.

Each ticket follows a standard **ServiceNow-style incident format**:

> `Reported Symptom` → `Diagnostic Steps` → `Root Cause` → `Resolution` → `User Communication`

> [!NOTE]
> These tickets are **representative scenarios** documenting the type of Tier 3 engagements handled in enterprise support roles. Ticket numbers and environment details are presented in standard ITSM format for professional documentation; company names and other client-identifying details have been generalized or removed to preserve confidentiality.

---

## Ticket Index

| # | Ticket ID | Title | Priority | Time to Resolve |
|---|-----------|-------|:--------:|:----------------:|
| 1 | [`INC0465520`](#inc0465520--cross-organization-multi-forest-trust-silently-fails-blocking-shared-application-access) | Cross-organization multi-forest trust silently fails, blocking shared application access | P1 | 1d 6h |
| 2 | [`INC0465884`](#inc0465884--automated-dr-failover-does-not-complete-as-designed-during-an-actual-primary-site-outage) | Automated DR failover does not complete as designed during an actual primary site outage | P1 | 9h 15m |
| 3 | [`INC0466230`](#inc0466230--recurring-network-capacity-incidents-require-structural-redesign-not-further-tactical-fixes) | Recurring network capacity incidents require structural redesign, not further tactical fixes | P2 | 6w 2d (project) |
| 4 | [`INC0466705`](#inc0466705--hybrid-federation-architecture-breaks-intermittently-across-overlapping-idp-trust-paths) | Hybrid federation architecture breaks intermittently across overlapping IdP trust paths | P1 | 2d 4h |
| 5 | [`INC0467112`](#inc0467112--legacy-system-decommission-risk-assessment-surfaces-undocumented-downstream-dependencies) | Legacy system decommission risk assessment surfaces undocumented downstream dependencies | P2 | 3w 1d (project) |

---

<br>

## `INC0465520` — Cross-organization multi-forest trust silently fails, blocking shared application access

<table>
<tr><td><b>Environment</b></td><td>Multi-forest AD trust spanning two partner organizations, external one-way trust</td></tr>
<tr><td><b>Priority</b></td><td>P1 — Critical</td></tr>
<tr><td><b>Category</b></td><td>Enterprise Architecture > Multi-Forest Identity Trust</td></tr>
<tr><td><b>Time to Resolve</b></td><td>1d 6h</td></tr>
</table>

**Reported Symptom**
A forest-level trust supporting joint operations and shared application access between two organizations failed silently. Users on one side lost authentication to resources on the other side entirely, with no clear indication of whether the fault was local, on the partner's side, or in between.

<details>
<summary><b>Diagnostic Steps</b></summary>

1. Opened a joint technical bridge with the partner organization immediately. Given the fault could originate on either side of the trust, coordinated real-time diagnosis with the partner's identity team rather than each side investigating independently and comparing notes hours later.
2. Validated the trust's current state on both sides. Ran nltest /trusted_domains and nltest /sc_query against the trust on the local domain, and requested the equivalent validation from the partner side, confirming the trust object existed but was failing secure channel validation.
3. Traced the authentication referral path. Cross-referenced the DCs historically designated to handle trust referrals against the current active DC inventory, finding a portion had been decommissioned with no update to the trust's dependent configuration.
4. Diagnosed the credential synchronization gap jointly. Working with the partner's identity team, confirmed the trust password had not been rotated in tandem following the standard interval, since the manual process had no clear owner after a personnel change.
5. Rebuilt the trust with coordinated validation at every step. Reset the trust password from an authoritative DC on each side in sequence, updated the referral path to current active domain controllers, and validated secure channel status from both organizations before considering the trust restored.
6. Co-authored a shared operational runbook. Documented joint ownership of trust password rotation with the partner organization, including current authoritative DCs on each side and a shared validation calendar, closing the governance gap that allowed the relationship to drift.

</details>

**Root Cause**
The trust's Kerberos trust password had drifted out of sync between the two domains after the manual synchronization process lapsed following a personnel change on the partner organization's side. Compounding this, the domain controllers historically handling the trust's authentication referrals had been partially decommissioned during an unrelated hardware refresh, with no update made to the trust's dependent configuration.

**Resolution**
Reset the trust password from an authoritative DC on each side in sequence, updated the referral path to current active domain controllers, and validated secure channel status from both organizations before considering the trust restored. Documented joint ownership of trust password rotation with the partner organization, including current authoritative DCs on each side and a shared validation calendar, closing the governance gap that allowed the relationship to drift.

> **User Communication (Ticket Notes)**
> *Confirmed with the affected user/team that service was fully restored before closing the ticket. Logged the preventive follow-up action identified during this incident for the team's process documentation.*

<div align="right"><a href="#ticket-index">back to top</a></div>

---

## `INC0465884` — Automated DR failover does not complete as designed during an actual primary site outage

<table>
<tr><td><b>Environment</b></td><td>Multi-site production architecture, primary data center and secondary availability zone</td></tr>
<tr><td><b>Priority</b></td><td>P1 — Critical</td></tr>
<tr><td><b>Category</b></td><td>Enterprise Architecture > Disaster Recovery Failover</td></tr>
<tr><td><b>Time to Resolve</b></td><td>9h 15m</td></tr>
</table>

**Reported Symptom**
A genuine, unplanned primary data center outage triggered automated failover to the secondary availability zone. Some services came up correctly; others did not, and a subset of services that did come up were serving stale or inconsistent data.

<details>
<summary><b>Diagnostic Steps</b></summary>

1. Prioritized business continuity over full diagnosis in the first hour. Manually completed failover for the services that hadn't come up automatically and redirected traffic away from the stale-data service while the underlying issue was assessed.
2. Reconstructed actual failover execution against the documented runbook. Reviewed the orchestration logs from the actual event step by step against the DR runbook, identifying the exact points of divergence.
3. Diagnosed the stale-data condition specifically. Traced the affected service's replication job history and found weeks of silent failures correlating with an unrelated monitoring platform migration that had deprioritized its alerts.
4. Diagnosed the missing-service gap specifically. Confirmed the second affected service had been provisioned after the DR architecture's last formal review and had never been incorporated into the failover automation's service inventory.
5. Corrected both gaps and validated through a controlled drill. Restored replication monitoring, formally incorporated the previously omitted service into failover automation, and tested both corrections in a controlled failover drill rather than waiting for the next real outage.
6. Implemented a standing DR governance checkpoint. Required an explicit DR architecture review before any new production service goes live, closing the gap that allowed a service to exist in production without ever being included in the DR design meant to protect it.

</details>

**Root Cause**
A dependent service's data replication job had silently failed for weeks prior to the outage, logged to a monitoring channel deprioritized after an unrelated alerting platform migration, leaving its secondary-site data significantly out of date. A second, newer service had been provisioned after the last formal DR architecture review and had never been incorporated into the failover automation at all.

**Resolution**
Restored replication monitoring, formally incorporated the previously omitted service into failover automation, and tested both corrections in a controlled failover drill rather than waiting for the next real outage. Required an explicit DR architecture review before any new production service goes live, closing the gap that allowed a service to exist in production without ever being included in the DR design meant to protect it.

> **User Communication (Ticket Notes)**
> *Confirmed with the affected user/team that service was fully restored before closing the ticket. Logged the preventive follow-up action identified during this incident for the team's process documentation.*

<div align="right"><a href="#ticket-index">back to top</a></div>

---

## `INC0466230` — Recurring network capacity incidents require structural redesign, not further tactical fixes

<table>
<tr><td><b>Environment</b></td><td>Enterprise core and distribution network layer, multi-site</td></tr>
<tr><td><b>Priority</b></td><td>P2 — High</td></tr>
<tr><td><b>Category</b></td><td>Enterprise Architecture > Network Redesign</td></tr>
<tr><td><b>Time to Resolve</b></td><td>6w 2d (project)</td></tr>
</table>

**Reported Symptom**
A recurring pattern of capacity-related network incidents — intermittent congestion, occasional routing instability during peak periods — had accumulated to the point where the pattern itself needed to be treated as the problem rather than continuing to firefight each occurrence as an isolated ticket.

<details>
<summary><b>Diagnostic Steps</b></summary>

1. Reframed the pattern as a design problem rather than a series of incidents. Mapped every capacity-related incident from the preceding period against the specific network segment and traffic type involved, revealing a consistent structural pattern rather than unrelated failures.
2. Modeled current traffic against the original design assumptions. Analyzed current traffic flow across the core and distribution layers and quantified precisely how far the environment had grown beyond its original design envelope.
3. Identified the specific structural bottlenecks. Traced each historical incident back to a specific architectural constraint — insufficient east-west capacity and an outdated routing topology — confirming tactical fixes had never addressed either.
4. Developed a redesign proposal grounded in current and projected need. Designed a revised architecture sized against current traffic plus a reasonable growth projection, incorporating a routing topology suited to the organization's current site distribution.
5. Built the business case and secured architectural approval. Presented the redesign to the infrastructure architecture review board with incident history and traffic analysis as supporting evidence, framing it as the alternative to continued recurring cost.
6. Executed a phased rollout with validation at each stage. Implemented the redesign in sequenced phases, confirming each stage's impact on the recurring incident pattern before proceeding to the next.

</details>

**Root Cause**
The core and distribution layer architecture had been designed years earlier around a traffic pattern and organizational footprint that no longer matched reality. Incremental growth had been absorbed through tactical additions rather than structural redesign, leaving an architecture straining against traffic it was never designed to carry.

**Resolution**
Presented the redesign to the infrastructure architecture review board with incident history and traffic analysis as supporting evidence, framing it as the alternative to continued recurring cost. Implemented the redesign in sequenced phases, confirming each stage's impact on the recurring incident pattern before proceeding to the next.

> **User Communication (Ticket Notes)**
> *Confirmed with the affected user/team that service was fully restored before closing the ticket.*

<div align="right"><a href="#ticket-index">back to top</a></div>

---

## `INC0466705` — Hybrid federation architecture breaks intermittently across overlapping IdP trust paths

<table>
<tr><td><b>Environment</b></td><td>Complex hybrid environment, three identity providers, multiple downstream service providers</td></tr>
<tr><td><b>Priority</b></td><td>P1 — Critical</td></tr>
<tr><td><b>Category</b></td><td>Enterprise Architecture > Identity Federation</td></tr>
<tr><td><b>Time to Resolve</b></td><td>2d 4h</td></tr>
</table>

**Reported Symptom**
Authentication began failing unpredictably for a subset of users across multiple applications in a hybrid environment with three identity providers and a legacy fourth identity source. The complexity of the federation architecture itself was the primary obstacle to understanding the failure.

<details>
<summary><b>Diagnostic Steps</b></summary>

1. Mapped the actual federation topology before attempting any fix. Built a complete current-state map of every IdP, every SP, and every trust relationship, discovering the undocumented overlapping trust no existing diagram had captured.
2. Correlated the failure pattern against the mapped topology. Cross-referenced the affected applications and users against the federation map and confirmed every affected case involved the overlapping trust path specifically.
3. Identified the triggering event. Reviewed recent changes across all IdPs and found a routine certificate rotation had occurred shortly before the failures began, disrupting the overlap's prior coincidental consistency.
4. Made a deliberate architectural decision rather than a quick patch. Used the federation map to determine which IdP should authoritatively own each SP relationship going forward, based on current organizational structure rather than historical onboarding shortcuts.
5. Executed the trust realignment in a controlled, staged sequence. Migrated each affected SP's trust relationship to its correctly designated IdP one at a time, validating authentication for a representative user set after each change.
6. Formalized the corrected architecture as the new standard. Documented the finalized, non-overlapping federation topology and required an explicit IdP designation step for any future application onboarding.

</details>

**Root Cause**
One identity provider had, at some point, been configured to also trust a subset of service providers that a second IdP was simultaneously configured to trust — an undocumented overlapping trust introduced during a rushed application onboarding effort. A routine certificate rotation on one IdP broke the coincidental consistency the overlap had been quietly relying on.

**Resolution**
Migrated each affected SP's trust relationship to its correctly designated IdP one at a time, validating authentication for a representative user set after each change. Documented the finalized, non-overlapping federation topology and required an explicit IdP designation step for any future application onboarding.

> **User Communication (Ticket Notes)**
> *Confirmed with the affected user/team that service was fully restored before closing the ticket. Logged the preventive follow-up action identified during this incident for the team's process documentation.*

<div align="right"><a href="#ticket-index">back to top</a></div>

---

## `INC0467112` — Legacy system decommission risk assessment surfaces undocumented downstream dependencies

<table>
<tr><td><b>Environment</b></td><td>Enterprise legacy system retirement, decade-old internal system</td></tr>
<tr><td><b>Priority</b></td><td>P2 — High</td></tr>
<tr><td><b>Category</b></td><td>Enterprise Architecture > Legacy Dependency Mapping</td></tr>
<tr><td><b>Time to Resolve</b></td><td>3w 1d (project)</td></tr>
</table>

**Reported Symptom**
A legacy internal system scheduled for decommission as part of a modernization initiative was believed to have a single known downstream consumer. A more thorough review, prompted by the system's age and thinning institutional knowledge, uncovered a very different picture.

<details>
<summary><b>Diagnostic Steps</b></summary>

1. Treated the known dependency list as a starting hypothesis, not a conclusion. Began with the single officially documented consumer but explicitly treated the risk assessment as incomplete until independently verified through direct technical evidence.
2. Instrumented the system to observe real consumption before assuming any list was complete. Enabled detailed connection and query logging on the system's database and network interfaces over an extended observation window to capture every actual source of access.
3. Investigated every unexpected consumer surfaced by direct observation. Traced each unaccounted connection source back to its origin, identifying the undocumented reporting jobs, the orphaned internal tool, and the compliance data feed, and engaged each consumer's owner to confirm legitimacy.
4. Assessed business criticality independently of technical visibility. Evaluated each newly discovered dependency by current business function rather than how it was built, finding the compliance feed still actively supported a recurring regulatory submission despite having no documented owner.
5. Built a remediation path for every dependency before proceeding. Re-pointed the reporting jobs to a supported data source, formally retired the orphaned tool after stakeholder confirmation, and built a documented replacement for the compliance feed ahead of the decommission date.
6. Executed the decommission with a recoverable rollback window. Proceeded with shutdown only once every discovered dependency had a validated remediation in place, keeping the system recoverable but offline for a defined period as a final safeguard.

</details>

**Root Cause**
Over more than a decade, the system had accumulated undocumented downstream consumers beyond its one officially recognized integration: scheduled reporting jobs querying its database directly, a since-departed team's internal tool never formally inventoried, and a data feed supporting a compliance reporting process with no current owner — none registered in any architecture diagram or service catalog.

**Resolution**
Re-pointed the reporting jobs to a supported data source, formally retired the orphaned tool after stakeholder confirmation, and built a documented replacement for the compliance feed ahead of the decommission date. Proceeded with shutdown only once every discovered dependency had a validated remediation in place, keeping the system recoverable but offline for a defined period as a final safeguard.

> **User Communication (Ticket Notes)**
> *Confirmed with the affected user/team that service was fully restored before closing the ticket.*

<div align="right"><a href="#ticket-index">back to top</a></div>

---

## Portfolio Snapshot

| Metric | Value |
|---|---|
| **Total Tickets Documented** | 5 |
| **Critical (P1) Incidents** | 3 |
| **High Priority (P2) Incidents** | 2 |
| **Average Time to Resolve** | ~2w 0d |
| **Systems Touched** | nltest · Active Directory Domains and Trusts · Cross-Organization Incident Bridge · Domain Controller Inventory & Dependency Mapping · Joint Operational Runbook · DR Orchestration · Data Replication Monitoring & Job History · DR Runbook & Architecture Documentation |

## Skills Demonstrated

`Multi-Forest AD Trust` · `Disaster Recovery Failover Architecture` · `Network Architecture Redesign` · `Identity Federation (Multi-IdP/SP)` · `Legacy Dependency Mapping` · `Cross-Organization Coordination`

---

<div align="center">

*Built to demonstrate structured, repeatable troubleshooting methodology across enterprise architecture & design failures — real-world Tier 3 scenarios, documented to enterprise standard.*

</div>