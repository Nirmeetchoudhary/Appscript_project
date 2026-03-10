# 💎 Jewelry Production Tracking System

A real-time jewelry order and production tracking system built using **Google Forms**, **Google Sheets**, **Apps Script**, and **Looker Studio** — designed for MIS Executive operations in a jewelry manufacturing business.

---

<img width="1911" height="697" alt="image" src="https://github.com/user-attachments/assets/0755eef6-fc90-486f-8142-7ad9e9dc93dd" />


## 🔗 Live Links

| Module | Link |
|--------|------|
| 📋 Stage Start Form | [Open Form](https://forms.gle/U1rAVSwEnLbyKjtv5) |
| ✅ Stage End Form | [Open Form](https://forms.gle/kcV9gAD7zHsSSp3g8) |
| ⚠️ Delay Report Form | [Open Form](https://forms.gle/Lzb6XxnavYAxeeRg6) |
| 📊 Looker Studio Dashboard | [View Dashboard](https://lookerstudio.google.com/s/hM2iXs0v9NE) |

---

## 🏗️ System Architecture
```
Worker fills Google Form
        ↓
Google Sheets (Auto data storage)
        ↓
Apps Script (Automation + Email Alerts)
        ↓
Looker Studio (Live Dashboard)
```

---

## 📌 Production Workflow

Every jewelry order passes through 4 stages in sequence:
```
1. Melting → 2. Designing → 3. Polishing → 4. Hallmarking → ✅ Ready for Delivery
```

Only one stage is active at a time. Workers log each stage via Google Forms.

---

## 📂 Google Sheets Structure

| Sheet Tab | Purpose | Data Source |
|-----------|---------|-------------|
| `Stage_Start_Responses` | Logs when a worker begins a stage | Auto — Form 1 |
| `Stage_End_Responses` | Logs when a worker completes a stage | Auto — Form 2 |
| `Delay_Responses` | Logs delay reasons and estimated hours | Auto — Form 3 |
| `Production_Master` | Combined tracking view with formulas | Formula-driven |
| `Dashboard_Summary` | Aggregated MIS metrics | Formula-driven |

---

## 📝 Google Forms

### Form 1 — Stage Start
Workers fill this when they **begin** a production stage.
- Order ID
- Worker Name & Phone
- Production Stage (Melting / Designing / Polishing / Hallmarking)
- Jewelry Type (Ring / Necklace / Bracelet)
- Gold Weight (grams)
- Starting Notes

### Form 2 — Stage End
Workers fill this when they **complete** a production stage.
- Order ID
- Worker Name & Phone
- Stage Completed
- Quality Status (Passed / Failed / Needs Rework)
- Issues faced

### Form 3 — Delay Report
Workers fill this when a stage is **stuck or delayed**.
- Order ID
- Worker Name & Phone
- Stage Facing Delay
- Reason (Material Shortage / Machine Issue / Worker Absent / Quality Issue / Other)
- Estimated Delay Hours
- Problem Description

---

## ⚙️ Apps Script Automation

Located in: `Extensions → Apps Script` inside the Google Sheet

### Features

**1. Delay Detection — runs every 1 hour automatically**
- Scans all `In Progress` stages in `Production_Master`
- If any stage exceeds 24 hours, it:
  - Highlights the row in 🔴 red
  - Sends an email alert to the manager with Order ID, Stage, Worker Name, and Delay Hours

**2. Hallmarking Completion Trigger**
- Fires when Form 2 is submitted
- If Stage = `Hallmarking` and Quality = `Passed`:
  - Automatically moves the order to `Ready_For_Delivery`
  - Records production completion time
  - Calculates total turnaround time (TAT)

### Triggers Setup

| Function | Trigger Type | Frequency |
|----------|-------------|-----------|
| `checkDelays` | Time-driven | Every 1 hour |
| `onFormSubmit` | On form submit | Instant |

---

## 📊 Looker Studio Dashboard

**Data Sources connected:**
- `Production_Master` — for live order tracking table
- `Dashboard_Summary` — for scorecard metrics

**Charts included:**

| Chart | Type | Shows |
|-------|------|-------|
| Total Orders | Scorecard | Count of unique Order IDs |
| Completed Stages | Scorecard | Count of completed stages |
| Delayed Stages | Scorecard (Red) | Count of delayed stages |
| Avg Stage Duration | Scorecard | Average hours per stage |
| Delay Hours by Stage | Bar Chart | Which stage delays most |
| Stage Status Breakdown | Pie Chart | In Progress vs Completed |
| Worker Performance | Bar Chart | Average hours per worker |
| Live Production Log | Table | Full order-wise tracking |

---

## 🚀 How to Use

**For Workers:**
1. Receive the 3 form links on WhatsApp from your supervisor
2. 🟢 Fill **Stage Start Form** when you begin a stage
3. 🔴 Fill **Stage End Form** when you finish a stage
4. 🟡 Fill **Delay Report Form** if anything is stuck

**For MIS Executive / Manager:**
1. Open the Looker Studio dashboard for live overview
2. Open `Production_Master` sheet for detailed tracking
3. Delay email alerts arrive automatically every hour

---

## 🛠️ Tech Stack

| Tool | Usage |
|------|-------|
| Google Forms | Data entry by workers |
| Google Sheets | Data storage + formulas |
| Google Apps Script | Automation + email alerts |
| Looker Studio | Visual dashboard |

---

## 📁 Repository Structure
```
Appscript_project/
│
├── README.md                  # This file
├── apps_script/
│   └── Code.gs                # Full Apps Script automation code
├── sheets/
│   └── formulas.md            # All Google Sheets formulas used
└── dashboard/
    └── looker_config.md       # Looker Studio chart configuration
```

---

## 👤 Author

**Manoj Ornament Jewel**
MIS Executive Project — Jewelry Production Tracking System

---

## 📄 License

This project is for internal business operations use only.
