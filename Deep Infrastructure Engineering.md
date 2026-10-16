<div align="center">

# IT Helpdesk Portfolio
### Deep Infrastructure Engineering — Tier 3 Ticket Documentation

![Category](https://img.shields.io/badge/Category-Deep%20Infrastructure%20Engineering-9B2C2C?style=for-the-badge)
![Tickets](https://img.shields.io/badge/Tickets-5-success?style=for-the-badge)
![Platform](https://img.shields.io/badge/Platform-ServiceNow%20Style-informational?style=for-the-badge)
![Environment](https://img.shields.io/badge/Environment-Kernel%20%7C%20Storage%20%7C%20Database-blueviolet?style=for-the-badge)

</div>

---

## About This Portfolio

This collection showcases five representative engagements spanning the most common **Deep Infrastructure Engineering** issues an enterprise Tier 3 team encounters.

Each ticket follows a standard **ServiceNow-style incident format**:

> `Reported Symptom` → `Diagnostic Steps` → `Root Cause` → `Resolution` → `User Communication`

> [!NOTE]
> These tickets are **representative scenarios** documenting the type of Tier 3 engagements handled in enterprise support roles. Ticket numbers and environment details are presented in standard ITSM format for professional documentation; company names and other client-identifying details have been generalized or removed to preserve confidentiality.

---

## Ticket Index

| # | Ticket ID | Title | Priority | Time to Resolve |
|---|-----------|-------|:--------:|:----------------:|
| 1 | [`INC0469302`](#inc0469302--cascading-multi-service-outage-with-no-single-obvious-trigger-requires-cross-team-root-cause-analysis) | Cascading multi-service outage with no single obvious trigger requires cross-team root-cause analysis | P1 | 1d 3h |
| 2 | [`INC0469688`](#inc0469688--fleet-wide-endpoint-instability-traced-to-a-rare-kernel-level-driver-race-condition) | Fleet-wide endpoint instability traced to a rare kernel-level driver race condition | P2 | 9d 4h |
| 3 | [`INC0470041`](#inc0470041--storage-array-firmware-bug-causes-silent-data-corruption-discovered-only-through-a-migration-audit) | Storage array firmware bug causes silent data corruption discovered only through a migration audit | P1 | 6d 20h |
| 4 | [`INC0470418`](#inc0470418--mission-critical-database-corruption-exceeds-standard-repair-tools-requiring-vendor-engineering-escalation) | Mission-critical database corruption exceeds standard repair tools, requiring vendor engineering escalation | P1 | 2d 16h |
| 5 | [`INC0470795`](#inc0470795--diminishing-returns-from-repeated-performance-tuning-signal-a-structural-architecture-ceiling) | Diminishing returns from repeated performance tuning signal a structural architecture ceiling | P2 | 8w 3d (project) |

---

<br>

## `INC0469302` — Cascading multi-service outage with no single obvious trigger requires cross-team root-cause analysis

<table>
<tr><td><b>Environment</b></td><td>Interdependent production services across five engineering teams</td></tr>
<tr><td><b>Priority</b></td><td>P1 — Critical</td></tr>
<tr><td><b>Category</b></td><td>Deep Infrastructure Engineering > Cascading Outage Root Cause</td></tr>
<tr><td><b>Time to Resolve</b></td><td>1d 3h</td></tr>
</table>

**Reported Symptom**
Within roughly twenty minutes, five ostensibly independent production services began failing in a rolling sequence. Each team could point to a symptom on their own system, but none explained why four other unrelated services were failing in the same short window.

<details>
<summary><b>Diagnostic Steps</b></summary>

1. Established a single, unified incident timeline before allowing siloed investigations. Consolidated every team's timeline of observed symptoms into one master timeline immediately rather than letting five parallel investigations each converge on their own local explanation.
2. Worked backward from the earliest symptom, not the loudest alert. Identified which of the five services showed its first anomalous symptom earliest and treated that as the most likely lead toward the true origin point.
3. Mapped the full dependency graph from real telemetry. Built a verified dependency map by tracing actual request and connection telemetry between services rather than trusting each team's documented understanding of their own dependencies.
4. Correlated the shared dependency's own health metrics against the timeline. Pulled the caching layer's memory and eviction metrics and found degradation beginning hours before the first visible service failure.
5. Traced the degradation to its actual code-level source. Reviewed recent changes to the caching layer and identified the specific deployment that introduced the memory leak.
6. Stabilized the shared dependency and validated recovery flowed outward correctly. Rolled back the offending deployment, restarted the affected nodes, and confirmed each of the five originally affected services recovered independently once the shared cause was removed.

</details>

**Root Cause**
A shared internal caching layer several dependency layers removed from most affected services' own awareness had begun silently degrading due to a slow memory leak in a recent code change, hours before the first visible service failure, producing a staggered failure sequence that looked like five unrelated incidents.

**Resolution**
Reviewed recent changes to the caching layer and identified the specific deployment that introduced the memory leak. Rolled back the offending deployment, restarted the affected nodes, and confirmed each of the five originally affected services recovered independently once the shared cause was removed.

> **User Communication (Ticket Notes)**
> *Confirmed with the affected user/team that service was fully restored before closing the ticket.*

<div align="right"><a href="#ticket-index">back to top</a></div>

---

## `INC0469688` — Fleet-wide endpoint instability traced to a rare kernel-level driver race condition

<table>
<tr><td><b>Environment</b></td><td>Enterprise endpoint fleet, multiple thousand managed devices</td></tr>
<tr><td><b>Priority</b></td><td>P2 — High</td></tr>
<tr><td><b>Category</b></td><td>Deep Infrastructure Engineering > Kernel / Firmware Conflict</td></tr>
<tr><td><b>Time to Resolve</b></td><td>9d 4h</td></tr>
</table>

**Reported Symptom**
Over several weeks, a slowly growing number of machines across the fleet began experiencing unexplained blue-screen crashes with no consistent pattern by department, hardware age, or workload. Standard first-line remediation provided only temporary relief.

<details>
<summary><b>Diagnostic Steps</b></summary>

1. Recognized the pattern was statistical, not deterministic. Treated the inability to reliably reproduce the crash on demand, combined with its gradual aggregate growth, as a sign of a low-probability, timing-dependent condition rather than a deterministic bug.
2. Collected kernel memory dumps from every occurrence. Configured the fleet to capture full kernel memory dumps on any unexplained crash rather than relying on minimal default crash logs.
3. Performed deep kernel-level analysis on accumulated dumps. Used kernel debugging tools to analyze dumps from multiple affected machines and identified a consistent fault signature in a driver-kernel interaction during power-state transitions.
4. Correlated the affected population against the implicated variables. Cross-referenced every affected machine's driver and kernel version and confirmed crashes occurred exclusively on one specific combination.
5. Reproduced the race condition under controlled, accelerated conditions. Built a test harness that rapidly and repeatedly triggered the implicated power-state transition, reliably reproducing the crash under accelerated conditions.
6. Remediated the fleet with a staged, monitored rollout. Obtained a validated corrected driver from the vendor and rolled it out in monitored waves, confirming stability at each stage before proceeding.

</details>

**Root Cause**
A specific combination of a third-party peripheral driver and a recent kernel update created a low-probability race condition occurring only under a rare timing sequence during device power-state transitions, statistically visible only once a large enough fleet running the affected combination had accumulated enough attempts at the vulnerable window.

**Resolution**
Built a test harness that rapidly and repeatedly triggered the implicated power-state transition, reliably reproducing the crash under accelerated conditions. Obtained a validated corrected driver from the vendor and rolled it out in monitored waves, confirming stability at each stage before proceeding.

> **User Communication (Ticket Notes)**
> *Confirmed with the affected user/team that service was fully restored before closing the ticket.*

<div align="right"><a href="#ticket-index">back to top</a></div>

---

## `INC0470041` — Storage array firmware bug causes silent data corruption discovered only through a migration audit

<table>
<tr><td><b>Environment</b></td><td>Enterprise SAN serving multiple production systems</td></tr>
<tr><td><b>Priority</b></td><td>P1 — Critical</td></tr>
<tr><td><b>Category</b></td><td>Deep Infrastructure Engineering > Storage Firmware / Data Integrity</td></tr>
<tr><td><b>Time to Resolve</b></td><td>6d 20h</td></tr>
</table>

**Reported Symptom**
A data integrity check performed during an unrelated migration project surfaced a small number of files with checksums that didn't match expected values, on data that had sat untouched for weeks with no error ever indicated.

<details>
<summary><b>Diagnostic Steps</b></summary>

1. Treated the discovery as a systemic risk, not an isolated data issue. Escalated the finding as a potential silent, ongoing data integrity risk affecting the entire array rather than simply restoring the specific corrupted files and closing the finding.
2. Conducted a full, systematic integrity audit across the entire array. Ran comprehensive checksum verification across every file and volume against known-good checksums from backup systems and application-level records.
3. Quantified the true scope of corruption. Catalogued every file across the array with a checksum mismatch, building an accurate picture of the corruption's actual extent.
4. Escalated directly to the storage vendor's engineering team. Provided detailed I/O pattern logs, controller cache state information, and corrupted data samples, engaging the vendor's engineering team directly given the severity.
5. Contained the ongoing risk while awaiting the firmware fix. Worked with the vendor to temporarily disable the specific caching behavior implicated, accepting a measured performance tradeoff to eliminate the corruption risk.
6. Remediated every confirmed file and validated the vendor's fix. Restored every corrupted file from verified clean backups, validated integrity, and re-enabled the caching behavior only once the vendor's firmware fix was independently validated.

</details>

**Root Cause**
A firmware bug in the storage array's controller, triggered only under a specific combination of concurrent write patterns and controller cache state, caused a small number of writes to be acknowledged as successful while actually writing subtly corrupted data — a fault invisible to any standard I/O error check.

**Resolution**
Worked with the vendor to temporarily disable the specific caching behavior implicated, accepting a measured performance tradeoff to eliminate the corruption risk. Restored every corrupted file from verified clean backups, validated integrity, and re-enabled the caching behavior only once the vendor's firmware fix was independently validated.

> **User Communication (Ticket Notes)**
> *Confirmed with the affected user/team that service was fully restored before closing the ticket.*

<div align="right"><a href="#ticket-index">back to top</a></div>

---

## `INC0470418` — Mission-critical database corruption exceeds standard repair tools, requiring vendor engineering escalation

<table>
<tr><td><b>Environment</b></td><td>Mission-critical production database, Severity-1 vendor case</td></tr>
<tr><td><b>Priority</b></td><td>P1 — Critical</td></tr>
<tr><td><b>Category</b></td><td>Deep Infrastructure Engineering > Database Engine Corruption</td></tr>
<tr><td><b>Time to Resolve</b></td><td>2d 16h</td></tr>
</table>

**Reported Symptom**
A mission-critical production database began throwing internal consistency errors that the database engine's own standard repair and consistency-check utilities could not resolve, with the database's criticality ruling out a simple restore-and-accept-data-loss approach.

<details>
<summary><b>Diagnostic Steps</b></summary>

1. Stabilized the immediate situation before attempting further repair. Isolated the database from write traffic to prevent the corruption from worsening while a resolution path was determined.
2. Exhausted and documented every standard recovery path. Systematically attempted every vendor-documented repair procedure applicable to the error signature, documenting each exact outcome to prove standard remediation had been genuinely exhausted.
3. Captured a complete, isolated forensic copy before further action. Took a full storage-level copy of the database in its exact corrupted state so vendor engineering could analyze the actual fault unaltered by further attempts.
4. Escalated to the vendor's engineering team with a complete technical package. Opened a Severity-1 case requesting engineering-level escalation with documented failed attempts, error signatures, and access to the isolated copy.
5. Collaborated directly with vendor engineering on a custom recovery procedure. Worked in real-time coordination as the vendor's team diagnosed the internal storage structure defect and developed a non-standard recovery procedure, validating each step against the isolated copy first.
6. Validated full data integrity before returning to production. Followed the vendor's custom procedure, ran complete data integrity and consistency validation cross-referenced against independent application-level checks, before restoring write access.

</details>

**Root Cause**
A rare interaction between a specific application query pattern and an edge case in the database engine's own internal storage structure handling — a latent defect in the engine itself rather than any configuration or operational error — meant no external repair tool, which assumes the engine's own internal logic is sound, had any way to address it.

**Resolution**
Worked in real-time coordination as the vendor's team diagnosed the internal storage structure defect and developed a non-standard recovery procedure, validating each step against the isolated copy first. Followed the vendor's custom procedure, ran complete data integrity and consistency validation cross-referenced against independent application-level checks, before restoring write access.

> **User Communication (Ticket Notes)**
> *Confirmed with the affected user/team that service was fully restored before closing the ticket.*

<div align="right"><a href="#ticket-index">back to top</a></div>

---

## `INC0470795` — Diminishing returns from repeated performance tuning signal a structural architecture ceiling

<table>
<tr><td><b>Environment</b></td><td>High-growth production platform, multi-year capacity planning engagement</td></tr>
<tr><td><b>Priority</b></td><td>P2 — High</td></tr>
<tr><td><b>Category</b></td><td>Deep Infrastructure Engineering > Capacity Modeling & Architecture Redesign</td></tr>
<tr><td><b>Time to Resolve</b></td><td>8w 3d (project)</td></tr>
</table>

**Reported Symptom**
A production platform experiencing sustained business growth had been kept performant for over a year through a steady sequence of tuning efforts, each buying less headroom than the last — a pattern of diminishing returns signaling the architecture had reached a structural ceiling no further tuning could raise.

<details>
<summary><b>Diagnostic Steps</b></summary>

1. Modeled the actual growth trajectory rather than reacting to the current bottleneck. Built a capacity model projecting business growth over the following two to three years, sizing any eventual solution against that trajectory rather than the platform's current strained state.
2. Quantified precisely where the architecture's structural ceiling sat. Conducted detailed load testing to identify the specific point beyond which no further vertical scaling or tuning could yield additional capacity.
3. Evaluated multiple architectural approaches against actual workload characteristics. Assessed read replica distribution, workload-specific partitioning, and a purpose-built service extraction against the platform's real query patterns rather than defaulting to a generic pattern.
4. Built the business case around the cost of inaction. Presented the capacity model, load testing results, and projected timeline until growth would exceed the ceiling regardless of further tuning investment.
5. Designed and validated the new architecture against projected growth. Sized the target architecture against the multi-year projection and validated it through load testing simulating future traffic volume before full implementation.
6. Executed a phased migration with continuous production validation. Migrated specific workload components incrementally, validating real production performance against the capacity model's predictions at each stage.

</details>

**Root Cause**
The platform's architecture had been designed years earlier around a single, vertically scaled database and application tier, appropriate for its original scale but with a structural ceiling on additional capacity that no amount of further tuning could raise.

**Resolution**
Sized the target architecture against the multi-year projection and validated it through load testing simulating future traffic volume before full implementation. Migrated specific workload components incrementally, validating real production performance against the capacity model's predictions at each stage.

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
| **Average Time to Resolve** | ~2w 2d |
| **Systems Touched** | Unified Incident Timeline & Cross-Team Correlation · Live Dependency Graph Tracing · Infrastructure Metrics & Memory Utilization Monitoring · Code-Level Change Review & Deployment History · Staged Rollback & Dependency-Ordered Recovery Validation · Kernel Memory Dump Collection & Analysis · Kernel Debugging Tools · Fleet Software & Driver Version Inventory |

## Skills Demonstrated

`Cascading Outage Root Cause Analysis` · `Kernel / Firmware Conflict Diagnosis` · `Storage Firmware & Data Integrity` · `Database Engine-Level Corruption` · `Capacity Modeling & Architecture Redesign` · `Vendor Engineering Collaboration`

---

<div align="center">

*Built to demonstrate structured, repeatable troubleshooting methodology across deep infrastructure engineering — real-world Tier 3 scenarios, documented to enterprise standard.*

</div>