# SOC342 - CVE-2025-53770 SharePoint ToolShell Auth Bypass and RCE

## Overview

This repository contains the investigation and incident response documentation for a confirmed exploitation of CVE-2025-53770 (ToolShell) against an on-premises Microsoft SharePoint server.

The incident involved successful remote code execution, execution of malicious PowerShell commands, extraction of SharePoint Machine Keys, deployment of a webshell, and placement of additional malicious artifacts on the affected server.

## Alert Information

| Field          | Value                                                            |
| -------------- | ---------------------------------------------------------------- |
| Alert Name     | SOC342 - CVE-2025-53770 SharePoint ToolShell Auth Bypass and RCE |
| Event ID       | 320                                                              |
| Severity       | Critical                                                         |
| Status         | Confirmed True Positive                                          |
| Event Time     | 22-Jul-2025 01:07 PM                                             |
| Hostname       | SharePoint01                                                     |
| Destination IP | 172.16.20.17                                                     |
| Source IP      | 107.191.58.76                                                    |
| HTTP Method    | POST                                                             |

## Detection Summary

The alert was triggered after detecting a suspicious unauthenticated POST request targeting:

/_layouts/15/ToolPane.aspx?DisplayMode=Edit&a=/ToolPane.aspx

The request characteristics matched known exploitation patterns associated with CVE-2025-53770:

* Unauthenticated access attempt
* Large POST payload
* Spoofed Referer header
* SharePoint ToolPane.aspx abuse
* Potential remote code execution activity

## Investigation Outcome

Investigation confirmed successful exploitation of the SharePoint server.

Observed malicious activity included:

* Execution of Base64-encoded PowerShell payloads
* Extraction of SharePoint Machine Keys
* Deployment of payload.exe
* Installation of webshell spinstall0.aspx
* Creation of notes.txt artifact
* Post-exploitation activity on the host

## Indicators of Compromise

### Source IP

107.191.58.76

### Malicious Files

payload.exe

spinstall0.aspx

notes.txt

### Targeted URL

/_layouts/15/ToolPane.aspx?DisplayMode=Edit&a=/ToolPane.aspx

## Response Actions

* Contained SharePoint01 from the network
* Removed malicious files and webshell
* Blocked identified IOCs
* Initiated incident response procedures
* Performed forensic review and threat hunting
* Started remediation and recovery activities

## Conclusion

The incident was validated as a confirmed compromise resulting from exploitation of CVE-2025-53770. The attacker achieved remote code execution and deployed a webshell on the SharePoint server. Immediate containment and remediation actions were performed to prevent further impact.

Refer to investigation.md for detailed analysis and findings.