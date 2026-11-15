# Arizona Digital Emcomm Net (AZDEN) — Winlink Templates

Official standardized Winlink Express template packages for the **Arizona Digital Emcomm Net (AZDEN)**.

This repository provides field-tested, offline-capable digital forms and display viewers designed for rapid, standardized emergency communications, net check-ins, and situation reports across Arizona.

---

## Package Contents

| File | Form Package | Purpose |
| :--- | :--- | :--- |
| `AZDEN_CheckIn.txt` | Check-In | Primary Check-In template definition driving message generation and variable mapping. |
| `AZDEN_CheckIn_Entry.html` | Check-In | Interactive Check-In data entry form served by Winlink Express (`http://{FormServer}:{FormPort}`). |
| `AZDEN_CheckIn_Display.html` | Check-In | Recipient display viewer rendering Check-In XML records (`RMS_Express_Form_*.xml`). |
| `AZDEN_CheckIn_Reply.txt` | Check-In | Standardized Net Control Station (NCS) reply template for acknowledging check-ins. |
| `AZDEN_Style.css` | Check-In | Unified Arizona-themed stylesheet linked via `{FormFolder}` for Check-In entry and display layouts. |
| `AZDEN-SITREP.txt` | Situation Report | Primary SitRep template definition mapping 26 report variables to `AZDEN-NET` / NCS. |
| `AZDEN-SITREP_Entry.html` | Situation Report | Multi-section interactive Situation Report form with responsive CSS Grid layout and self-contained offline CSS. |
| `AZDEN-SITREP_Display.html` | Situation Report | Printable recipient display viewer rendering Situation Report XML records. |

---

## Included Templates

### 1. AZDEN Station Check-In (`AZDEN_CheckIn.txt`)
Quick net check-in form capturing callsign, operator name, position/grid, timestamp, Net Control target, triage station status (**Green / Yellow / Red**), and brief traffic/comments, paired with `AZDEN_CheckIn_Reply.txt` for NCS acknowledgments.

### 2. AZDEN Situation Report (`AZDEN-SITREP.txt`)
Comprehensive multi-section post-incident report defaulting destination target `AZDEN-NET`, organized into five structured sections:
1. **Incident and Routing**: Incident name, date/time (`{DateTime}`), position/grid (`{Position}`), callsign (`{Callsign}`), operator name (`{User}`), and Net Control target.
2. **Station Communication Capabilities**: Backup power source (`Commercial Grid`, `Generator`, `Solar - Battery`, `Vehicle`), estimated runtime in hours, and active bands/modes monitored.
3. **Critical Infrastructure & Utilities**: Status flags and per-utility notes for **Grid Power**, **Water**, **Cell Service**, **POTS**, **Internet**, and **Cable TV**.
4. **Neighborhood & Safety Conditions**: Road access hazards/closures and structural or property damage assessments.
5. **Immediate Needs & Welfare**: Urgent medical/life-safety needs, local community resource requests, and Health & Wellness (`I am safe`) message queue count.

---

## Key Features

* **Triage Station Condition Assessment (`AZDEN_CheckIn`)**:
  * **Green**: Fully operational / healthy, stable power, no resources needed.
  * **Yellow**: Assistance or resources needed (equipment, relief, fuel).
  * **Red**: Immediate medical, rescue, or safety assistance required.
* **Interactive Date/Time Picker**:
  * Pre-populated with current Winlink Express timestamp (`{DateTime}`).
  * Clicking the date field opens a prompt to update or confirm the timestamp on demand.
* **Offline Draft Persistence ("Save / Load Form Data")**:
  * Operators can save recurring station profiles or in-progress drafts as local `.txt` JSON files.
  * Reload saved drafts with one click before submitting.
  * Draft payloads (`parseme` staging area) remain local and are never transmitted over RF.
* **Outside-Winlink Safety Detection**:
  * Detects when a form is opened directly in a standalone browser outside Winlink Express, hiding **Submit** while allowing local drafting and saving for handoff to a radio operator.
* **100% Offline Stylesheets & Zero RF Overhead**:
  * `AZDEN_CheckIn` shares `AZDEN_Style.css` via `{FormFolder}`.
  * `AZDEN-SITREP` embeds self-contained CSS directly in its HTML files with zero network dependencies.
  * HTML and CSS assets remain strictly local on workstations; only plain text and compact `RMS_Express_Form_*.xml` payloads travel over RF.
* **Strict Windows CRLF Compliance**:
  * Configured via `.gitattributes` and validated to enforce Windows CRLF (`\r\n`) line endings required by Winlink Express.

---

## Installation in Winlink Express

### Method 1: Git Clone (Recommended)

Open a command prompt (or Git Bash) and clone this repository into your Winlink Express templates folder:

```cmd
cd "C:\RMS Express\Global Folders\Templates"
git clone https://github.com/barryshaffer/AZDEN_templates.git
```

To pull future form updates, run:
```cmd
cd "C:\RMS Express\Global Folders\Templates\AZDEN_templates"
git pull
```

### Method 2: Manual Download (ZIP)

1. Download this repository as a `.zip` archive from GitHub (`Code` -> `Download ZIP`).
2. Extract the folder into `C:\RMS Express\Templates\` (or `C:\RMS Express\Global Folders\Templates\`).
3. Ensure the folder is named `AZDEN_templates`.

---

## Using the Forms in Winlink Express

1. Open **Winlink Express**.
2. Click **Message** &rarr; **New Message**.
3. In the message composer, click **Select Template**.
4. Navigate to **Templates** (or **Global Templates**) &rarr; **AZDEN_templates** &rarr; double-click **`AZDEN_CheckIn.txt`** or **`AZDEN-SITREP.txt`**.
5. Your default web browser will launch displaying the selected form.
6. Verify your callsign, grid/position, and complete the form fields.
7. Click **Submit**.
8. Winlink Express will automatically populate the Subject, message body, and attach the corresponding `RMS_Express_Form_*.xml` record.
9. Post to Outbox and transmit via your selected mode (VARA HF, VARA FM, Packet, Telnet, or PACTOR).

---

## License & Attribution

Maintained for the amateur radio emergency communications community and the Arizona Digital Emcomm Net. Free to use, adapt, and distribute for EmComm operations.
