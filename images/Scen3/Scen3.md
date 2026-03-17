# Scenario 3: Command & Control Server Communication

### Achieved Results:

After the victim launches the malware, Wazuh will detect the alerts and display them on the Dashboard as shown in Figure 4.12.
![Figure 4.12: Wazuh detects C2 server behaviors through rules 100006, 100007, 100008, and 100013](alert-c2-server.png)

Regarding Active-Response (Figure 4.13), it reacts to these malicious actions by terminating the process, isolating the malware into the quarantine directory, then blocking inbound and outbound connections of the Linux Endpoint, and finally reporting back (this could be logging or reporting via email/Slack).
![Figure 4.13: Response actions upon detecting the C2 server](c2-ar-new.png)

As for the malware on the victim's machine, its process has been terminated and it has been isolated into the quarantine directory (Figure 4.14). When conducting a short experiment by copying and re-running the malware file, the text `[+] Payload downloaded: 14135296 bytes` is no longer printed and there is no longer a connection to the C2 server. (Figure 4.15)

![Figure 4.14: Malicious file isolated into the Quarantine directory](quarrantine-stager.png)

![Figure 4.15: Malicious file process terminated and no longer connecting to C2](malware-terminated.png)
