# 🤖 EVI - Evidence Investigator

**Simple Log Tampering Detector for Beginners**

EVI (Evidence Investigator) is a beginner-friendly tool that checks system logs for signs of tampering. It looks for **missing time gaps** that might indicate deleted entries (common in cyber attacks).

## 🎯 What Does EVI Do? (No Tech Background Needed)

Imagine logs are a timeline of your computer's activity. If there's a **big gap** (e.g., 30 minutes missing), EVI flags it as suspicious.

**Real-World Use:**
- Check if someone deleted log entries to hide hacking
- Verify system activity during incidents
- Monitor live logs for sudden gaps

**Classification (Easy to Understand):**
- **LOW**: Normal pause (like coffee break)
- **MEDIUM**: Unusual - check manually
- **CRITICAL**: Likely tampering!

## 🚀 Quick Start (5 Minutes)

1. **Clone & Enter:**
```
git clone https://github.com/kasmya/evi-evidence-inspector.git
cd evi-evidence-inspector
```

2. **Install:**
```
pip install -r requirements.txt
```

3. **Run:**
```
python main.py
```

4. **Demo (No Own Logs Needed):**
```
[ENTER at startup] → EVI > 4 → See tampering demo!
```

## 📱 What You See

```
EVI ASCII Logo
Full Intro (what EVI does)
Dashboard:
  📊 System Status     | 🔍 Findings
  [1-5 Actions]         | CRITICAL gaps found!
EVI > [type 1 for scan]
```

**Example Scan:**
- Input: `test_logs/tampered.log` [ENTER]
- Output: "CRITICAL gap: 30 minutes - logs likely deleted!"

## 📂 File Structure (Same as Your Laptop)

```
EVI/
├── main.py              # Run this!
├── requirements.txt     # pip install
├── README.md           # This file
├── HOW_IT_WORKS.md     # Technical details
├── TODO.md             # Future features
├── .gitignore          # Ignores junk
├── conversation/       # EVI talks/chat
├── core/               # Gap detection engine
├── mascot/             # EVI robot ASCII
├── modes/              # Scan/live/hybrid
├── test_logs/          # Demo files (tampered.log = bad example)
└── tui/                # Text UI (Rich terminal)
```

## 🎮 Usage Modes

| Choice | What | Example |
|--------|------|---------|
| **1 Forensic** | Analyze saved log | `test_logs/tampered.log` |
| **2 Live** | Watch log file real-time | System `/var/log/syslog` |
| **3 Hybrid** | Both above | Scan + watch |
| **4 Demo** | Fake tampering demo | No files needed |
| **5 Help** | Commands list |
| **0 Exit** | Goodbye |

## 🔍 How Gap Detection Works (Simple)

1. Read log timestamps (e.g., "2024-10-01 10:00:01")
2. Calculate gaps between lines (>60s = flag)
3. Classify: Low (1min), Medium (5min), Critical (30min+)

**Test Files:**
- `clean.log` = Normal (no flags)
- `tampered.log` = Gaps (CRITICAL!)

## 🛠️ Customize

- Edit `core/engine.py` threshold (line ~30)
- Add your logs to `test_logs/`
- Live: Point to `/var/log/auth.log`

## 📞 Troubleshooting

**"Module not found"** → `pip install -r requirements.txt`
**"Permission denied"** → Use sudo for system logs
**"No gaps"** → Try tampered.log demo

## 🤝 Share with Coworker

```
git clone https://github.com/kasmya/evi-evidence-inspector.git
cd evi-evidence-inspector
pip install -r requirements.txt
python main.py  # Press 4 for demo
```

**Non-Tech:** Just copy the folder + `python main.py`

---

⭐ **Star if useful!** Questions? Open issue.

