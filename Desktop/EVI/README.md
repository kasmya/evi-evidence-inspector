# EVI - Evidence Investigator (Log Tampering Detector)

**Easy Log Checker for Everyone**

**What is EVI?**
EVI finds **missing parts** in log files (like gaps in a story). Perfect for detecting if someone deleted evidence.

**Why use it?**
- Check if logs were tampered with
- See if your system was hacked
- Simple for beginners, powerful for pros

## 🚀 Start in 1 Minute

1. `git clone https://github.com/kasmya/evi-evidence-inspector.git`
2. `cd evi-evidence-inspector`
3. `pip install -r requirements.txt`
4. `python main.py`

**Press 4 for instant demo!**

## 📂 Where is Everything?

**Run:** `main.py` (this file starts EVI)

**Code Structure:**
```
┌─ main.py              ← RUN THIS
├── conversation/       ← EVI talks to you
├── core/              ← Finds gaps (engine.py)
├── tui/               ← Pretty terminal screen
├── modes/             ← 1.Forensic 2.Live 3.Hybrid
├── mascot/            ← EVI robot art
├── test_logs/         ← Demo files
│   ├── clean.log      ← Normal logs
│   └── tampered.log   ← BROKEN logs (gaps!)
├── requirements.txt   ← pip install
├── README.md          ← You are here
└── HOW_IT_WORKS.md    ← Tech details
```

**Test Logs Explained:**
- `test_logs/clean.log` = Perfect logs (no gaps)
- `test_logs/tampered.log` = Fake hacked logs (missing 30min = CRITICAL!)

## 🎮 How to Use

**Dashboard Options:**
- **1** Scan file (forensic) → `test_logs/tampered.log` [ENTER]
- **2** Watch live log
- **3** Scan + watch
- **4** Demo (no files needed!)
- **0** Exit

**Example Output:**
```
CRITICAL gap detected: 30 minutes missing!
Likely logs were deleted.
```

## 🤔 For Beginners

**What are logs?**
Computer diary (every action timestamped).

**What are gaps?**
```
10:00 Normal
10:30 ???? MISSING ????
11:00 Normal
```
→ EVI flags **30min gap = suspicious!**

## 📱 Screenshot Guide

1. Run → See logo + intro
2. Dashboard appears
3. Type **4** → See demo gaps
4. Type **1** → Scan tampered.log → See CRITICAL!

## 🔧 Quick Fixes

- Error "rich not found" → `pip install -r requirements.txt`
- No demo → Use test_logs/tampered.log

**Share:** Zip folder or clone repo!

**Repo:** https://github.com/kasmya/evi-evidence-inspector/tree/main
**Code:** All Python files in root + folders above.

⭐ Questions? Issues welcome!

