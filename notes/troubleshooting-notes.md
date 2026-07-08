# Troubleshooting Notes

## Problem

Start-MpScan returns:

"A scan is already in progress."

### Cause

Another Defender scan is currently running.

### Resolution

Wait for the scan to complete before starting another scan.

---

## Problem

Event ID 1000 not found.

### Cause

Defender scan never started.

### Resolution

Run:

```powershell
Start-MpScan -ScanType QuickScan
```

---

## Problem

Event ID 1001 missing.

### Cause

The scan has not completed yet.

### Resolution

Allow the scan to finish, then refresh Event Viewer.

---

## Problem

No Windows Defender Operational logs.

### Cause

Wrong Event Log selected.

### Resolution

Open:

Applications and Services Logs

↓

Microsoft

↓

Windows

↓

Windows Defender

↓

Operational

---

## Problem

PowerShell returns no events.

### Cause

Incorrect Event Log name.

### Correct command

```powershell
Get-WinEvent -LogName "Microsoft-Windows-Windows Defender/Operational"
```

---

## Problem

Microsoft Defender not responding.

### Verify Defender

```powershell
Get-MpComputerStatus
```

Ensure:

- AMServiceEnabled = True
- AntivirusEnabled = True
- Real-time protection enabled

---

## Lesson Learned

Always correlate:

- Event Viewer
- PowerShell
- Scan ID
- Scan timestamps

to validate the full Defender scan lifecycle during a SOC investigation.
