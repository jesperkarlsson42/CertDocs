# SC-200 Cheat Sheet

## Microsoft Sentinel

| Keyword | Association |
|---------|------------|
| SIEM + SOAR | Microsoft Sentinel |
| Log collection | Data connectors |
| Analytic rules | Detect threats, create incidents |
| Watchlists | Import CSV reference data for queries |
| Threat intelligence | TI indicators (IoCs) fed into Sentinel |
| Workbooks | Dashboards & visualisations |
| Hunting queries | Proactive KQL-based threat hunting |
| Livestream | Real-time hunting session |
| Notebooks | Jupyter notebooks for advanced investigation |
| Playbooks | Logic Apps triggered by automation rules |
| Automation rules | Triage/auto-close/assign incidents, run playbooks |
| UEBA | User & Entity Behavior Analytics |
| Entity pages | Aggregated view of user/host/IP activity |
| Repositories | CI/CD for Sentinel content (GitHub/Azure DevOps) |
| Content hub | Install packaged solutions & standalone content |
| Near-real-time (NRT) rules | Run every 1 min, lowest latency analytic rules |
| Fusion | ML-based multi-stage attack detection (built-in) |
| Workspace manager | Manage multiple Sentinel workspaces at scale |
| Data collection rules (DCR) | Filter/transform logs before ingestion |
| Log types: Analytics / Basic / Archive | Cost tiers – Analytics (full KQL), Basic (limited KQL, 8-day default), Archive (restore to query) |
| CEF / Syslog | Collected via AMA + DCR on Linux forwarder |

---

## Microsoft Defender XDR

| Keyword | Association |
|---------|------------|
| Defender for Endpoint (MDE) | Devices – EDR, ASR, TVM |
| Defender for Office 365 (MDO) | Email & collaboration – Safe Links, Safe Attachments |
| Defender for Identity (MDI) | On-prem Active Directory – lateral movement, pass-the-hash |
| Defender for Cloud Apps (MDA) | CASB – shadow IT, app governance, session policies |
| Unified incidents | Correlated alerts across all Defender products |
| Advanced hunting | KQL across Defender XDR tables |
| Threat analytics | Reports on active threat campaigns |
| Action center | Approve/reject pending automated actions |
| AIR | Automated Investigation & Response |
| Live response | Remote shell on endpoint for investigation |
| Device groups | Scope RBAC & automation to subsets of devices |
| Indicators (IoCs) | Allow/block hashes, IPs, URLs, certs |
| ASR rules | Attack Surface Reduction – block Office macros, scripts, etc. |
| TVM | Threat & Vulnerability Management – prioritised recommendations |
| Web content filtering | Block site categories on endpoints |
| Device isolation | Network-isolate a compromised device |
| Secure score | Posture improvement recommendations |

---

## Microsoft Defender for Cloud

| Keyword | Association |
|---------|------------|
| CSPM | Cloud Security Posture Management – misconfigurations |
| CWPP | Cloud Workload Protection – runtime threat detection |
| Defender plans | Per-resource: Servers, Storage, SQL, Containers, App Service, Key Vault, DNS, ARM |
| Secure score | Measure & improve cloud posture |
| Recommendations | Remediation steps for misconfigurations |
| Regulatory compliance | Map controls to standards (CIS, NIST, PCI-DSS) |
| Security alerts | Threat detections from Defender plans |
| Just-In-Time (JIT) VM access | Lock down management ports, open on request |
| Adaptive application controls | Whitelist allowed processes on VMs |
| Adaptive network hardening | NSG rule recommendations |
| File integrity monitoring (FIM) | Track changes to critical OS/app files |
| Agentless scanning | Disk snapshot-based vulnerability & secret scanning |
| Auto-provisioning | Automatically deploy agents/extensions |
| Governance rules | Assign owners & deadlines to recommendations |
| Attack path analysis | Graph-based risk prioritisation (Defender CSPM) |
| Cloud security explorer | Query cloud resource graph for risk |
| Workload protections | Alerts for servers, containers, databases, etc. |

---

## Microsoft Purview

| Keyword | Association |
|---------|------------|
| DLP | Data Loss Prevention – block sensitive data sharing |
| Sensitivity labels | Classify & protect docs/emails (encrypt, watermark) |
| Information barriers | Block communication between user groups |
| Insider risk management | Detect risky user behaviour (data theft, leaks) |
| eDiscovery | Legal hold, search, export content |
| Audit (Standard / Premium) | Log user & admin activity (Premium = longer retention) |
| Communication compliance | Monitor messages for policy violations |
| Data lifecycle management | Retention & deletion policies |

---

## Multi-Cloud, Third-Party & On-Prem Integration

### Sentinel Data Connectors

| Connector Type | Use Case |
|---------------|----------|
| Service-to-service | Azure AD, M365, Defender XDR (native, one-click) |
| CEF / Syslog (via AMA) | Firewalls, proxies, Linux appliances (Palo Alto, Fortinet, Check Point) |
| REST API / Logic App | Third-party SaaS with no built-in connector |
| Azure Functions connector | Custom polling from external APIs |
| AWS S3 connector | Ingest AWS CloudTrail, VPC Flow Logs, GuardDuty via S3 bucket |
| GCP Pub/Sub connector | Ingest Google Cloud audit & security logs |
| Custom logs (DCR-based) | Any text/JSON log via AMA + Data Collection Rule |
| Windows event forwarding | On-prem Windows servers via AMA or WEF |
| Codeless Connector Platform (CCP) | Build connectors via JSON config (no code) |

### Defender for Cloud – Multi-Cloud

| Feature | Detail |
|---------|--------|
| AWS account onboarding | Native connector – CSPM + Defender for Servers/Containers on AWS |
| GCP project onboarding | Native connector – CSPM + Defender for Servers/Containers on GCP |
| Arc-enabled servers | On-prem & multi-cloud VMs managed as Azure resources |
| Defender for Servers (Arc) | EDR, vulnerability assessment, FIM on non-Azure machines |
| Defender for SQL (Arc) | Threat detection for SQL Server on-prem or other clouds |
| Auto-provisioning (Arc) | Deploy MDE, AMA, VA extensions to Arc machines |

### Defender for Cloud Apps (MDA) – Third-Party SaaS

| Feature | Detail |
|---------|--------|
| Cloud discovery | Analyse firewall/proxy logs or MDE signals to find shadow IT |
| Log collector | Docker-based, deployed on-prem to upload firewall/proxy logs |
| App connectors | API-based: AWS, GCP, Salesforce, ServiceNow, Box, Dropbox, etc. |
| Conditional Access App Control | Reverse-proxy session control for any SAML/OIDC app |
| OAuth app governance | Detect overprivileged or malicious third-party OAuth apps |

### Key On-Prem Integrations

| Component | Detail |
|-----------|--------|
| Azure Arc | Extend Azure management to on-prem/multi-cloud servers & K8s |
| MDI sensor | Installed on domain controllers – monitors AD authentication |
| MDE on-prem | Onboard via local script, GPO, SCCM, or Intune |
| AD connect | Sync on-prem AD to Entra ID (required for MDI full coverage) |
| Log Analytics gateway | On-prem proxy for machines without direct internet access |

---

## KQL Essentials

| Operator | Use |
|----------|-----|
| `where` | Filter rows |
| `project` | Select/rename columns |
| `extend` | Add calculated columns |
| `summarize` | Aggregate (count, sum, avg, dcount) |
| `join` | Combine tables |
| `union` | Stack tables vertically |
| `render` | Visualise (timechart, barchart, piechart) |
| `let` | Declare variables / reusable sub-queries |
| `ago()` | Relative time – `ago(1h)`, `ago(7d)` |
| `has` / `contains` | String matching (has = whole word, faster) |
| `in` / `!in` | Match against a list of values |
| `parse` | Extract fields from unstructured text |
| `mv-expand` | Expand multi-value arrays into rows |
| `arg_max()` / `arg_min()` | Row with max/min value per group |
| `make_set()` / `make_list()` | Aggregate into array (unique / all) |

---

## Key Incident Response Flow

1. **Triage** – review incident, set severity/status/owner
2. **Investigate** – entity mapping, timeline, evidence graph
3. **Contain** – isolate device, disable user, block IoC
4. **Remediate** – remove malware, reset credentials, patch
5. **Post-incident** – close incident, update analytic rules, lessons learned

---

## Role-Based Access (RBAC) Quick Ref

| Role | Scope |
|------|-------|
| Security Reader | View-only across security portals |
| Security Operator | Manage alerts, read security settings, run response actions |
| Security Administrator | Full security config + everything Operator can do |
| Sentinel Contributor | Manage Sentinel resources (rules, workbooks, playbooks) |
| Sentinel Responder | Manage incidents (assign, change status) |
| Sentinel Reader | View incidents, workbooks, rules |
| Logic App Contributor | Required to run Sentinel playbooks |

---

## High-Value Exam Tips

- **Sentinel data connector** ≠ **analytic rule** – connector ingests data, analytic rule detects threats
- **Automation rule** runs first, then triggers **playbook** (Logic App)
- **Fusion** cannot be customised, only enabled/disabled
- **NRT rules** don't support entity mapping grouping by alert
- **MDE onboarding** = local script, GPO, Intune, or SCCM
- **MDA** discovers shadow IT via log upload or Defender for Endpoint integration
- **MDI sensor** installed on domain controllers or AD FS servers
- **JIT access** requires Defender for Servers Plan 2 (or P1 with limited features)
- **Secure score** exists in both Defender XDR and Defender for Cloud (different scopes)
- **Workbooks** = monitor, **Notebooks** = investigate (Jupyter)
- **Basic logs** = cheaper, limited KQL, 8-day interactive retention
- **Archive tier** = restore before querying, up to 12 years retention