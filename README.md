# microsoft-defender-lab13-scan-lifecycle-investigation
## Overview

This lab demonstrates how Microsoft Defender records antivirus scan activity through Windows Defender Operational logs.

The objective is to investigate the complete scan lifecycle by triggering a Quick Scan and validating the corresponding Windows Defender events.

---

## Objectives

- Verify Microsoft Defender health
- Trigger a Quick Scan
- Observe scan lifecycle events
- Investigate Event ID 1000 (Scan Started)
- Investigate Event ID 1001 (Scan Completed)
- Correlate scan execution using Event Viewer and PowerShell

---

## Environment

- Windows 10
- Microsoft Defender Antivirus
- Windows Event Viewer
- Windows PowerShell

---

# Lab Workflow

1. Verify Defender is running
2. Start Quick Scan
3. Observe Quick Scan progress
4. Open Windows Defender Operational Log
5. Investigate Event ID 1000
6. Investigate Event ID 1001
7. Correlate PowerShell output with Event Viewer

---

## Event IDs Investigated

| Event ID | Description |
|----------|-------------|
|1000|Scan Started|
|1001|Scan Completed|

---

## PowerShell Commands

Verify Defender

```powershell
Get-MpComputerStatus
```

Start Quick Scan

```powershell
Start-MpScan -ScanType QuickScan
```

View Scan Events

```powershell
Get-WinEvent -LogName "Microsoft-Windows-Windows Defender/Operational" | Where-Object {$_.Id -in 1000,1001} | Select TimeCreated, Id, Message | Format-List
```

---

# Investigation Summary

Observed Defender initiating a Quick Scan and successfully completing it.

Validated:

- Scan ID
- Scan Type
- User
- Scan Parameters
- Scan Duration
- Scan Lifecycle

No threats were detected during the scan.

---

# MITRE ATT&CK

Although this activity represents legitimate administrative behavior, adversaries frequently abuse Defender scan operations to validate malware execution or modify security configurations.

| Technique | ID |
|-----------|----|
|Indicator Removal on Host|T1070|
|Impair Defenses|T1562|
|Modify Security Tools|T1562.001|

---

# Skills Demonstrated

- Microsoft Defender Investigation
- Event Viewer Analysis
- Windows Security Logs
- PowerShell Investigation
- Event Correlation
- Endpoint Security Monitoring
- SOC Investigation Workflow

---
