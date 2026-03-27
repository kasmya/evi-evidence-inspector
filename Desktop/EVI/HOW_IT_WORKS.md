# HOW IT WORKS - Detailed Technical Guide

## 🎯 Overview

EVI is a **terminal-based (TUI) log analyzer** built with Python + Rich library. It detects **timestamp gaps** in logs, classifying them by severity.

## 🔧 Architecture

```
main.py → tui.display.run_dashboard() → modes/*.py → core.engine.detect_gaps()
```

**Flow:**
1. Logo + intro (conversation.explainer)
2. Rich Layout dashboard
3. User choice → Mode → Engine → Results

## 🧠 Core Detection (core/engine.py)

**Algorithm:**
```python
parse timestamps → calculate deltas → threshold check → classify
```

**Thresholds:**
- LOW: 60-300s
- MEDIUM: 300-1800s
- CRITICAL: >1800s

**Output:** EngineStats (gaps list, severity)

## 📱 UI Flow (tui/)

**Layout (layout.py):** Split panels (Status | Findings)
**Display (display.py):** Input loop, mode dispatch

**Startup:**
- ASCII (main.py)
- Greeting (conversation/)
- Dashboard

## 📦 Modes

| Mode | File | Logic |
|------|------|-------|
| Forensic | modes/forensic.py | Static parse |
| Live | modes/live.py | Watchdog tail -f |
| Hybrid | modes/hybrid.py | Forensic + live |

## 🎨 Styling (Rich)

Panels, live updates, colors for severity.

## 📋 Setup & Extensibility

**Add Mode:** Copy modes/forensic.py → new/
**Change Threshold:** core/engine.py THRESHOLD = 60
**New Log Format:** engine.parse_line()

**Test:** test_logs/ (clean = good, tampered = gaps)

## 🧪 Testing

```
pytest test_logs/  # Add unit tests
```

## 🔮 Future (TODO.md)

- Export reports
- GUI version
- ML anomaly detection

## 📚 Dependencies

Rich (UI), Watchdog (live), Matplotlib (optional charts)

**File structure preserved exactly** - clone = your laptop folder.

