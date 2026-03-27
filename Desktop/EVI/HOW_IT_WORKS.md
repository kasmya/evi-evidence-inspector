# HOW IT WORKS — Complete Technical Deep Dive

## 🎯 Executive Summary

EVI = **Evidence Investigator** — automated log gap detector for cybersecurity investigations.

**Core Problem Solved:**
Attackers delete logs → Timeline breaks → EVI finds the gaps.

## 🔬 Detailed Architecture

```
┌─ main.py (Entry)
│
├─ conversation/ (EVI Persona)
│  └─ explainer.py (Intro, help text)
│
├─ core/ (Detection Engine)
│  └─ engine.py (Timestamp parsing, gap calc, severity)
│
├─ tui/ (User Interface)
│  ├── layout.py (Dashboard panels)
│  └── display.py (Input loop, mode dispatch)
│
├─ modes/ (Analysis Types)
│  ├── forensic.py (Static analysis)
│  ├── live.py (Real-time tail -f)
│  └── hybrid.py (Forensic + live)
│
├─ mascot/ (Visuals)
│  └─ robot.py (ASCII, voice lines)
│
└─ test_logs/ (Samples)
   ├── clean.log (Normal)
   └── tampered.log (Gaps demo)
```

## ⚙️ Core Engine Deep Dive (core/engine.py)

### Timestamp Parsing

```python
def parse_line(line):
    # Matches common formats:
    # "2024-10-01 10:00:01 INFO ..."
    # "Oct 1 10:00:01 server ..."
    return datetime object
```

### Gap Calculation

```python
def detect_gaps(log_path):
    timestamps = [parse_line(line) for line in file]
    gaps = [t2 - t1 for t1, t2 in zip(timestamps, timestamps[1:])]
    return classify_gaps(gaps)
```

### Severity Logic

```
gap_seconds < 60 → LOW
60 ≤ gap < 300 → MEDIUM  
gap ≥ 300 → CRITICAL
```

## 🖥️ TUI Deep Dive

### Layout System (Rich)

**4 Panels:**
1. **Header** — EVI title
2. **System Status** — Logs loaded, last scan
3. **Findings** — Gap count, max severity
4. **Actions** — Numbered menu
5. **Prompt** — "EVI > "

### Event Loop

```
while True:
    show_dashboard(stats)
    choice = input("EVI > ")
    dispatch_mode(choice)
```

## 📡 Modes Deep Dive

### 1. Forensic (Static)

```
file → parse_all → engine.detect_gaps → display_results
```

### 2. Live Monitoring

```
watchdog + tail -f → real-time parse → immediate gap alert
```

### 3. Hybrid

```
forensic( historical ) + live( future )
```

### 4. Demo

```
tampered.log → guaranteed CRITICAL → teaching example
```

## 🎨 EVI Persona System

**Voice Lines** (mascot/robot.py):
```
categories: welcome, scanning, gap, complete
random.choice(VOICE_LINES[category])
```

**Explainer** (conversation/explainer.py):
* Startup narrative
* Gap explanations
* Next steps guidance

## 📊 Data Flow Diagram

```
User Input → Mode Selection → Log Parser → Timeline → Gap Detector → Classifier → Display → User
                    ↑                                                                 ↓
                 test_logs/ ← Demo Data ←───────────────────────────────────────────────
```

## 🧪 Test Logs Explained

**clean.log** (8 lines, 1s intervals):
```
2024-10-01 10:00:01 → 10:00:10 (normal)
```

**tampered.log** (gaps):
```
10:00:01
10:04:10 (4min gap - MEDIUM)
10:34:45 (30min gap - CRITICAL)
```

## 🔧 Configuration Points

1. **Thresholds** — `core/engine.py` THRESHOLD vars
2. **Log Formats** — `parse_line()` regexes
3. **Voice** — `mascot/robot.py` VOICE_LINES
4. **UI** — `tui/layout.py` panels

## 🛠️ Extensibility

**New Mode:**
```
cp modes/forensic.py modes/custom.py
# Modify logic
display.py: add "6: Custom"
```

**New Format:**
```
engine.py: add parse_line regex
```

## 📈 Performance

* Single file: <1s
* Live: 1Hz polling
* Memory: O(n) lines

## 🚨 Error Handling

* Invalid timestamps → Skip line
* Permission denied → User prompt
* Empty file → "No activity detected"

## 📱 Complete Startup Sequence

1. ASCII logo (`main.py`)
2. Separator (`mascot/robot.py`)
3. Greeting (`conversation/explainer.py`)
4. Dashboard (`tui/layout.py`)
5. Input loop (`tui/display.py`)

## 🔍 Source Code Map

```
main.py (100 lines) - Orchestration
core/engine.py (150 lines) - Intelligence
tui/display.py (200 lines) - User experience
tui/layout.py (100 lines) - Visuals
modes/*.py (50 lines each) - Analysis variants
conversation/explainer.py (100 lines) - Personality
```

**Total: ~1000 LOC** — readable, modular.

## 🎉 Ready for Production

✅ Self-contained
✅ Zero dependencies beyond requirements.txt
✅ Interactive + documented
✅ Demo data included
✅ Extensible design

**Deploy:** Clone → pip → python main.py

---

**For Developers:** See individual .py comments
**For Users:** README + demo mode
**For Auditors:** Gap reports + timestamps

**EVI: Because logs lie by omission.**

