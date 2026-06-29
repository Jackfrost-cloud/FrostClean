# FrostClean

# FrostClean v1.0.0

Initial release.

A PowerShell-based Windows cleanup utility with a live, animated console UI — progress bar, step-by-step status list, and a final before/after disk space summary.

## Features

- Self-elevates to Administrator automatically
- Animated terminal UI (header, progress bar, step list with live status)
- 20 cleanup steps covering:
  - Windows temp files & Prefetch
  - Windows Update cache
  - Windows event logs (Application, System, Security)
  - Thumbnail cache, Recycle Bin, WER crash reports
  - DNS cache
  - Browser caches (Brave, Edge)
  - App caches (Discord, Spotify, Roblox, Steam, VS Code)
  - GPU shader caches (NVIDIA/Intel)
  - Dev tool caches (npm, pip)
  - Windows Disk Cleanup (`cleanmgr`) and DISM component store cleanup (`/ResetBase`)
- Per-step freed space tracking (MB) and total before/after summary in GB

## Usage

```powershell
powershell -ExecutionPolicy Bypass -File .\FrostClean.ps1
```

## Known limitations (addressed in v2)

- No dry-run / preview mode — every run deletes immediately
- No logging — errors are silently discarded (`$ErrorActionPreference = 'SilentlyContinue'`)
- Clears the Security event log, which may not be desirable on systems with audit policies
- Runs `DISM /ResetBase` unconditionally, which is irreversible (removes the ability to uninstall superseded updates)
- If DISM exceeds its 180s timeout, the job is force-killed, which can interrupt the component cleanup mid-operation
