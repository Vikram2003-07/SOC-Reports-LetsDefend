# SOC170 - Passwd Found in Requested URL - Possible LFI Attack

## Overview

This investigation relates to a web application security alert triggered by a request attempting to access the `/etc/passwd` file through a Local File Inclusion (LFI) technique.

## Alert Details

* Event ID: 120
* Rule: SOC170 - Passwd Found in Requested URL - Possible LFI Attack
* Event Time: March 01, 2022, 10:10 AM
* Hostname: WebServer1006
* Destination IP: 172.16.17.13
* Source IP: 106.55.45.162
* HTTP Method: GET
* Device Action: Allowed

## Requested URL

https://172.16.17.13/?file=../../../../etc/passwd

## Summary

An external source IP attempted to access the Linux password file (`/etc/passwd`) using directory traversal sequences in the URL. The target server is a Windows-based system, making the requested file path invalid. The server responded with HTTP status code 500 and a response size of 0 bytes, indicating the attack attempt was unsuccessful.

## Investigation Outcome

* Classification: True Positive
* Attack Type: Local File Inclusion (LFI) Attempt
* Impact: No evidence of successful file disclosure
* Status: Failed Attack Attempt

## Conclusion

The alert correctly identified a malicious attempt to exploit a potential LFI vulnerability. The request failed because the targeted file does not exist on the Windows server, resulting in an internal server error.