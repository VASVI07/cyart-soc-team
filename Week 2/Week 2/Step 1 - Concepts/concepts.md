
## Log Analysis
Log analysis is the process of reviewing system logs to understand what activities happened in a system. Logs record events like logins, file access, or network activity.
Example: Checking login logs to identify multiple failed login attempts from the same IP address.

Log Analysis Flow

![Screenshot 2026-04-03 114103](https://github.com/user-attachments/assets/aef819be-69b9-4608-b2d0-51ef6d144a07)

Create Sample Log Data
| Timestamp        | Event ID | Source IP    | Status        |
| ---------------- | -------- | ------------ | ------------- |
| 2025-08-18 12:00 | 4625     | 192.168.1.10 | Failed Login  |
| 2025-08-18 12:01 | 4625     | 192.168.1.10 | Failed Login  |
| 2025-08-18 12:02 | 4625     | 192.168.1.10 | Failed Login  |
| 2025-08-18 12:03 | 4624     | 192.168.1.10 | Success Login |

4625 = Failed login
4624 = Successful login

Analyze the Log
Now think like a SOC analyst:
Ask:
Same IP? → ✅ Yes (192.168.1.10)
Multiple failed attempts? → ✅ Yes (3 times)
Then success? → ✅ Yes

Identify Suspicious Pattern
Conclusion:
This looks like a brute force attack
Why?
Repeated failures
Followed by success
Same IP

Log Analysis Finding:
Multiple failed login attempts (Event ID 4625) were observed from IP 192.168.1.10, followed by a successful login (Event ID 4624). This indicates a possible brute force attack.

## Log Correlation
Log correlation is the process of connecting multiple logs from different sources to identify patterns or detect suspicious activity.
Example: Multiple failed login attempts followed by a successful login and unusual outbound traffic from the same IP address.

## Anomaly Detection
Anomaly detection is the process of identifying unusual patterns or activities that do not match normal behavior in a system.
Example: A user logging in at 3 AM from a different country when they usually log in during office hours.

## Threat Intelligence
Threat intelligence is information about known cyber threats, such as malicious IP addresses, file hashes, or attacker techniques, used to detect and respond to attacks.
Example: Checking if an IP address in logs is listed as malicious in tools like VirusTotal or AlienVault OTX.

## Incident Escalation
Incident escalation is the process of passing a security alert or incident to a higher-level team when it requires deeper investigation or has higher severity.
Example: A Tier 1 analyst escalates a confirmed unauthorized access incident to Tier 2 for further analysis.

## Evidence Preservation
Evidence preservation is the process of collecting and storing digital evidence in a secure and accurate way so it can be used for investigation or legal purposes.
Example: Creating a memory dump from a compromised system and generating a hash value to ensure its integrity.
