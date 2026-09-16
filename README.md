

Linux Log Investigation

1. Objective

The objective of this investigation was to examine Linux system logs and identify authentication activity, user sessions, privilege escalation activity, system warnings, and any indicators of suspicious behavior.

The investigation was performed as a practical SOC Analyst exercise to understand how Linux logs can be used to investigate security-related events.

⸻

2. Environment

Operating System: Kali Linux
Environment: Virtual Machine
Primary User: kali
Investigation Type: Linux Log Analysis
Role: Junior SOC Analyst / Security Analyst

⸻

3. Logs Investigated

The investigation focused primarily on:

* journalctl system logs
* Authentication/session activity
* sudo activity
* System warnings
* Login/session events
* System boot information

⸻

4. Evidence Collection

The following commands were used during the investigation:

ls -lag /var/log

Used to review available Linux log files and their permissions.

whoami

Used to identify the current logged-in user.

sudo journalctl --since "24 hours ago" | grep -Ei "accepted|session opened"

Used to identify successful authentication and session-opening events.

sudo journalctl -p warning

Used to review system events recorded at warning level.

⸻

5. Investigation Findings

5.1 Successful Authentication

The logs showed a successful local desktop login for the user:

User: kali

The login occurred through LightDM, the graphical login manager.

A LightDM session was also observed. This represents the graphical login screen/service rather than an additional human user.

Finding

A legitimate local user session was identified.

⸻

5.2 Failed Authentication

No failed authentication attempts were identified in the portions of the logs reviewed.

There was no evidence of repeated failed login attempts or an obvious brute-force pattern.

Finding

No suspicious failed authentication activity was identified in the reviewed logs.

⸻

5.3 Sudo Activity

Multiple sudo sessions were observed where:

kali → root

The activity occurred repeatedly while the investigation was being performed.

Analysis

The sudo activity is consistent with the user executing administrative commands during the investigation.

There was no evidence from the reviewed events that another unknown user obtained root privileges.

Finding

Privilege escalation activity was observed, but it appeared consistent with legitimate administrative activity.

⸻

5.4 Cron Activity

Several CRON sessions were recorded for:

root

These occurred repeatedly throughout the period examined.

Analysis

Cron is a Linux scheduling mechanism used to automatically execute tasks.

The repeated root sessions are therefore not automatically indicators of compromise. They are consistent with scheduled system tasks.

Finding

No suspicious behavior was identified from the observed Cron sessions.

⸻

6. System Warning Analysis

The warning-level logs contained several system and service warnings.

Some important observations included:

CPU / Virtualization Warnings

Messages relating to Spectre/RETBleed and CPU features were observed.

These appeared to be system or virtualization-related warnings rather than evidence of an active attack.

Desktop Service Warnings

Warnings involving services such as:

* GNOME Keyring
* WirePlumber
* Colord
* OBEX

were observed.

These appeared to be desktop/service issues rather than authentication or security incidents.

Systemd Compatibility Warnings

Warnings involving older-style services such as:

* dns2tcp
* inetsim
* stunnel4
* ptunnel

were observed.

These tools are present in the Kali environment and the messages were related to service initialization rather than evidence that an attacker was using them.

⸻

7. Previous Boot Activity

Some warning events were dated May 18, representing an older system boot.

The logs showed:

* Hardware/virtualization initialization messages
* LightDM session activity
* A local kali desktop session
* An unclean system journal shutdown

These events were separated from the more recent investigation activity.

Finding

The older boot events did not provide evidence of malicious authentication activity.

⸻

8. Investigation Timeline

Event	Activity	Assessment
May 18	System boot and LightDM sessions	Normal system activity
May 18	kali local desktop session	Legitimate local login
May 18	Unclean journal shutdown warning	System issue, not confirmed security incident
Sept. 15	kali local desktop login	Legitimate local login
Sept. 15	Multiple sudo sessions	Consistent with administrative investigation
Sept. 15	Repeated Cron sessions	Scheduled system activity
Sept. 15	System warnings	Mostly service/VM-related

⸻

9. SOC Analysis

From the available evidence, the following observations were made:

* The primary interactive user was kali.
* Successful local authentication was observed.
* No failed authentication attempts were identified in the reviewed logs.
* No remote/SSH authentication activity was identified in the reviewed evidence.
* Multiple sudo sessions were observed and were consistent with the investigation activity.
* Root Cron sessions appeared consistent with scheduled tasks.
* Several system warnings were identified, but they did not provide clear evidence of compromise.
* Older May 18 events were separated from the more recent investigation activity.

⸻

10. Security Assessment

Based on the logs reviewed, no clear indicators of compromise were identified.

The observed activity was primarily consistent with normal local system usage, scheduled tasks, administrative commands, and expected Kali Linux services.

This assessment is limited to the logs and time periods that were reviewed during this investigation.

⸻

11. SOC Conclusion

The Linux log investigation demonstrated how a SOC Analyst can use system logs to investigate authentication, user sessions, privilege escalation, scheduled tasks, and system warnings.

The investigation did not identify a confirmed security incident within the reviewed evidence.

The exercise reinforced the importance of:

* Reviewing authentication logs
* Identifying legitimate versus suspicious sessions
* Investigating sudo activity
* Understanding scheduled tasks
* Separating system errors from security incidents
* Building a timeline from log evidence

⸻

12. Evidence / Screenshots

The following screenshots should be added to the GitHub project:

1. /var/log directory listing
2. Current user (whoami)
3. Authentication/session log output
4. sudo activity
5. Warning-level journal output
6. Relevant timeline evidence

Screenshots should be placed in an evidence/ folder.

⸻

13. Project Skills Demonstrated

Technical Skills

* Linux command line
* Linux log analysis
* journalctl
* Authentication investigation
* User/session analysis
* sudo investigation
* Cron analysis
* System troubleshooting
* Security event interpretation
* SOC-style documentation

SOC Skills

* Evidence collection
* Event analysis
* Timeline construction
* Distinguishing normal activity from suspicious activity
* Documenting security findings
* Writing an investigation conclusion
