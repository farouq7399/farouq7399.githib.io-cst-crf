# farouq7399.githib.io-cst-crf

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>CRF CST Framework — Interactive Mindmap</title>
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Sans:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
:root{--bg:#0a0e1a;--surface:#111827;--surface2:#1a2236;--border:#1e293b;--text:#e2e8f0;--text-dim:#94a3b8;--text-muted:#64748b;--d1:#f59e0b;--d1-bg:rgba(245,158,11,.08);--d1-border:rgba(245,158,11,.25);--d2:#06b6d4;--d2-bg:rgba(6,182,212,.08);--d2-border:rgba(6,182,212,.25);--d3:#ef4444;--d3-bg:rgba(239,68,68,.08);--d3-border:rgba(239,68,68,.25);--d4:#8b5cf6;--d4-bg:rgba(139,92,246,.08);--d4-border:rgba(139,92,246,.25);--d5:#10b981;--d5-bg:rgba(16,185,129,.08);--d5-border:rgba(16,185,129,.25);--d6:#f97316;--d6-bg:rgba(249,115,22,.08);--d6-border:rgba(249,115,22,.25);--cl1:#3b82f6;--cl2:#a855f7;--cl3:#f43f5e}
*{margin:0;padding:0;box-sizing:border-box}
body{font-family:'IBM Plex Sans',sans-serif;background:var(--bg);color:var(--text);min-height:100vh}
body::before{content:'';position:fixed;inset:0;background:radial-gradient(ellipse 80% 60% at 20% 10%,rgba(245,158,11,.04) 0%,transparent 60%),radial-gradient(ellipse 60% 50% at 80% 80%,rgba(139,92,246,.04) 0%,transparent 60%);pointer-events:none}
.app{position:relative;z-index:1;max-width:1400px;margin:0 auto;padding:2rem 1.5rem 4rem}
.header{text-align:center;margin-bottom:2.5rem;padding:2.5rem 2rem;background:linear-gradient(135deg,var(--surface),var(--surface2));border:1px solid var(--border);border-radius:20px;position:relative;overflow:hidden}
.header::after{content:'';position:absolute;top:0;left:0;right:0;height:3px;background:linear-gradient(90deg,var(--d1),var(--d2),var(--d3),var(--d4),var(--d5),var(--d6))}
.header h1{font-size:2rem;font-weight:700;letter-spacing:-.5px;margin-bottom:.4rem;background:linear-gradient(135deg,#fff 30%,var(--text-dim));-webkit-background-clip:text;-webkit-text-fill-color:transparent}
.header p{color:var(--text-dim);font-size:.95rem;font-weight:300}
.legend{display:flex;gap:1rem;justify-content:center;flex-wrap:wrap;margin-top:1.2rem}
.legend-item{display:flex;align-items:center;gap:.4rem;font-size:.78rem;font-family:'JetBrains Mono',monospace;font-weight:500}
.legend-dot{width:10px;height:10px;border-radius:3px}
.controls{display:flex;gap:.7rem;justify-content:center;margin-bottom:2rem;flex-wrap:wrap}
.ctrl-btn{background:var(--surface);border:1px solid var(--border);color:var(--text-dim);padding:.5rem 1.1rem;border-radius:10px;font-family:'IBM Plex Sans',sans-serif;font-size:.82rem;font-weight:500;cursor:pointer;transition:all .2s}
.ctrl-btn:hover{background:var(--surface2);color:var(--text);border-color:#334155}
.ctrl-btn.active{background:rgba(139,92,246,.15);border-color:var(--d4);color:var(--d4)}
.search-wrap{max-width:500px;margin:0 auto 2rem;position:relative}
.search-wrap input{width:100%;background:var(--surface);border:1px solid var(--border);color:var(--text);padding:.75rem 1rem .75rem 2.8rem;border-radius:12px;font-family:'IBM Plex Sans',sans-serif;font-size:.9rem;outline:none;transition:border-color .2s}
.search-wrap input:focus{border-color:#475569}
.search-wrap input::placeholder{color:var(--text-muted)}
.search-icon{position:absolute;left:1rem;top:50%;transform:translateY(-50%);color:var(--text-muted)}
.stats-bar{display:flex;gap:1.5rem;justify-content:center;flex-wrap:wrap;margin-bottom:2rem}
.stat{text-align:center}
.stat-num{font-family:'JetBrains Mono',monospace;font-size:1.6rem;font-weight:700;background:linear-gradient(135deg,#fff,var(--text-dim));-webkit-background-clip:text;-webkit-text-fill-color:transparent}
.stat-label{font-size:.72rem;color:var(--text-muted);text-transform:uppercase;letter-spacing:.5px}
.domain{margin-bottom:1.5rem;border-radius:16px;overflow:hidden;border:1px solid var(--border);transition:all .3s;animation:fadeIn .4s ease both}
.domain-header{padding:1.1rem 1.4rem;cursor:pointer;display:flex;align-items:center;gap:.9rem;user-select:none;transition:background .2s}
.domain-header:hover{filter:brightness(1.15)}
.domain-icon{font-size:1.5rem;width:44px;height:44px;display:flex;align-items:center;justify-content:center;border-radius:12px;flex-shrink:0}
.domain-title{font-size:1.1rem;font-weight:600;flex:1}
.domain-count{font-family:'JetBrains Mono',monospace;font-size:.72rem;padding:.2rem .6rem;border-radius:6px;font-weight:500}
.domain-chevron{font-size:1.2rem;transition:transform .3s;color:var(--text-muted)}
.domain.open .domain-chevron{transform:rotate(180deg)}
.domain-body{max-height:0;overflow:hidden;transition:max-height .4s ease}
.domain.open .domain-body{max-height:20000px}
.domain-inner{padding:0 1.2rem 1.2rem}
.subdomain{margin-bottom:.8rem;border-radius:12px;overflow:hidden;transition:all .25s}
.subdomain-header{padding:.8rem 1rem;cursor:pointer;display:flex;align-items:center;gap:.7rem;border-radius:12px;user-select:none;transition:background .15s}
.subdomain-header:hover{filter:brightness(1.2)}
.sub-icon{font-size:1.1rem;width:32px;text-align:center;flex-shrink:0}
.sub-title{font-size:.92rem;font-weight:500;flex:1}
.sub-count{font-family:'JetBrains Mono',monospace;font-size:.68rem;padding:.15rem .5rem;border-radius:5px;font-weight:500}
.sub-chevron{font-size:.9rem;transition:transform .25s;color:var(--text-muted)}
.subdomain.open .sub-chevron{transform:rotate(180deg)}
.sub-body{max-height:0;overflow:hidden;transition:max-height .35s ease}
.subdomain.open .sub-body{max-height:8000px}
.sub-inner{padding:.4rem .6rem .6rem 2.8rem}
.control-item{padding:.65rem .9rem;margin-bottom:.35rem;border-radius:8px;background:rgba(255,255,255,.02);border:1px solid transparent;transition:all .2s}
.control-item:hover{background:rgba(255,255,255,.04);border-color:rgba(255,255,255,.06)}
.control-item.match{background:rgba(245,158,11,.1);border-color:rgba(245,158,11,.3)}
.ctrl-top{display:flex;align-items:center;gap:.6rem;margin-bottom:.25rem}
.ctrl-id{font-family:'JetBrains Mono',monospace;font-size:.72rem;font-weight:500;color:var(--text-muted);min-width:42px}
.cl-badge{font-family:'JetBrains Mono',monospace;font-size:.62rem;font-weight:500;padding:.1rem .45rem;border-radius:4px;letter-spacing:.3px}
.cl-badge.cl1{background:rgba(59,130,246,.15);color:var(--cl1)}
.cl-badge.cl2{background:rgba(168,85,247,.15);color:var(--cl2)}
.cl-badge.cl3{background:rgba(244,63,94,.15);color:var(--cl3)}
.ctrl-name{font-size:.85rem;font-weight:500;color:var(--text)}
.ctrl-keywords{font-size:.76rem;color:var(--text-muted);line-height:1.5;padding-left:.2rem}
.ctrl-keywords span{display:inline-block;background:rgba(255,255,255,.04);padding:.1rem .45rem;border-radius:4px;margin:.12rem .15rem;font-family:'JetBrains Mono',monospace;font-size:.7rem;border:1px solid rgba(255,255,255,.05);transition:all .15s}
.ctrl-keywords span.hl{background:rgba(245,158,11,.15);border-color:rgba(245,158,11,.3);color:var(--d1)}
.d1 .domain-header{background:var(--d1-bg)}.d1 .domain-icon{background:rgba(245,158,11,.15)}.d1 .domain-title{color:var(--d1)}.d1 .domain-count{background:rgba(245,158,11,.12);color:var(--d1)}.d1 .subdomain-header{background:rgba(245,158,11,.04)}.d1 .sub-count{background:rgba(245,158,11,.1);color:var(--d1)}.d1{border-color:var(--d1-border)}
.d2 .domain-header{background:var(--d2-bg)}.d2 .domain-icon{background:rgba(6,182,212,.15)}.d2 .domain-title{color:var(--d2)}.d2 .domain-count{background:rgba(6,182,212,.12);color:var(--d2)}.d2 .subdomain-header{background:rgba(6,182,212,.04)}.d2 .sub-count{background:rgba(6,182,212,.1);color:var(--d2)}.d2{border-color:var(--d2-border)}
.d3 .domain-header{background:var(--d3-bg)}.d3 .domain-icon{background:rgba(239,68,68,.15)}.d3 .domain-title{color:var(--d3)}.d3 .domain-count{background:rgba(239,68,68,.12);color:var(--d3)}.d3 .subdomain-header{background:rgba(239,68,68,.04)}.d3 .sub-count{background:rgba(239,68,68,.1);color:var(--d3)}.d3{border-color:var(--d3-border)}
.d4 .domain-header{background:var(--d4-bg)}.d4 .domain-icon{background:rgba(139,92,246,.15)}.d4 .domain-title{color:var(--d4)}.d4 .domain-count{background:rgba(139,92,246,.12);color:var(--d4)}.d4 .subdomain-header{background:rgba(139,92,246,.04)}.d4 .sub-count{background:rgba(139,92,246,.1);color:var(--d4)}.d4{border-color:var(--d4-border)}
.d5 .domain-header{background:var(--d5-bg)}.d5 .domain-icon{background:rgba(16,185,129,.15)}.d5 .domain-title{color:var(--d5)}.d5 .domain-count{background:rgba(16,185,129,.12);color:var(--d5)}.d5 .subdomain-header{background:rgba(16,185,129,.04)}.d5 .sub-count{background:rgba(16,185,129,.1);color:var(--d5)}.d5{border-color:var(--d5-border)}
.d6 .domain-header{background:var(--d6-bg)}.d6 .domain-icon{background:rgba(249,115,22,.15)}.d6 .domain-title{color:var(--d6)}.d6 .domain-count{background:rgba(249,115,22,.12);color:var(--d6)}.d6 .subdomain-header{background:rgba(249,115,22,.04)}.d6 .sub-count{background:rgba(249,115,22,.1);color:var(--d6)}.d6{border-color:var(--d6-border)}
.domain.hidden,.subdomain.hidden,.control-item.hidden{display:none}
@keyframes fadeIn{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:translateY(0)}}
@media(max-width:700px){.app{padding:1rem .8rem 3rem}.header h1{font-size:1.4rem}.sub-inner{padding-left:1rem}}
</style>
</head>
<body>
<div class="app">
<div class="header">
<h1>🏛️ CST CRF Cybersecurity Controls</h1>
<p>Complete CSR Framework — 6 Domains · 29 Subdomains · 114 Controls</p>
<div class="legend">
<div class="legend-item"><div class="legend-dot" style="background:var(--cl1)"></div> CL1 — Basic</div>
<div class="legend-item"><div class="legend-dot" style="background:var(--cl2)"></div> CL2 — Advanced</div>
<div class="legend-item"><div class="legend-dot" style="background:var(--cl3)"></div> CL3 — Optimize</div>
</div>
</div>
<div class="stats-bar">
<div class="stat"><div class="stat-num" id="cl1Count">0</div><div class="stat-label">CL1 Controls</div></div>
<div class="stat"><div class="stat-num" id="cl2Count">0</div><div class="stat-label">CL2 Controls</div></div>
<div class="stat"><div class="stat-num" id="cl3Count">0</div><div class="stat-label">CL3 Controls</div></div>
</div>
<div class="search-wrap">
<span class="search-icon">🔍</span>
<input type="text" id="searchInput" placeholder="Search controls, keywords, IDs…" />
</div>
<div class="controls">
<button class="ctrl-btn active" data-filter="all">All</button>
<button class="ctrl-btn" data-filter="cl1">CL1 Only</button>
<button class="ctrl-btn" data-filter="cl2">CL2 Only</button>
<button class="ctrl-btn" data-filter="cl3">CL3 Only</button>
<button class="ctrl-btn" id="expandAll">⊞ Expand All</button>
<button class="ctrl-btn" id="collapseAll">⊟ Collapse All</button>
</div>
<div id="mindmap"></div>
</div>
<script>
const DATA=[
{id:1,title:"Governance",icon:"🏛️",cls:"d1",subs:[
{id:"1.1",title:"Cybersecurity Strategy",icon:"🎯",controls:[
{id:"1.1.1",cl:1,name:"Define Cybersecurity Strategy",kw:["mission/objectives","regulatory requirements","cybersecurity program","top-management commitment"]},
{id:"1.1.2",cl:1,name:"Approve Strategy",kw:["formal approval","executive sign-off"]},
{id:"1.1.3",cl:1,name:"Strategy Action Plan",kw:["activities","budget","timeline","resources"]},
{id:"1.1.4",cl:3,name:"Update Strategy",kw:["measure","review","update","regulatory changes","lessons learned"]}
]},
{id:"1.2",title:"Cybersecurity Management",icon:"⚙️",controls:[
{id:"1.2.1",cl:1,name:"Define Cybersecurity Organization",kw:["committee","functions","direct reporting to top mgmt","segregation of duties (SoD)"]},
{id:"1.2.2",cl:1,name:"Implement Cybersecurity Organization",kw:["org structure","mandate","operating model"]},
{id:"1.2.3",cl:1,name:"Execute Action Plan",kw:["plan execution","tracking","accountability"]},
{id:"1.2.4",cl:1,name:"Oversee Implementation",kw:["oversight","issue resolution","escalation"]},
{id:"1.2.5",cl:3,name:"Optimize Organization",kw:["KPIs","effectiveness","optimization"]}
]},
{id:"1.3",title:"Cybersecurity Compliance",icon:"📋",controls:[
{id:"1.3.1",cl:1,name:"Define Requirements for Compliance",kw:["national","international/cross-border","internal requirements"]},
{id:"1.3.2",cl:1,name:"Compliance Process",kw:["change detection","impact","communication"]},
{id:"1.3.3",cl:1,name:"Incorporate Requirements",kw:["control mapping","policy updates","awareness"]},
{id:"1.3.4",cl:3,name:"Improve Compliance",kw:["effectiveness review","continual improvement"]}
]},
{id:"1.4",title:"Cybersecurity Audit",icon:"🔍",controls:[
{id:"1.4.1",cl:2,name:"Audit Requirements",kw:["independence","periodicity","protect/retain audit records","report to top mgmt"]},
{id:"1.4.2",cl:2,name:"Internal Audit Process",kw:["scope","methodology","sampling"]},
{id:"1.4.3",cl:2,name:"Conduct Audits",kw:["plan","trigger events"]},
{id:"1.4.4",cl:2,name:"Audit Reporting",kw:["reports","corrective actions"]},
{id:"1.4.5",cl:2,name:"Protect Audit Records",kw:["tamper-proof","restricted access"]},
{id:"1.4.6",cl:2,name:"Retain Records",kw:["retention period","storage"]},
{id:"1.4.7",cl:3,name:"Improve Audit Program",kw:["trend analysis","closure rate"]}
]},
{id:"1.5",title:"Awareness & Training (Personnel)",icon:"🎓",controls:[
{id:"1.5.1",cl:1,name:"Define Awareness & Training Req.",kw:["goals","scope","frequency","resources"]},
{id:"1.5.2",cl:1,name:"Awareness & Training Program",kw:["roles/responsibilities","phishing/social engineering","acceptable use","clear desk/screen"]},
{id:"1.5.3",cl:2,name:"Validation Tests",kw:["simulated phishing","metrics"]},
{id:"1.5.4",cl:2,name:"Triggered Training",kw:["onboarding","role-based triggers"]},
{id:"1.5.5",cl:2,name:"Role-Based Training",kw:["cyber","IT ops","developers","privileged users","executives"]},
{id:"1.5.6",cl:3,name:"Improve Program",kw:["feedback loop","continuous update"]}
]},
{id:"1.6",title:"Customer Cybersecurity Awareness",icon:"📢",controls:[
{id:"1.6.1",cl:1,name:"Define Customer Awareness Req.",kw:["goals","scope","frequency","channels"]},
{id:"1.6.2",cl:1,name:"Implement Customer Awareness",kw:["emerging threats","service-specific tips"]},
{id:"1.6.3",cl:2,name:"Periodic Delivery",kw:["schedule","campaign"]},
{id:"1.6.4",cl:3,name:"Improve Customer Program",kw:["measure reach/effectiveness"]}
]},
{id:"1.7",title:"Cybersecurity in Project Mgmt",icon:"📊",controls:[
{id:"1.7.1",cl:1,name:"Requirements for Security in PM",kw:["security roles in project team","project security objectives"]},
{id:"1.7.2",cl:1,name:"Project Risk Assessment",kw:["risk identification","mitigation plans"]},
{id:"1.7.3",cl:2,name:"Track Project Risks",kw:["risk register updates","status tracking"]},
{id:"1.7.4",cl:3,name:"Improve Security in PM",kw:["lessons learned","process updates"]}
]},
{id:"1.8",title:"Cybersecurity in Human Resources",icon:"👥",controls:[
{id:"1.8.1",cl:1,name:"HR Security Requirements",kw:["pre-employment checks","competency for critical roles","NDAs","code of conduct","acceptable use"]},
{id:"1.8.2",cl:1,name:"Access on Role Change",kw:["modify authorizations","least privilege"]},
{id:"1.8.3",cl:1,name:"Investigate Breaches",kw:["disciplinary process","evidence"]},
{id:"1.8.4",cl:1,name:"Termination Controls",kw:["revoke access","retrieve assets","retain needed access to org info"]},
{id:"1.8.5",cl:3,name:"Improve HR Security",kw:["process maturity","KPI"]}
]}
]},
{id:2,title:"Asset Management",icon:"📦",cls:"d2",subs:[
{id:"2.1",title:"Asset Discovery",icon:"🔎",controls:[
{id:"2.1.1",cl:1,name:"Asset Inventory Requirements",kw:["scope (HW/SW/data)","update frequency","ownership"]},
{id:"2.1.2",cl:1,name:"Asset Discovery Process",kw:["tooling","identification","assign owner"]},
{id:"2.1.3",cl:1,name:"Inventory Maintenance",kw:["review/update on change"]},
{id:"2.1.4",cl:2,name:"Automated Discovery & Central Tracking",kw:["CMDB","auto-discovery","single source"]},
{id:"2.1.5",cl:3,name:"Improve Discovery",kw:["coverage","accuracy metrics"]}
]},
{id:"2.2",title:"Asset Classification",icon:"🏷️",controls:[
{id:"2.2.1",cl:1,name:"Classification Requirements",kw:["classify","label","handling rules"]},
{id:"2.2.2",cl:1,name:"Asset Classification Process",kw:["criteria (criticality, business value, CIA, legal)"]},
{id:"2.2.3",cl:3,name:"Improve Classification",kw:["periodic re-eval"]}
]},
{id:"2.3",title:"BYOD",icon:"📱",controls:[
{id:"2.3.1",cl:1,name:"BYOD Requirements",kw:["isolation (personal/org)","restricted use","restricted critical access","secure deletion"]},
{id:"2.3.2",cl:1,name:"Enforce BYOD",kw:["MDM/MAM","policy enforcement"]},
{id:"2.3.3",cl:1,name:"Secure Deletion of Org Data",kw:["wipe on exit/change"]},
{id:"2.3.4",cl:2,name:"Encrypt Org Data on BYOD",kw:["device/container encryption"]},
{id:"2.3.5",cl:3,name:"Improve BYOD",kw:["monitor","reporting"]}
]},
{id:"2.4",title:"Acceptable Use of Info Assets",icon:"✅",controls:[
{id:"2.4.1",cl:1,name:"Acceptable Use Requirements",kw:["rules of use","prohibited actions"]},
{id:"2.4.2",cl:1,name:"Enforce Acceptable Use",kw:["SW install control","web control","removable media by need"]},
{id:"2.4.3",cl:3,name:"Improve AUP",kw:["compliance checks"]}
]},
{id:"2.5",title:"Asset Maintenance",icon:"🔧",controls:[
{id:"2.5.1",cl:2,name:"Maintenance Requirements",kw:["maintenance","tracking/monitoring","recovery plan"]},
{id:"2.5.2",cl:2,name:"Maintenance Process & Logs",kw:["on-prem & offsite","logging"]},
{id:"2.5.3",cl:2,name:"Execute Recovery",kw:["during/after incident","per plan"]},
{id:"2.5.4",cl:2,name:"Monitor by Classification",kw:["risk-based monitoring"]},
{id:"2.5.5",cl:3,name:"Improve Maintenance",kw:["effectiveness metrics"]}
]},
{id:"2.6",title:"Secure Disposal of Assets",icon:"🗑️",controls:[
{id:"2.6.1",cl:1,name:"Disposal Requirements",kw:["rules per classification/label"]},
{id:"2.6.2",cl:1,name:"Secure Disposal Process",kw:["secure erase","shredding","drilling","prevent disclosure"]},
{id:"2.6.3",cl:3,name:"Improve Disposal",kw:["audit trail","certificates"]}
]}
]},
{id:3,title:"Cybersecurity Risk Management",icon:"⚠️",cls:"d3",subs:[
{id:"3.1",title:"Risk Assessment",icon:"📐",controls:[
{id:"3.1.1",cl:1,name:"Risk Assessment Requirements",kw:["purpose","scope","frequency","cover org/individual/third-party risk"]},
{id:"3.1.2",cl:1,name:"Risk Assessment Process",kw:["identify","analyze","evaluate","Risk Register","report top risks to regulator"]},
{id:"3.1.3",cl:2,name:"Integrate Risk Assessment",kw:["projects","major changes","new products/services"]},
{id:"3.1.4",cl:3,name:"Improve Risk Assessment",kw:["quality checks","calibration"]}
]},
{id:"3.2",title:"Risk Treatment & Monitoring",icon:"🛡️",controls:[
{id:"3.2.1",cl:1,name:"Treatment & Monitoring Requirements",kw:["treatment plan","monitoring plan"]},
{id:"3.2.2",cl:1,name:"Risk Treatment Process",kw:["Risk Treatment Plan","mitigate/transfer/accept/avoid"]},
{id:"3.2.3",cl:1,name:"Risk Monitoring Process",kw:["track implementation","residual risk","accepted risk"]},
{id:"3.2.4",cl:3,name:"Improve Treatment & Monitoring",kw:["dashboards","thresholds"]}
]}
]},
{id:4,title:"Logical Security",icon:"🔐",cls:"d4",subs:[
{id:"4.1",title:"Cryptography",icon:"🔑",controls:[
{id:"4.1.1",cl:1,name:"Crypto Requirements",kw:["approved algorithms/protocols","prohibited legacy","where to apply (transit/rest/use)"]},
{id:"4.1.2",cl:1,name:"Cryptographic Solutions List",kw:["products","algorithms","protocols","approvals"]},
{id:"4.1.3",cl:1,name:"Apply Cryptography",kw:["by classification","full data lifecycle"]},
{id:"4.1.4",cl:2,name:"Key Lifecycle Management",kw:["generation","protection","archiving","recovery","destruction"]},
{id:"4.1.5",cl:3,name:"Improve Crypto",kw:["periodic review","updates"]}
]},
{id:"4.2",title:"Change Management",icon:"🔄",controls:[
{id:"4.2.1",cl:1,name:"Change Requirements",kw:["identify","classify","prioritize changes"]},
{id:"4.2.2",cl:1,name:"Change Process",kw:["authorization for cyber-relevant changes"]},
{id:"4.2.3",cl:1,name:"Plan/Test/Risk-Assess Changes",kw:["testing","risk assessment","communication","formal approval"]},
{id:"4.2.4",cl:2,name:"Emergency Changes",kw:["procedure","documentation"]},
{id:"4.2.5",cl:3,name:"Improve Change Management",kw:["post-implementation review"]}
]},
{id:"4.3",title:"Vulnerability Management",icon:"🐛",controls:[
{id:"4.3.1",cl:1,name:"VM Requirements",kw:["scope","tools","reporting","scan frequency","remediation timeframes"]},
{id:"4.3.2",cl:1,name:"VM Process",kw:["scan","analyze (impact/criticality)","Vulnerabilities Report","recommended actions"]},
{id:"4.3.3",cl:2,name:"Event-Triggered Scans",kw:["releases","major changes","new equipment"]},
{id:"4.3.4",cl:2,name:"Specialized/Automated Tools",kw:["web/mobile/app-specific scanners"]},
{id:"4.3.5",cl:3,name:"Enhanced Classification/Reporting",kw:["threat intel","pentest inputs"]},
{id:"4.3.6",cl:3,name:"Improve VM",kw:["coverage","SLA adherence"]}
]},
{id:"4.4",title:"Patch Management",icon:"🩹",controls:[
{id:"4.4.1",cl:1,name:"Patch Requirements",kw:["scope","tools/triggers","test environment","frequency"]},
{id:"4.4.2",cl:1,name:"Patch Process & Remediation Plan",kw:["use VM/Risk inputs","test","backups","regular patch cycles"]},
{id:"4.4.3",cl:2,name:"Verify Patching",kw:["validate installed patches","close vulnerabilities"]},
{id:"4.4.4",cl:2,name:"Emergency Patch",kw:["critical vulnerabilities"]},
{id:"4.4.5",cl:2,name:"Regular Patches for All Assets",kw:["completeness","cadence"]},
{id:"4.4.6",cl:2,name:"Automate & Enforce",kw:["endpoints/servers automation"]},
{id:"4.4.7",cl:2,name:"Threat-Informed Prioritization",kw:["TI/pentest feed"]},
{id:"4.4.8",cl:3,name:"Improve Patch Program",kw:["metrics","compliance rates"]}
]},
{id:"4.5",title:"Network Security",icon:"🌐",controls:[
{id:"4.5.1",cl:1,name:"Network Security Requirements",kw:["network control","segregation","protect network services/data"]},
{id:"4.5.2",cl:1,name:"Network Plan (As-Built)",kw:["connections","devices","critical servers"]},
{id:"4.5.3",cl:1,name:"Control Traffic",kw:["block malicious","monitor loads","control unwanted comms"]},
{id:"4.5.4",cl:1,name:"Trusted Protocols & IPs Only",kw:["firewalls","disable unused (e.g. IPv6)"]},
{id:"4.5.5",cl:1,name:"Protect Data in Transit",kw:["encryption","integrity"]},
{id:"4.5.6",cl:1,name:"Segmentation",kw:["zones/subnets","prod vs dev/test","users vs auth servers"]},
{id:"4.5.7",cl:1,name:"Restrict Network Access",kw:["ACL/NAC","IAM alignment"]},
{id:"4.5.8",cl:1,name:"Protect Telco Traffic",kw:["VoIP/SIP","SS7"]},
{id:"4.5.9",cl:1,name:"Segregate Customer vs Ops Networks",kw:["hosted customer separation"]},
{id:"4.5.10",cl:2,name:"Cooperate to Block Abuse",kw:["spam","DDoS","spoofing","caller ID auth"]},
{id:"4.5.11",cl:2,name:"Secure Interconnects/IXPs",kw:["BGP security","redundancy","strong crypto"]},
{id:"4.5.12",cl:2,name:"Handle DoS/DDoS",kw:["internal/external defenses"]},
{id:"4.5.13",cl:2,name:"Avoid Congestion",kw:["capacity","load balancing"]},
{id:"4.5.14",cl:2,name:"Analyze/Filter Traffic",kw:["port/host-based filtering","anomaly detection"]},
{id:"4.5.15",cl:3,name:"Improve Network Security",kw:["maturity","KPIs"]}
]},
{id:"4.6",title:"Logging & Monitoring",icon:"📡",controls:[
{id:"4.6.1",cl:1,name:"L&M Requirements",kw:["events to log","monitoring","retention","log protection"]},
{id:"4.6.2",cl:1,name:"Activate Logging",kw:["user","exceptions","security","privileged ops"]},
{id:"4.6.3",cl:1,name:"Protect Logs/Facilities",kw:["access control","integrity"]},
{id:"4.6.4",cl:1,name:"Periodic Review & Escalation",kw:["suspicious events to IR"]},
{id:"4.6.5",cl:1,name:"Log Retention",kw:["retention period (e.g. 12 months)"]},
{id:"4.6.6",cl:2,name:"SIEM/Log Mgmt Tool",kw:["correlation","integration"]},
{id:"4.6.7",cl:2,name:"Real-Time on Critical Assets",kw:["continuous monitoring"]},
{id:"4.6.8",cl:2,name:"Improve Detection with TI",kw:["rules updates","intel feeds"]},
{id:"4.6.9",cl:3,name:"Improve L&M",kw:["alert quality","MTTR"]}
]},
{id:"4.7",title:"Identity & Access Management",icon:"🪪",controls:[
{id:"4.7.1",cl:1,name:"IAM Requirements",kw:["user/privileged accounts","grant/revoke","authN/Z","passwords"]},
{id:"4.7.2",cl:1,name:"Allocate/Revoke User Rights",kw:["RBAC","least privilege","need-to-know/use","ACL","revoke on exit"]},
{id:"4.7.3",cl:1,name:"Control Privileged Access",kw:["PAM principles","session control"]},
{id:"4.7.4",cl:1,name:"MFA for Critical/Remote",kw:["strong authentication"]},
{id:"4.7.5",cl:1,name:"Password Management",kw:["complexity","rotation","lockouts","secure transmission"]},
{id:"4.7.6",cl:2,name:"Periodic Access Reviews",kw:["owner reviews","recertification"]},
{id:"4.7.7",cl:2,name:"Automate/Centralize IAM",kw:["provisioning","SSO","central policy"]},
{id:"4.7.8",cl:2,name:"Dedicated Admin Systems",kw:["jump servers","admin VMs"]},
{id:"4.7.9",cl:3,name:"Improve IAM",kw:["metrics","anomaly-based controls"]}
]},
{id:"4.8",title:"Application Whitelisting",icon:"✔️",controls:[
{id:"4.8.1",cl:1,name:"Whitelisting Requirements",kw:["authorized software list","approved tools"]},
{id:"4.8.2",cl:1,name:"Index of Authorized Software",kw:["apps","libraries (DLL/SO)","signed scripts (PS1/PY/macros)"]},
{id:"4.8.3",cl:1,name:"Review/Update Index",kw:["periodic updates"]},
{id:"4.8.4",cl:2,name:"Enforce with Tools",kw:["cannot be disabled/bypassed"]},
{id:"4.8.5",cl:3,name:"Improve Whitelisting",kw:["coverage","exceptions mgmt"]}
]},
{id:"4.9",title:"Incident Management",icon:"🚨",controls:[
{id:"4.9.1",cl:1,name:"Incident Mgmt Requirements",kw:["definition","classification/prioritization","reporting","testing","evidence","lessons"]},
{id:"4.9.2",cl:1,name:"Incident Response Process",kw:["detect","classify","contain","eradicate","recover","report to regulator","lessons learned"]},
{id:"4.9.3",cl:1,name:"IR Training/Testing",kw:["tabletops","communication tests"]},
{id:"4.9.4",cl:2,name:"IR Tools & Integration",kw:["automation","ticketing","SIEM/SOAR integration"]},
{id:"4.9.5",cl:2,name:"Threat Intelligence Use",kw:["analysis enhancement"]},
{id:"4.9.6",cl:2,name:"Forensics Capability",kw:["investigation","imaging"]},
{id:"4.9.7",cl:2,name:"Evidence Handling",kw:["preservation","chain of custody"]},
{id:"4.9.8",cl:3,name:"Improve IR",kw:["MTTD/MTTR reduction"]}
]},
{id:"4.10",title:"Malware Handling",icon:"🦠",controls:[
{id:"4.10.1",cl:1,name:"Malware Requirements",kw:["detection","prevention","technical safeguards"]},
{id:"4.10.2",cl:1,name:"Endpoint Protection",kw:["signature/EDR","update","not user-disablable"]},
{id:"4.10.3",cl:1,name:"Block Malicious Sources",kw:["web filters","email filters","download restrictions"]},
{id:"4.10.4",cl:1,name:"Scan Removable Media",kw:["on insert/connect"]},
{id:"4.10.5",cl:2,name:"DNS Query Logging",kw:["malicious domain lookups"]},
{id:"4.10.6",cl:2,name:"Advanced Monitoring/Alerts",kw:["malware event analytics"]},
{id:"4.10.7",cl:3,name:"Improve Malware Program",kw:["detection efficacy"]}
]},
{id:"4.11",title:"Information Protection",icon:"🔒",controls:[
{id:"4.11.1",cl:1,name:"Information Protection Requirements",kw:["classification levels","privacy/ownership","transmission","retention","PII"]},
{id:"4.11.2",cl:1,name:"Information Classification Process",kw:["categorize per criteria","legal/technical/national/cross-border"]},
{id:"4.11.3",cl:1,name:"Security Mechanisms",kw:["crypto","DLP","transit/rest/use"]},
{id:"4.11.4",cl:1,name:"Environment Separation",kw:["no production data in test/dev","no cross-environment transfer"]},
{id:"4.11.5",cl:2,name:"Retention Periods",kw:["define","restrict critical data retention"]},
{id:"4.11.6",cl:3,name:"Improve Info Protection",kw:["audits","continuous improvement"]}
]},
{id:"4.12",title:"Backup & Recovery Management",icon:"💾",controls:[
{id:"4.12.1",cl:1,name:"Backup & Recovery Requirements",kw:["online/offline scope","retention","rapid recovery","periodicity","protection","availability"]},
{id:"4.12.2",cl:1,name:"Backup Process",kw:["RPO","full system where needed"]},
{id:"4.12.3",cl:1,name:"Recovery Process",kw:["recover by criticality"]},
{id:"4.12.4",cl:1,name:"Protect Backups",kw:["encryption","physical security"]},
{id:"4.12.5",cl:2,name:"Alternate Backup Site",kw:["equivalent security"]},
{id:"4.12.6",cl:2,name:"Test & Review",kw:["restore drills","effectiveness"]},
{id:"4.12.7",cl:2,name:"Automate",kw:["backup/recovery automation"]},
{id:"4.12.8",cl:3,name:"Improve B&R",kw:["RTO/RPO performance"]}
]},
{id:"4.13",title:"Configuration Mgmt & Hardening",icon:"🔩",controls:[
{id:"4.13.1",cl:1,name:"Config & Hardening Requirements",kw:["secure images","baselines"]},
{id:"4.13.2",cl:1,name:"Implement Baselines",kw:["apply to assets"]},
{id:"4.13.3",cl:1,name:"System Hardening",kw:["disable defaults"]},
{id:"4.13.4",cl:1,name:"Restrict Unnecessary Functions",kw:["ports/services/functions"]},
{id:"4.13.5",cl:1,name:"Monitor/Verify Config",kw:["baseline comparison"]},
{id:"4.13.6",cl:2,name:"Tool-Based Monitoring/Alerts",kw:["unauthorized deviation"]},
{id:"4.13.7",cl:2,name:"Automated Configuration",kw:["configure/reconfigure via change mgmt"]},
{id:"4.13.8",cl:3,name:"Improve Config/Hardening",kw:["compliance rates"]}
]},
{id:"4.14",title:"Secure Software Development",icon:"💻",controls:[
{id:"4.14.1",cl:1,name:"Secure SDLC Requirements",kw:["secure coding standards","approved libs/APIs","env segregation/access","security testing scope"]},
{id:"4.14.2",cl:1,name:"Access Control for Envs",kw:["authorized personnel only"]},
{id:"4.14.3",cl:1,name:"Security-by-Design/Tools",kw:["SAST/DAST","secure integration"]},
{id:"4.14.4",cl:1,name:"Secure Transmission Between Envs",kw:["integrity & trust"]},
{id:"4.14.5",cl:1,name:"Trusted Third-Party Components",kw:["up-to-date","vetted"]},
{id:"4.14.6",cl:2,name:"Security Review of Code",kw:["defect classes","input validation"]},
{id:"4.14.7",cl:2,name:"Security Testing",kw:["meets org requirements"]},
{id:"4.14.8",cl:3,name:"Improve SSDLC",kw:["coverage","quality gates"]}
]},
{id:"4.15",title:"Email & Web Browser Protection",icon:"📧",controls:[
{id:"4.15.1",cl:1,name:"Requirements for Email/Web Protection",kw:["standardized security mechanisms"]},
{id:"4.15.2",cl:1,name:"Implement Controls",kw:["spam/phish filters","MFA","email backup/archive","APT protection","block untrusted sites"]},
{id:"4.15.3",cl:1,name:"Restrict Webmail",kw:["firewall/URL filters"]},
{id:"4.15.4",cl:3,name:"Improve Protections",kw:["metrics","tuning"]}
]},
{id:"4.16",title:"Penetration Testing",icon:"🎯",controls:[
{id:"4.16.1",cl:2,name:"Pentest Requirements",kw:["purpose/objectives","frequency"]},
{id:"4.16.2",cl:2,name:"Pentest Process",kw:["scope/frequency (quarterly for critical)","methodology (grey/white box)"]},
{id:"4.16.3",cl:2,name:"Use VM Inputs",kw:["guide testing focus"]},
{id:"4.16.4",cl:2,name:"Reporting & Remediation",kw:["Pen-Test Report","patch/remediate"]},
{id:"4.16.5",cl:3,name:"Improve Pentesting",kw:["retests","closure rates"]}
]}
]},
{id:5,title:"Physical Security",icon:"🏢",cls:"d5",subs:[
{id:"5.1",title:"Protection of Physical Info Assets",icon:"🏗️",controls:[
{id:"5.1.1",cl:1,name:"Physical Protection Requirements",kw:["facilities","offsite","delivery/loading","transport","environmental threats"]},
{id:"5.1.2",cl:1,name:"Security Perimeters",kw:["zoning"]},
{id:"5.1.3",cl:1,name:"Secure Storage",kw:["secure zones off-hours"]},
{id:"5.1.4",cl:1,name:"Loading/Delivery Controls",kw:["segregation","supervision"]},
{id:"5.1.5",cl:1,name:"Environmental & Cable Security",kw:["fire/power/disasters","cable protection/labeling","CCTV/alarms/motion","operate per specs"]},
{id:"5.1.6",cl:1,name:"Secure Transport",kw:["risk-assessed movement"]},
{id:"5.1.7",cl:3,name:"Improve Physical Protection",kw:["inspections","tests"]}
]},
{id:"5.2",title:"Physical Access Management",icon:"🚪",controls:[
{id:"5.2.1",cl:1,name:"Physical Access Requirements",kw:["authorization","monitoring"]},
{id:"5.2.2",cl:1,name:"Physical Access Control List (PACL)",kw:["authorized individuals","credentials"]},
{id:"5.2.3",cl:1,name:"Access Grant/Manage Process",kw:["issue/track keys/cards"]},
{id:"5.2.4",cl:1,name:"Visitor Controls",kw:["badges","escort","unusual activity"]},
{id:"5.2.5",cl:2,name:"Review PACL",kw:["remove unneeded access"]},
{id:"5.2.6",cl:2,name:"Review Physical Access Logs",kw:["suspicious activity"]},
{id:"5.2.7",cl:3,name:"Improve Physical Access Mgmt",kw:["metrics","audits"]}
]}
]},
{id:6,title:"Third-Party Security",icon:"🤝",cls:"d6",subs:[
{id:"6.1",title:"Cloud Services",icon:"☁️",controls:[
{id:"6.1.1",cl:1,name:"Cloud Requirements",kw:["security expectations","SLAs"]},
{id:"6.1.2",cl:1,name:"Cloud Risk Assessment",kw:["before adoption/changes","consider information protection"]},
{id:"6.1.3",cl:1,name:"Cloud Cybersecurity Requirements",kw:["derived from classification & risk"]},
{id:"6.1.4",cl:1,name:"Cloud SLAs",kw:["incident notification/recovery","termination for non-compliance","exit procedures"]},
{id:"6.1.5",cl:1,name:"Data Residency",kw:["hosting/storage in KSA"]},
{id:"6.1.6",cl:2,name:"Audit/Monitor Cloud Provider",kw:["compliance checks"]},
{id:"6.1.7",cl:3,name:"Improve Cloud Controls",kw:["periodic evaluation"]}
]},
{id:"6.2",title:"Outsourcing Services",icon:"📄",controls:[
{id:"6.2.1",cl:1,name:"Outsourcing Requirements",kw:["risk assessment","expected cybersecurity","SLAs"]},
{id:"6.2.2",cl:1,name:"Outsourcing Risk Assessment",kw:["before outsourcing","consider information protection"]},
{id:"6.2.3",cl:1,name:"Third-Party Cybersecurity Req.",kw:["NDA","security clauses"]},
{id:"6.2.4",cl:1,name:"Outsourcing SLAs",kw:["incident communication","termination for non-compliance","exit & secure deletion"]},
{id:"6.2.5",cl:2,name:"Audit/Monitor Third Parties",kw:["contractual compliance"]},
{id:"6.2.6",cl:2,name:"Personnel Screening (Critical)",kw:["background checks for vendor staff"]},
{id:"6.2.7",cl:3,name:"Improve Outsourcing Controls",kw:["performance reviews","risk re-assessments"]}
]}
]}
];

let cl1=0,cl2=0,cl3=0;
DATA.forEach(d=>d.subs.forEach(s=>s.controls.forEach(c=>{if(c.cl===1)cl1++;else if(c.cl===2)cl2++;else cl3++})));
document.getElementById('cl1Count').textContent=cl1;
document.getElementById('cl2Count').textContent=cl2;
document.getElementById('cl3Count').textContent=cl3;

const container=document.getElementById('mindmap');
function renderKw(kws){return kws.map(k=>'<span>'+k+'</span>').join('')}

DATA.forEach((domain,di)=>{
const total=domain.subs.reduce((a,s)=>a+s.controls.length,0);
const dEl=document.createElement('div');
dEl.className='domain '+domain.cls;
dEl.style.animationDelay=(di*0.06)+'s';
let subsHTML='';
domain.subs.forEach(sub=>{
let ctrlsHTML='';
sub.controls.forEach(ctrl=>{
ctrlsHTML+='<div class="control-item" data-cl="'+ctrl.cl+'" data-text="'+(ctrl.id+' '+ctrl.name+' '+ctrl.kw.join(' ')).toLowerCase()+'"><div class="ctrl-top"><span class="ctrl-id">'+ctrl.id+'</span><span class="cl-badge cl'+ctrl.cl+'">CL'+ctrl.cl+'</span><span class="ctrl-name">'+ctrl.name+'</span></div><div class="ctrl-keywords">'+renderKw(ctrl.kw)+'</div></div>';
});
subsHTML+='<div class="subdomain"><div class="subdomain-header" onclick="toggleSub(this)"><span class="sub-icon">'+sub.icon+'</span><span class="sub-title">'+sub.id+' '+sub.title+'</span><span class="sub-count">'+sub.controls.length+'</span><span class="sub-chevron">▾</span></div><div class="sub-body"><div class="sub-inner">'+ctrlsHTML+'</div></div></div>';
});
dEl.innerHTML='<div class="domain-header" onclick="toggleDomain(this)"><div class="domain-icon">'+domain.icon+'</div><span class="domain-title">Domain '+domain.id+' — '+domain.title+'</span><span class="domain-count">'+total+' controls</span><span class="domain-chevron">▾</span></div><div class="domain-body"><div class="domain-inner">'+subsHTML+'</div></div>';
container.appendChild(dEl);
});

function toggleDomain(h){h.parentElement.classList.toggle('open')}
function toggleSub(h){h.parentElement.classList.toggle('open')}
window.toggleDomain=toggleDomain;
window.toggleSub=toggleSub;

document.getElementById('expandAll').addEventListener('click',()=>{document.querySelectorAll('.domain,.subdomain').forEach(el=>el.classList.add('open'))});
document.getElementById('collapseAll').addEventListener('click',()=>{document.querySelectorAll('.domain,.subdomain').forEach(el=>el.classList.remove('open'))});

let activeFilter='all';
document.querySelectorAll('.ctrl-btn[data-filter]').forEach(btn=>{
btn.addEventListener('click',()=>{
document.querySelectorAll('.ctrl-btn[data-filter]').forEach(b=>b.classList.remove('active'));
btn.classList.add('active');
activeFilter=btn.dataset.filter;
applyFilters();
});
});

const searchInput=document.getElementById('searchInput');
searchInput.addEventListener('input',()=>applyFilters());

function applyFilters(){
const query=searchInput.value.toLowerCase().trim();
document.querySelectorAll('.control-item').forEach(item=>{
const cl=item.dataset.cl;
const text=item.dataset.text;
const clMatch=activeFilter==='all'||('cl'+cl)===activeFilter;
const searchMatch=!query||text.includes(query);
item.classList.toggle('hidden',!(clMatch&&searchMatch));
item.querySelectorAll('.ctrl-keywords span').forEach(tag=>{
tag.classList.toggle('hl',query&&tag.textContent.toLowerCase().includes(query));
});
item.classList.toggle('match',query&&text.includes(query)&&clMatch);
});
document.querySelectorAll('.subdomain').forEach(sub=>{
sub.classList.toggle('hidden',!sub.querySelectorAll('.control-item:not(.hidden)').length);
});
document.querySelectorAll('.domain').forEach(dom=>{
dom.classList.toggle('hidden',!dom.querySelectorAll('.subdomain:not(.hidden)').length);
});
if(query){document.querySelectorAll('.domain:not(.hidden),.subdomain:not(.hidden)').forEach(el=>el.classList.add('open'))}
}
</script>
</body>
</html>
