<!-- Animated Header Banner -->
<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0f0c29,50:302b63,100:24243e&height=200&section=header&text=IBM%20Z%20Mainframe%20Dev%20Environment&fontSize=32&fontColor=ffffff&animation=fadeIn&fontAlignY=38&desc=VSC1%20%7C%20Zowe%20Explorer%20%7C%20z%2FOS%20Connection%20Setup&descAlignY=55&descAlign=62" />

<!-- Badges Row 1 -->
[![IBM Z Xplore](https://img.shields.io/badge/IBM%20Z%20Xplore-Complete%20✓-00b4d8?style=for-the-badge&logo=ibm&logoColor=white)](https://ibmzxplore.influitive.com)
[![Challenge](https://img.shields.io/badge/Challenge-VSC1-blueviolet?style=for-the-badge&logo=visualstudiocode&logoColor=white)](https://code.visualstudio.com)
[![Platform](https://img.shields.io/badge/Platform-z%2FOS-critical?style=for-the-badge&logo=linux&logoColor=white)](#)
[![Status](https://img.shields.io/badge/Status-Production%20Ready-success?style=for-the-badge&logo=checkmarx&logoColor=white)](#)

<!-- Badges Row 2 -->
[![Node.js](https://img.shields.io/badge/Node.js-LTS-339933?style=flat-square&logo=nodedotjs&logoColor=white)](https://nodejs.org)
[![VSCode](https://img.shields.io/badge/VSCode-Latest-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white)](https://code.visualstudio.com)
[![Zowe](https://img.shields.io/badge/Zowe-Explorer-1d4e89?style=flat-square&logo=zowe&logoColor=white)](https://www.zowe.org)
[![Java](https://img.shields.io/badge/Java-LTS%20Runtime-ED8B00?style=flat-square&logo=openjdk&logoColor=white)](https://developer.ibm.com/languages/java/)
[![License](https://img.shields.io/badge/License-IBM%20Z%20Xplore-lightgrey?style=flat-square)](#)

</div>

---

## 🚀 What Is This Project?

> **In plain English:** This project documents how I successfully configured a **professional IBM Mainframe development environment** from scratch — the same kind of setup used by engineers at major banks, airlines, and insurance companies that run the world's most critical financial systems.

IBM Z mainframes process **over $8 trillion in daily commercial transactions worldwide**. This challenge (VSC1) is the foundational gateway to that world — proving I can set up, secure, and operate a live connection to a real z/OS mainframe server using modern developer tooling.

**Completing this is not just clicking "Next, Next, Finish."** It requires understanding network security, TLS/SSL certificate trust chains, JSON configuration, mainframe data set architecture, and JCL job submission — all at once.

---

## 🎯 Why This Matters to Your Team

<div align="center">

| 💡 Skill Demonstrated | 🏦 Real-World Application |
|---|---|
| Mainframe z/OS connectivity | Banks, insurers, and gov't systems run on z/OS |
| Zowe Explorer configuration | Industry-standard modern Z access tool |
| SSL/TLS self-signed cert handling | Required in enterprise private cloud environments |
| JCL job submission | Core skill for every mainframe operation |
| JSON-based profile management | Modern DevOps config-as-code practices |
| Multi-platform setup (Win/Mac/Linux) | Cross-environment engineering capability |
| Network firewall/connectivity troubleshooting | Critical for enterprise deployments |

</div>

---

## 🏗️ System Architecture

Here is a visual map of exactly how my local machine talks to the IBM Z mainframe:

```mermaid
graph TB
    subgraph 💻 Local Machine
        VS[🖥️ VS Code Editor]
        ZE[🔌 Zowe Explorer Plugin]
        ZOE[📝 IBM Z Open Editor]
        NODE[⚙️ Node.js Runtime]
        JAVA[☕ Java Runtime]
        CFG[📄 zowe.config.json]
    end

    subgraph 🔐 Security Layer
        TLS[🔒 TLS/SSL Encryption]
        CERT[📜 Self-Signed Certificate]
        AUTH[🔑 z/OS Credentials]
    end

    subgraph 🖥️ IBM Z Mainframe Server
        ZOSMF[🌐 z/OSMF REST API
204.90.115.200:10443]
        ZOS[🏢 z/OS Operating System]
        DS[📦 Data Sets
ZXP.PUBLIC.JCL]
        USS[📁 Unix System Services
/z/z#####]
        JOBS[⚙️ Job Entry Subsystem
JCL Submission]
    end

    VS --> ZE
    VS --> ZOE
    ZE --> NODE
    ZOE --> JAVA
    ZE --> CFG
    CFG --> TLS
    TLS --> CERT
    CERT --> AUTH
    AUTH --> ZOSMF
    ZOSMF --> ZOS
    ZOS --> DS
    ZOS --> USS
    ZOS --> JOBS
    JOBS -->|✅ CHKVSC Validation| ZOS

    style VS fill:#007ACC,color:#fff
    style ZOSMF fill:#1d4e89,color:#fff
    style ZOS fill:#0f0c29,color:#fff
    style TLS fill:#d62828,color:#fff
    style CFG fill:#f4a261,color:#000
```

---

## 🔄 Setup Flow — Step by Step

This flowchart shows the exact sequence I followed to go from zero to a live mainframe connection:

```mermaid
flowchart LR
    A([🟢 Start]) --> B[Download
Node.js LTS]
    B --> C[Download
Java Runtime]
    C --> D[Install
VS Code]
    D --> E[Install IBM
Z Open Editor
Extension]
    E --> F[Zowe Explorer
Auto-Installed]
    F --> G[Create Team
Config File
zowe.config.json]
    G --> H[Set zosmf
Port: 10443]
    H --> I[Set tso
Account: FB3]
    I --> J[Set Host IP
204.90.115.200]
    J --> K[Disable
rejectUnauthorized]
    K --> L[Add Z-Userid
& Password]
    L --> M[Set DATA SETS
Filter]
    M --> N[Set USS
Filter]
    N --> O[Set JOBS
Filter]
    O --> P[Navigate to
ZXP.PUBLIC.JCL]
    P --> Q[Submit
CHKVSC Job]
    Q --> R([🏆 VSC1
Complete!])

    style A fill:#2dc653,color:#000
    style R fill:#2dc653,color:#000
    style G fill:#f4a261,color:#000
    style K fill:#d62828,color:#fff
    style Q fill:#1d4e89,color:#fff
```

---

## 🔒 Security Architecture Deep Dive

This was not a simple username/password login. Here is the full security stack in play:

```mermaid
sequenceDiagram
    participant DEV as 💻 Developer (Me)
    participant VSC as VS Code + Zowe
    participant CFG as zowe.config.json
    participant NET as Network / Firewall
    participant ZOS as z/OS Server (204.90.115.200)

    DEV->>VSC: Open Zowe Explorer
    VSC->>CFG: Load Team Configuration
    CFG-->>VSC: Host, Port, Auth settings
    DEV->>VSC: Enter Z-userid + Password
    VSC->>VSC: Store credentials securely
(OS Keychain / Credential Store)
    VSC->>NET: Initiate HTTPS connection
Port 10443
    NET->>ZOS: TCP/IP Route to mainframe
    ZOS-->>NET: Present Self-Signed TLS Certificate
    NET-->>VSC: Certificate received
    VSC->>VSC: rejectUnauthorized: false
✅ Accept self-signed cert
    VSC->>ZOS: Authenticated REST API call
via z/OSMF
    ZOS-->>VSC: 200 OK — Mainframe access granted
    VSC-->>DEV: 🟢 Data Sets, USS, JOBS visible
```

### 🛡️ Security Features Breakdown

| Security Feature | Implementation | Purpose |
|---|---|---|
| **TLS/SSL Encryption** | HTTPS on port 10443 | All data in transit is encrypted end-to-end |
| **Self-Signed Certificate Handling** | `rejectUnauthorized: false` in config | Allows enterprise internal certs not signed by a public CA |
| **OS Credential Store** | macOS Keychain / Windows Credential Manager | Passwords never stored in plain text on disk |
| **z/OSMF REST API Auth** | HTTP Basic Auth over TLS | Industry-standard mainframe API authentication |
| **Team Configuration File** | `zowe.config.json` with scoped profiles | Separates connection config from secrets |
| **Profile Scoping** | Global vs Project config | Prevents credential leakage across projects |
| **Password Rotation** | 60-day expiry policy | Enforces regular credential hygiene |
| **Firewall Validation** | Pre-connection browser test | Confirms network path before tool configuration |

> 🔑 **Key Insight:** The self-signed cert setup mirrors exactly what you encounter in private banking and government cloud environments where internal Certificate Authorities (CAs) are used instead of public ones like Let's Encrypt.

---

## 🛠️ Full Technology Stack

```mermaid
pie title Technology Stack Breakdown
    "VS Code (IDE)" : 25
    "Zowe Explorer (Mainframe Access)" : 25
    "IBM Z Open Editor (COBOL/JCL Syntax)" : 20
    "Node.js (Zowe Runtime)" : 15
    "Java Runtime (Z Open Editor Engine)" : 10
    "z/OSMF REST API (Mainframe Interface)" : 5
```

| Layer | Technology | Version | Role |
|---|---|---|---|
| **IDE** | Visual Studio Code | Latest Stable | Primary development environment |
| **Mainframe Extension** | IBM Z Open Editor | Latest | COBOL, JCL, PL/I syntax support |
| **Mainframe Access** | Zowe Explorer | Bundled with Z Open Editor | Browse Data Sets, USS, Jobs |
| **Runtime (Zowe)** | Node.js | LTS (20.x+) | Powers Zowe Explorer's UI layer |
| **Runtime (Z Editor)** | Java | LTS (IBM Semeru) | Powers language server for Z files |
| **API Protocol** | z/OSMF REST API | z/OS native | RESTful access to mainframe resources |
| **Config Format** | JSON (zowe.config.json) | Team Configuration v2 | Profile and connection management |
| **Transport Security** | TLS/HTTPS | Port 10443 | Encrypted communication channel |
| **OS Support** | Windows / macOS / Linux | All platforms | Cross-platform toolchain |

---

## ⚡ Quick Start

### Prerequisites Checklist

```
✅ Network access to 204.90.115.200:10443 (test in browser first!)
✅ IBM Z Xplore account with assigned Z-userid (e.g., Z12345)
✅ ~45 minutes of focused setup time
✅ Admin rights on your local machine
```

### Installation Timeline

```mermaid
gantt
    title VSC1 Setup Timeline (~45 minutes)
    dateFormat mm
    axisFormat %M min

    section Downloads
    Download Node.js LTS         : 00, 5m
    Download Java Runtime        : 02, 5m
    Download VS Code             : 04, 5m

    section Installations
    Install Node.js              : 07, 5m
    Install Java                 : 09, 4m
    Install VS Code              : 11, 4m
    Install IBM Z Open Editor    : 14, 6m

    section Configuration
    Create zowe.config.json      : 20, 5m
    Configure zosmf + tso        : 23, 5m
    Set host + cert settings     : 26, 4m
    Add Z credentials            : 29, 3m

    section Validation
    Set DATA SETS filter         : 32, 3m
    Set USS + JOBS filters       : 34, 3m
    Navigate to ZXP.PUBLIC.JCL   : 37, 3m
    Submit CHKVSC validation job : 40, 5m
```

### Step-by-Step Setup

#### 1️⃣ Install Node.js
```bash
# Download from: https://nodejs.org/en/
# Choose the LTS version (more stable, recommended for enterprise use)
# Verify install:
node --version
npm --version
```

#### 2️⃣ Install Java Runtime
```bash
# IBM Semeru (recommended): https://developer.ibm.com/languages/java/semeru-runtimes/downloads/
# Choose LTS version
# Verify install:
java -version
```

#### 3️⃣ Install VS Code + IBM Z Open Editor
```
1. Download VS Code: https://code.visualstudio.com/download
2. Launch VS Code
3. Click the Extensions icon (4 boxes) in the left sidebar
4. Search: "IBM Z Open Editor"
5. Click Install → This also installs Zowe Explorer automatically
```

#### 4️⃣ Configure zowe.config.json
```json
{
  "profiles": {
    "zosmf": {
      "type": "zosmf",
      "properties": {
        "port": 10443
      }
    },
    "tso": {
      "type": "tso",
      "properties": {
        "account": "FB3"
      }
    },
    "base": {
      "type": "base",
      "properties": {
        "host": "204.90.115.200",
        "rejectUnauthorized": false
      },
      "secure": ["user", "password"]
    }
  }
}
```

> ⚠️ **Security Note:** `rejectUnauthorized: false` is intentional here because the z/OS server uses a **self-signed certificate** — common in private enterprise environments. In public production systems, you would use a CA-verified certificate and set this to `true`.

#### 5️⃣ Set Up Your Filters

| Section | Filter Value | Purpose |
|---|---|---|
| DATA SETS | `Z#####` then add `,ZXP.PUBLIC.*` | See your datasets + public JCL members |
| Unix System Services | `/z/z#####` (lowercase!) | Access USS home directory |
| JOBS | `Owner: Z##### \| Prefix: * \| Status: *` | Monitor all your submitted jobs |

#### 6️⃣ Submit Validation Job
```
1. In DATA SETS, navigate to: ZXP.PUBLIC.JCL
2. Find member: CHKVSC
3. Right-click → Submit Job
4. Wait a few seconds
5. Visit https://ibmzxplore.influitive.com → VSC1 marked COMPLETE ✅
```

---

## 🔧 Troubleshooting Guide

```mermaid
flowchart TD
    A[❌ Problem Encountered] --> B{What type?}

    B -->|Can't reach server| C[ETIMEDOUT / Timed Out]
    B -->|Wrong credentials| D[REST API Error / Red Circle]
    B -->|Config broken| E[Corrupted zowe.config.json]
    B -->|500 Error on dataset| F[EDC5041I fopen failed]

    C --> C1[Test in browser:
204.90.115.200:10443/zosmf/info]
    C1 --> C2{Can you reach it?}
    C2 -->|No| C3[Request firewall rule change
from your network provider]
    C2 -->|Yes| C4[Check port 10443 in config]

    D --> D1[Right-click profile
→ Manage Profile
→ Update Credentials]
    D1 --> D2[Re-enter Z-userid
& password carefully]

    E --> E1[Restore from sample
team configuration]
    E1 --> E2[Restart VS Code
to clear cache]

    F --> F1[This is NORMAL on first filter use]
    F1 --> F2[Close the error
and continue — it's fine!]

    style A fill:#d62828,color:#fff
    style C3 fill:#f4a261,color:#000
    style F2 fill:#2dc653,color:#000
```

---

## 📊 What I Connected To — The z/OS Ecosystem

```mermaid
mindmap
  root((z/OS
Mainframe))
    DATA SETS
      Sequential Files
      Partitioned Data Sets PDS
      Members COBOL JCL programs
      ZXP.PUBLIC.JCL
        CHKVSC validation job
    Unix System Services USS
      Home Directory /z/z#####
      File System Access
      Shell Commands
    JOBS JES2
      JCL Submission
      Job Monitoring
      Output SYSOUT viewing
    z/OSMF REST API
      Port 10443
      HTTPS Encrypted
      JSON Responses
      Profile Management
```

---

## 🧠 Key Concepts Explained (Plain English)

| Term | What It Actually Means |
|---|---|
| **z/OS** | IBM's operating system that runs on mainframe hardware. It's like Windows, but for supercomputers that process millions of bank transactions per second. |
| **Zowe Explorer** | A VS Code plugin that lets modern developers browse mainframe files and run jobs — like File Explorer, but for a computer the size of a refrigerator in a data center. |
| **z/OSMF** | The mainframe's REST API. Think of it as the mainframe's "web server" that lets modern tools talk to it using standard HTTP requests. |
| **Data Sets** | The mainframe equivalent of files and folders — but with very specific naming rules and record structures. |
| **JCL (Job Control Language)** | Instructions that tell the mainframe what program to run, with what data, and how to handle output. Like a shell script, but for z/OS. |
| **CHKVSC** | The specific JCL validation job I submitted to prove my connection was working correctly. |
| **TSO Account** | Your billing/resource account on the mainframe (set to `FB3` for IBM Z Xplore). Like a project billing code in cloud computing. |
| **Team Configuration** | A JSON file that stores connection settings for your whole team — modern "config as code" applied to mainframe connectivity. |
| **rejectUnauthorized: false** | Tells the connection layer "I know this certificate isn't from a public authority, but I trust it anyway" — needed for private enterprise environments. |
| **USS (Unix System Services)** | A full UNIX file system running inside z/OS. Yes, the mainframe runs Linux-style commands too. |

---

## 🏆 Skills Demonstrated by Completing This

<div align="center">

```mermaid
radar
  title Skills Applied in VSC1
  options
    max 10
  "Mainframe Architecture" : 9
  "Security Config" : 8
  "DevTools Setup" : 9
  "Network Troubleshooting" : 7
  "JSON Config Management" : 8
  "Enterprise Tooling" : 9
  "Cross-Platform Setup" : 8
```

</div>

| Category | Skills Applied |
|---|---|
| 🏢 **Enterprise Architecture** | Understanding z/OS data architecture, JES2 job subsystem, z/OSMF API layer |
| 🔒 **Security & Certs** | TLS/SSL configuration, self-signed cert trust management, OS credential store integration |
| 🛠️ **DevOps & Tooling** | VS Code extension ecosystem, config-as-code (JSON profiles), multi-tool integration |
| 🌐 **Networking** | Port-level connectivity testing, firewall requirements, REST API validation |
| 🔍 **Troubleshooting** | Diagnosing REST errors, credential issues, config corruption, and z/OS error codes |
| 📋 **JCL Basics** | Navigating PDS members, submitting batch jobs, understanding validation output |

---

## 📁 Project Structure

```
📦 ibm-z-vscode-mainframe-setup/
├── 📄 README.md                  ← You are here
├── 📄 zowe.config.json           ← Team configuration file (sanitized)
├── 📁 docs/
│   ├── 📄 architecture.md        ← Detailed architecture notes
│   ├── 📄 security-notes.md      ← SSL/cert configuration rationale
│   └── 📄 troubleshooting.md     ← Common issues and fixes
├── 📁 jcl/
│   └── 📄 CHKVSC.jcl             ← Validation JCL reference copy
└── 📁 screenshots/
    ├── 🖼️ zowe-connected.png      ← Live connection screenshot
    ├── 🖼️ datasets-view.png       ← Data sets browser view
    └── 🖼️ job-complete.png        ← VSC1 challenge completion
```

---

## 🌐 Resources & References

| Resource | Link |
|---|---|
| IBM Z Xplore Platform | [ibmzxplore.influitive.com](https://ibmzxplore.influitive.com) |
| Zowe Explorer Docs | [docs.zowe.org](https://docs.zowe.org) |
| IBM Z Open Editor | [marketplace.visualstudio.com](https://marketplace.visualstudio.com/items?itemName=IBM.zopeneditor) |
| IBM Semeru Java Runtime | [developer.ibm.com/languages/java](https://developer.ibm.com/languages/java/semeru-runtimes/downloads/) |
| Node.js LTS | [nodejs.org](https://nodejs.org/en/) |
| VS Code Download | [code.visualstudio.com](https://code.visualstudio.com/download) |

---

## 👨‍💻 About the Developer

<div align="center">

**Built and documented by Anand Sundar** — a Senior Full-Stack Engineer with 9+ years of experience in high-throughput payment infrastructure, distributed systems, and backend architecture.

This IBM Z Xplore challenge is part of an active journey into **mainframe engineering and cloud solutions architecture** — bridging modern distributed systems knowledge with the enterprise mainframe platforms that power the world's financial backbone.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](#)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-181717?style=for-the-badge&logo=github&logoColor=white)](#)

</div>

---

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:24243e,50:302b63,100:0f0c29&height=120&section=footer&animation=fadeIn" />

**⭐ If this helped you connect to IBM Z — give it a star!**

*IBM Z Xplore © IBM 2021–2025 | Challenge VSC1 | 250826-0742*

</div>
