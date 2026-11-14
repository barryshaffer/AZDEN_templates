# Arizona Digital Emcomm Net (AZDEN) — Winlink Templates

Official standardized Winlink Express template package for the **Arizona Digital Emcomm Net (AZDEN)**.

This repository provides field-tested, offline-capable digital forms and display viewers designed for rapid, standardized emergency communications and net check-ins across Arizona.

---

## Package Contents

| File | Purpose |
| :--- | :--- |
| `AZDEN_CheckIn.txt` | Primary template definition file driving message generation and mapping form variables to email headers and message body. |
| `AZDEN_CheckIn_Entry.html` | Browser-based interactive data entry form served by Winlink Express's local loopback server (`http://{FormServer}:{FormPort}`). |
| `AZDEN_CheckIn_Display.html` | Recipient display viewer that renders structured XML check-in records (`RMS_Express_Form_*.xml`) into a formatted layout. |
| `AZDEN_Style.css` | Unified Arizona-themed stylesheet linked via `{FormFolder}` for both entry and display layouts. |
| `AZDEN_CheckIn_Reply.txt` | Standardized net control station (NCS) reply template for acknowledging received check-ins. |

---

## Key Features

* **Triage Station Condition Assessment**:
  * **Green**: Fully operational / healthy, stable power, no resources needed.
  * **Yellow**: Assistance or resources needed (equipment, relief, fuel).
  * **Red**: Immediate medical, rescue, or safety assistance required.
* **Interactive Date/Time Picker**:
  * Pre-populated with current UTC/local timestamp.
  * Clicking the date field opens an entry dialog to update or confirm the timestamp on demand.
* **Offline Draft Persistence ("Save / Load Form Data")**:
  * Operators can save recurring station profiles (callsign, operator name, position) as local `.txt` draft files.
  * Load pre-saved configurations with one click before submitting.
  * Draft data payloads are never transmitted over RF.
* **Outside-Winlink Safety Detection**:
  * Automatically detects when an operator opens the form directly in a web browser without Winlink running and disables submission while allowing local data saving.
* **Shared External Stylesheet (`{FormFolder}`)**:
  * Compliant with Winlink's official W4PHS specification (`<link href="{FormFolder}AZDEN_Style.css" rel="stylesheet" type="text/css" />`).
  * Enforces DRY design while keeping RF transmission size minimal (stylesheets remain local and are never sent over the air).
* **Strict Windows CRLF Compliance**:
  * Configured via `.gitattributes` to ensure Windows CRLF (`\r\n`) line endings regardless of the operating system used to clone.

---

## Installation in Winlink Express

### Method 1: Git Clone (Recommended)

Open a command prompt (or Git Bash) and clone this repository into your Winlink Express templates folder:

```cmd
cd "C:\RMS Express\Templates"
git clone https://github.com/<owner>/AZDEN_templates.git
```
*(Or clone into `C:\RMS Express\Global Templates\AZDEN_templates`)*

To pull future form updates, run:
```cmd
cd "C:\RMS Express\Templates\AZDEN_templates"
git pull
```

### Method 2: Manual Download (ZIP)

1. Download this repository as a `.zip` archive from GitHub (`Code` -> `Download ZIP`).
2. Extract the folder into `C:\RMS Express\Templates\` (or `C:\RMS Express\Global Templates\`).
3. Ensure the folder is named `AZDEN_templates`.

---

## Using the Form in Winlink Express

1. Open **Winlink Express**.
2. Click **Message** &rarr; **New Message**.
3. In the message composer, click **Select Template**.
4. Navigate to **Templates** (or **Global Templates**) &rarr; **AZDEN_templates** &rarr; double-click **`AZDEN_CheckIn.txt`**.
5. Your default web browser will launch displaying the AZDEN Check-In form.
6. Verify your callsign, grid, position, and select your station condition.
7. Click **Submit**.
8. Winlink Express will automatically populate the Subject, message body, and attach the `RMS_Express_Form_AZDEN_CheckIn.xml` record.
9. Post to Outbox and transmit via your selected mode (VARA HF, VARA FM, Packet, Telnet, or PACTOR).

---

## License & Attribution

Maintained for the amateur radio emergency communications community and the Arizona Digital Emcomm Net. Free to use, adapt, and distribute for EmComm operations.
