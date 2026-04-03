
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

Log Correlation flow:

<img width="344" height="280" alt="image" src="https://github.com/user-attachments/assets/0d0ace1f-96df-4774-8963-ef62a83e6f3e" />

We’ll simulate 3 different logs and connect them:

Step A — Create Correlated Log Table

<img width="860" height="220" alt="image" src="https://github.com/user-attachments/assets/06b3c9e6-72ff-462e-95ba-79e546f87a00" />

Step B — Correlate
Now connect the dots:
Same Source IP? → ✅ Yes
Sequence:
Failed logins → success → outbound traffic
Timing close together? → ✅ Yes

Step C — Identify Pattern
This is NOT random anymore.
This is a correlated attack pattern
Meaning:
Attacker tried passwords
Got access
Then communicated outside

Log Correlation Finding
Logs from authentication and network sources were correlated using the same Source IP (192.168.1.100). Multiple failed login attempts (Event ID 4625) were followed by a successful login (4624) and outbound traffic to 8.8.8.8.
This indicates a potential compromise where the attacker gained access and initiated external communication.

## Anomaly Detection
Anomaly detection is the process of identifying unusual patterns or activities that do not match normal behavior in a system.
Example: A user logging in at 3 AM from a different country when they usually log in during office hours.

Anomaly Detection flow:

<img width="258" height="267" alt="image" src="https://github.com/user-attachments/assets/574940bd-b541-4476-82f1-0d33e3051ce1" />

We’ll simulate normal vs abnormal behavior:

Step A — Create Log Data

| Timestamp        | User  | Location | Login Time | Status       |
| ---------------- | ----- | -------- | ---------- | ------------ |
| 2025-08-18 09:00 | vasvi | India    | 09:00 AM   | Normal Login |
| 2025-08-19 09:15 | vasvi | India    | 09:15 AM   | Normal Login |
| 2025-08-20 03:00 | vasvi | Russia   | 03:00 AM   | Suspicious   |


Step B — Identify Normal Behavior

From first two rows:
Login time → morning (9 AM)
Location → India
This is your baseline (normal behavior)

Step C — Detect Anomaly
Now look at last row:
Time → ❌ 3 AM (unusual)
Location → ❌ Russia (different country)
This is not normal

Step D — Analyst Thinking 🧠
Ask:
Same user? → ✅ Yes
Different pattern? → ✅ Yes
Risk? → ✅ High
Possible:
Account compromise
Unauthorized access

Anomaly Detection Finding
User "vasvi" typically logs in from India during morning hours (around 9 AM). However, a login was detected at 3:00 AM from Russia.
This behavior deviates from the normal pattern and indicates a possible unauthorized access or account compromise.



## Threat Intelligence
Threat intelligence is information about known cyber threats, such as malicious IP addresses, file hashes, or attacker techniques, used to detect and respond to attacks.
Example: Checking if an IP address in logs is listed as malicious in tools like VirusTotal or AlienVault OTX.

Threat Intelligence Flow

<img width="675" height="264" alt="image" src="https://github.com/user-attachments/assets/f4727bad-46a3-4f98-8b26-9f44962d6527" />

We will simulate checking an IP using VirusTotal

Step A — Pick a Sample IP
Use this:8.8.8.8
(Google DNS — will show mostly clean, good for learning)


Step B — Go to VirusTotal
Open browser
Go to:  https://www.virustotal.com

Step C — Search IP
Click Search tab
Paste IP:8.8.8.8
Press Enter

Step D — Observe Results
You will see:
Detection ratio (like 0/90 or similar)
Community score
Details about IP

Step E — Understand Output
If 0 detections → Likely safe
If many detections → Malicious
This is called IP reputation check

Threat Intelligence Finding
The IP address 8.8.8.8 was analyzed using VirusTotal. The results showed no malicious detections, indicating that the IP is likely safe.
This demonstrates how threat intelligence can be used to verify whether an IP address is associated with known threats.

## Incident Escalation
Incident escalation is the process of passing a security alert or incident to a higher-level team when it requires deeper investigation or has higher severity.
Example: A Tier 1 analyst escalates a confirmed unauthorized access incident to Tier 2 for further analysis.

Incident Escalation Flow

<img width="670" height="244" alt="image" src="https://github.com/user-attachments/assets/fb794d9f-b54c-4996-9ec2-23f58635ea7a" />

We will simulate a real escalation case

Step A — Define the Incident
Use this scenario:
Alert: Unauthorized access
Time: 2025-08-18 13:00
IP: 192.168.1.200
Technique: T1078 (Valid Accounts)

Step B — Think Like Tier 1 Analyst
Ask:
Is it suspicious? → ✅ Yes
Is it confirmed? → ✅ Yes
Can Tier 1 handle it? → ❌ No
So → Escalate to Tier 2

Incident Escalation Report
A high-priority alert was detected involving unauthorized access to Server-Y on 2025-08-18 at 13:00. The activity originated from IP address 192.168.1.200 and is associated with MITRE ATT&CK technique T1078 (Valid Accounts).
Initial analysis confirms suspicious login behavior. The affected system has been isolated to prevent further compromise.
This incident is being escalated to Tier 2 for deeper investigation and response.



## Evidence Preservation
Evidence preservation is the process of collecting and storing digital evidence in a secure and accurate way so it can be used for investigation or legal purposes.
Example: Creating a memory dump from a compromised system and generating a hash value to ensure its integrity.

Evidence Preservation Flow

<img width="677" height="277" alt="image" src="https://github.com/user-attachments/assets/25193882-efd6-450f-9c2a-bfa6ffee5e4c" />

We’ll simulate collecting evidence + hashing it

Step A — Create a Sample Evidence File
Open Notepad
Write:
This is a simulated memory dump from Server-Y.
Suspicious activity detected.
Save file as:
memory_dump.txt

Step B — Generate Hash (VERY IMPORTANT)
Now we prove the file is not changed.
If you are on Windows:
Open Command Prompt
Navigate to file location (example):
cd Desktop
Run:
certutil -hashfile memory_dump.txt SHA256
Output will look like:
SHA256 hash of file:
A1B2C3D4E5F6...
This is your evidence fingerprint


Step C — Understand Why Hash Matters
If file changes → hash changes ❌
Same hash → file is intact ✅
This proves evidence integrity

Step D — Document Evidence (VERY IMPORTANT)

Evidence Collection Record

| Item        | Description            | Collected By | Date       | Hash Value |
|-------------|------------------------|--------------|------------|------------|
| Memory Dump | Server-Y simulated dump | SOC Analyst  | 2025-08-18 | <PASTE HASH HERE> |

The evidence was collected and hashed using SHA256 to ensure integrity. The hash value confirms that the file has not been altered.






