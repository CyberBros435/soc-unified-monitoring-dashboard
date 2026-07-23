# 🛡️ SOC Unified Monitoring Dashboard — Multi-Source Splunk Visualization

![Splunk](https://img.shields.io/badge/SIEM-Splunk-black?logo=splunk)
![Status](https://img.shields.io/badge/status-complete-brightgreen)
![License](https://img.shields.io/badge/license-MIT-blue)

Combined two unrelated log sources — Windows Security Event Logs and a
custom ransomware simulation log — into a single Splunk dashboard,
practicing the "single pane of glass" approach real SOC teams use to
monitor multiple detection domains at once.

**Full report:** [report.md](report.md)

---

## 📌 Table of Contents
- [Overview](#overview)
- [Why This Matters](#why-this-matters)
- [Data Sources](#data-sources)
- [Results Snapshot](#results-snapshot)
- [What I Learned](#what-i-learned)
- [Related Projects](#related-projects)

---

## Overview

| | |
|---|---|
| **Goal** | Merge two independent log sources into one unified dashboard |
| **SIEM** | Splunk Enterprise (local lab) |
| **Panels** | 2 (Ransomware Event Breakdown, Failed Logon Sources) |
| **Skill Focus** | Multi-source dashboard design, SOC monitoring UX |

## Why This Matters
A real SOC analyst never watches one log type in isolation — they need
one screen showing multiple unrelated risk signals simultaneously
(auth failures, file integrity events, network anomalies, etc.). This
project simulates that by merging two independently-built detections
into a single dashboard view.

## Data Sources
| Panel | Source | Query Type |
|---|---|---|
| Ransomware Event Breakdown | `ransom_activity_analysis` (custom JSON log) | `stats count by event_type` |
| Failed Logon Sources | `WinEventLog:Security` (EventCode 4625) | `stats count by Security_ID` |

## Results Snapshot

**Ransomware Events**
| event_type | count |
|---|---|
| file_decrypted | 14 |
| file_encrypted | 14 |
| decrypt_complete | 2 |
| file_skipped | 2 |
| ransom_complete | 2 |
| ransom_init | 2 |

**Failed Logons**
| Security_ID | Count | Identity |
|---|---|---|
| S-1-0-0 | 5 | Null SID |
| S-1-5-18 | 5 | LOCAL SYSTEM |

*(Full build steps, screenshots, and findings in [report.md](report.md))*

## What I Learned
- Dashboards in Splunk are containers — each panel pulls from a completely different index/sourcetype/query independently, no schema normalization needed.
- "Unified monitoring" ≠ correlating data together — it means presenting multiple independent signals side-by-side for faster human triage.
- Different chart types per panel (bar vs. pie) help visually distinguish unrelated data domains at a glance.

## Next Steps
- [ ] Add a third panel from a different log source
- [ ] Build a real **correlation search** linking events across sources by host/time window

## Related Projects
- 🔗 [Ransomware Detection & MITRE Mapping](https://github.com/CyberBros435/ransomware-siem-analysis)
- 🔗 [Failed Logon Frequency Analysis](https://github.com/CyberBros435/System_Log_Analyser)
- 🔗 [Single-Panel Dashboard (v1)](https://github.com/CyberBros435/soc-dashboard-splunk-visualization)

---

**Author**: Mudasir Zia | [GitHub](https://github.com/CyberBros435) | [LinkedIn](https://linkedin.com/in/mudasir-zia-a535243b5)
