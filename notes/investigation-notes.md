# Investigation Notes

## Scenario

A Windows endpoint initiated a Microsoft Defender Quick Scan.

The objective was to validate the scan lifecycle using Windows Defender Operational logs.

---

## Evidence Collected

PowerShell

- Get-MpComputerStatus
- Start-MpScan -ScanType QuickScan
- Get-WinEvent

Windows Event Viewer

Microsoft-Windows-Windows Defender/Operational

---

## Event Timeline

### Event ID 1000

Scan Started

Observed:

- Scan ID
- Scan Type
- User
- Trigger
- Scan Resources
- Scan Priority

---

### Event ID 1001

Scan Completed

Observed:

- Same Scan ID
- Scan Duration
- Scan Parameters
- User
- Successful completion

---

## Correlation

Event ID 1000 and Event ID 1001 contained the same Scan ID, confirming both events belonged to the same Quick Scan operation.

---

## SOC Analysis

This activity is legitimate endpoint protection behavior.

Indicators supporting benign activity:

- Defender service healthy
- Quick Scan initiated by administrator
- Successful completion
- No abnormal Defender events
- No malware detections generated

---

## Findings

Status

Normal

Threat Detected

No

Investigation Result

Benign Defender Scan
