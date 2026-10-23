# ControlNetForge Pro (v1.0.0)

**ControlNet (5.0 Mbps CIP / IEC 61158 Type 2\) Protocol Studio, Network Update Time (NUT) Scheduler, RG-6 Coaxial Attenuation Sizer, & 10-Point Safety Auditor**

---

## ⚡ Overview

**ControlNetForge Pro** is an industrial automation protocol engineering suite specifically targeted at **ControlNet (ODVA CIP / IEC 61158 Type 2\)** deterministic fieldbus networks (Rockwell Automation Allen-Bradley ControlLogix 1756, Flex I/O 1794, Kinetix servo drives, and PowerFlex inverters). It delivers zero-dependency, browser-based, and command-line automation for:

1. **5.0 Mbps Manchester II Scheduled Frame Engine**: Models 5.0 Mbps physical signaling, 16-bit Preamble (`0xAA55`), Sync Delimiter (`0x7E`), LNK header parsing, and ITU-T CRC-16 Frame Check Sequences (\$x^{16} \+ x^{12} \+ x^5 \+ 1\$).  
2. **Network Update Time (NUT) Bandwidth Allocator**: Automatically calculates Scheduled Service Portion (SSP) versus Unscheduled Service Portion (USP) intervals, SMax/UMax boundaries, and verifies Requested Packet Interval (RPI) binary harmonization (\$RPI \= NUT \\times 2^n\$).  
3. **RG-6 Coaxial Trunk & Tap Attenuation Sizer**: Models \$75\\ \\Omega\$ quad-shield coaxial cable attenuation (\$1.63\\text{ dB}/100\\text{m}\$ at \$5.0\\text{ MHz}\$) and passive BNC tap insertion losses (\$0.75\\text{ dB/tap}\$) against the strict \$13.3\\text{ dB}\$ transceiver dynamic range limit.  
4. **10-Point ControlNet Safety Auditor**: Pre-flight verification checking MAC ID ranges (`1..99`), duplicate node collision risks, 48-tap limits, dual \$75\\ \\Omega\$ terminators, SSP load ceilings (\$\\le 75%\$), and redundant media cabling.  
5. **Multi-Target Exporter**: Outputs RSNetWorx for ControlNet schedule CSV tables, Studio 5000 / RSLogix 5000 tag alias mappings (`1756-CNBR` / `1756-CN2R`), and Python virtual frame generation scripts.

---

## 📁 Repository Structure

product\_199/

├── source-code/

│   ├── controlnet-engine.js         \# Manchester II framing, delimiters, CRC-16, LNK headers

│   ├── controlnet-nut-scheduler.js  \# NUT bandwidth allocator & RPI binary harmonization

│   ├── controlnet-coax-sizer.js     \# RG-6 coaxial attenuation & tap loss budget math

│   ├── controlnet-auditor.js        \# 10-Point ControlNet physical & protocol safety auditor

│   ├── controlnet-forge.css         \# Allen-Bradley red & silver industrial UI theme

│   ├── app.js                       \# Interactive web controller

│   └── index.html                   \# Responsive 5-tab web studio

├── build/

│   ├── controlnet-cli.py            \# Standalone Python CLI executable (chmod \+x)

│   └── controlnetforge-pro-v1.0.0.zip\# Production release archive

├── documentation/

│   ├── ARCHITECTURE.md              \# Engineering specification & protocol mathematics

│   ├── USER\_GUIDE.md                \# Operator manual & CLI instructions

│   ├── MONETIZATION\_AND\_MARKETING\_PLAYBOOK.md \# Commercial strategy & pricing tiers

│   └── PROGRESS\_REPORT.md           \# Cycle \#199 milestone report

├── screenshots/

│   └── controlnet-studio-preview.svg\# High-resolution SVG preview diagram

└── README.md                        \# Master product documentation

---

## 🚀 Quick Start

### 1\. Launch Interactive Web Studio

Open `product_199/source-code/index.html` in any web browser. Zero server, node packages, or build steps required.

### 2\. Standalone Python CLI Usage

\# Make CLI executable

chmod \+x product\_199/build/controlnet-cli.py

\# Build a Scheduled I/O Data Frame for Node 2, Connection 0x1001

./product\_199/build/controlnet-cli.py frame-build \--mac 2 \--conn 0x1001

\# Dissect a raw ControlNet hex frame

./product\_199/build/controlnet-cli.py frame-dissect "AA 55 7E 02 10 01 01 00 11 22 33 44 55 66 77 C1 76"

\# Calculate NUT Bandwidth Allocation

./product\_199/build/controlnet-cli.py nut-schedule \--conns '\[{"id":1,"bytes":32,"rpi":5.0},{"id":2,"bytes":64,"rpi":5.0}\]' \--nut 5.0

\# Evaluate RG-6 Coaxial Line Attenuation

./product\_199/build/controlnet-cli.py coax-size \--trunk 400 \--taps 4

\# Run 10-Point Safety Auditor

./product\_199/build/controlnet-cli.py audit \--nodes '\[{"mac":1},{"mac":2},{"mac":3}\]' \--conns '\[{"id":1,"bytes":32,"rpi":5.0}\]' \--trunk 400 \--taps 4

---

## 🧪 Verification & Automated Testing

The engine has been tested against 10 comprehensive unit tests:

python3 test\_controlnetforge.py

\# Output: Ran 10 tests in 0.612s \- OK

---

## 💼 Commercial & Pricing Model

- **Community Edition**: Free / Open Source (Frame Builder, Dissector, Basic NUT Calculator, Web UI).  
- **Professional License**: \$299 one-time per engineer seat (Full NUT Bandwidth Allocator, 10-Point Safety Auditor, Python CLI, RSNetWorx & Studio 5000 Exporters).  
- **Plant Site License**: \$2,490 / facility / year (Site-wide multi-seat license, automated CI/CD schedule verification hooks, priority technical support).