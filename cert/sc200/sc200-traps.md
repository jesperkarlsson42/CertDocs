# SC-200 Exam Traps & Gotchas

Common traps and easily confused concepts that appear on the SC-200 exam.

---

## Sentinel – Things That Sound Alike But Aren't

| Trap | Clarification |
|------|--------------|
| Data connector vs Analytic rule | Connector **ingests** data; analytic rule **detects** threats in that data |
| Automation rule vs Playbook | Automation rule = lightweight triage (runs first); Playbook = Logic App (complex actions) |
| Workbook vs Notebook | Workbook = dashboard/monitoring; Notebook = Jupyter investigation |
| Hunting query vs Livestream | Hunting = on-demand query; Livestream = continuous real-time query |
| NRT rule vs Scheduled rule | NRT runs every 1 min (no custom schedule); Scheduled has configurable frequency |
| Fusion rule vs Custom rule | Fusion = ML multi-stage (enable/disable only); Custom = fully editable KQL |
| Watchlist vs Threat intelligence | Watchlist = reference data (CSV); TI = malicious indicators (IoCs) |
| Analytics tier vs Basic tier | Analytics = full KQL, 90-day default; Basic = limited KQL, 8-day default, cheaper |

---

## Automation & Playbook Traps

| Trap | Why it's wrong | Correct answer |
|------|---------------|----------------|
| "Playbook runs automatically on incident" | Playbooks don't self-trigger | An **automation rule** must trigger the playbook |
| "Security Reader can run playbooks" | Insufficient permissions | Need **Logic App Contributor** + **Sentinel Responder** |
| "Automation rules run in random order" | They have a defined order | Rules run by **order number** (lowest first) |
| "One automation rule per incident" | No limit | **Multiple** automation rules can fire on the same incident |

---

## Defender XDR Traps

| Trap | Why it's wrong | Correct answer |
|------|---------------|----------------|
| "MDE is installed on DCs for identity" | Wrong product | **MDI** sensor goes on domain controllers; MDE is for endpoints |
| "MDA needs an agent on endpoints" | MDA is agentless CASB | MDA uses **API connectors** and **MDE integration** for discovery |
| "Live response is enabled by default" | Security measure | Must be **enabled in advanced settings** first |
| "Device isolation cuts all connections" | Defender connection survives | Isolated device keeps **Defender cloud connection** for remote commands |
| "AIR always auto-remediates" | Depends on config | AIR can be set to **full auto, semi-auto, or no automation** per device group |
| "ASR rules and MDE onboarding are the same" | Different features | MDE onboarding enrolls the device; ASR rules are **separate policies** |

---

## Defender for Cloud Traps

| Trap | Why it's wrong | Correct answer |
|------|---------------|----------------|
| "JIT works on free tier" | Requires paid plan | JIT requires **Defender for Servers Plan 2** |
| "CSPM and CWPP are the same" | Different functions | CSPM = posture/misconfigurations; CWPP = runtime threat detection |
| "Secure score in Defender XDR = Defender for Cloud" | Different scopes | XDR = M365 security posture; Cloud = Azure/multi-cloud resource posture |
| "Defender for Cloud only works in Azure" | Multi-cloud support | Native connectors for **AWS and GCP** + **Azure Arc** for on-prem |
| "Agentless scanning requires agents" | Confusing name | It uses **disk snapshots** – no agent installed on the VM |

---

## MDI Traps

| Trap | Why it's wrong | Correct answer |
|------|---------------|----------------|
| "MDI sensor on a separate server" | Must be on DC | Sensor installs **directly on domain controllers** (or AD FS servers) |
| "MDI monitors endpoint processes" | Wrong scope | MDI monitors **AD authentication traffic** on domain controllers |
| "MDI works without AD Connect" | Partial coverage | Full coverage requires **AD Connect** syncing to Entra ID |

---

## KQL Traps

| Trap | Why it's wrong | Correct answer |
|------|---------------|----------------|
| `contains` is faster than `has` | Opposite is true | `has` is **faster** (whole-word match); `contains` is slower (substring) |
| `project` filters rows | Wrong operator | `project` selects **columns**; `where` filters **rows** |
| `summarize` keeps all columns | It aggregates | Only the `by` columns and aggregation functions survive `summarize` |
| `join` without `kind=` | Default may surprise | Default join kind is `innerunique` – deduplicates left side |
| `ago(7d)` returns a duration | Returns a datetime | `ago()` returns a **datetime** (now minus the duration) |

---

## Log & Data Traps

| Trap | Why it's wrong | Correct answer |
|------|---------------|----------------|
| "Basic logs support full KQL" | Limited operators | Basic logs only support `where`, `extend`, `project`, `summarize` – no `join` |
| "Archive tier can be queried directly" | Must restore first | Archive logs must be **restored** before querying |
| "CEF and Syslog go to the same table" | Different tables | CEF → `CommonSecurityLog`; Syslog → `Syslog` |
| "Legacy Log Analytics agent is current" | Deprecated | **Azure Monitor Agent (AMA)** with DCR is the current standard |
| "Free ingestion for all connectors" | Only some are free | Free: Azure Activity, Defender XDR alerts, Office 365 (partial). Most others are **paid** |

---

## RBAC Traps

| Trap | Why it's wrong | Correct answer |
|------|---------------|----------------|
| "Sentinel Reader can close incidents" | Read-only role | Need **Sentinel Responder** to manage incidents |
| "Security Operator = Security Admin" | Different permissions | Operator = manage alerts + response; Admin = full security config |
| "Sentinel Contributor can run playbooks" | Missing Logic App role | Also need **Logic App Contributor** to execute playbooks |
