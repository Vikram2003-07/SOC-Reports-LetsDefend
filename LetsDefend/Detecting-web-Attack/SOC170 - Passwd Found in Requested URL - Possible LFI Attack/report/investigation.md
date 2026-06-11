# Investigation Report

## Alert Information

| Field          | Value                                                        |
| -------------- | ------------------------------------------------------------ |
| Event ID       | 120                                                          |
| Rule           | SOC170 - Passwd Found in Requested URL - Possible LFI Attack |
| Hostname       | WebServer1006                                                |
| Source IP      | 106.55.45.162                                                |
| Destination IP | 172.16.17.13                                                 |
| HTTP Method    | GET                                                          |
| Device Action  | Allowed                                                      |

## Observations

### Suspicious Request

The following URL was requested:

https://172.16.17.13/?file=../../../../etc/passwd

The attacker attempted to traverse directories and access the sensitive Linux file `/etc/passwd`, a common indicator of Local File Inclusion (LFI) exploitation attempts.

### Threat Intelligence Review

#### VirusTotal

* Source IP: 106.55.45.162
* Result: 0 security vendors flagged the IP as malicious.

#### Cisco Talos

* Reputation: Neutral

### Server Response Analysis

* HTTP Status Code: 500
* Response Size: 0 Bytes

The web server generated an internal error and did not return any file content to the requester.

### Environment Validation

The destination host is a Windows server.

Since `/etc/passwd` is a Linux system file and does not exist on Windows systems, the requested resource could not be accessed.

## Assessment

An external actor originating from China attempted to exploit a possible LFI vulnerability by requesting the Linux password file through directory traversal techniques.

The attack was unsuccessful because:

1. The target server is Windows-based.
2. The requested Linux file does not exist on the host.
3. No file content was returned.
4. The server responded with HTTP 500 Internal Server Error.

## Verdict

* True Positive
* Malicious LFI Attempt Detected
* Exploitation Failed
* No Evidence of Data Exposure
