# Scenario 1: Reverse Shell

Execution steps:
• Step 1: Launch a Reverse Shell to connect to the attacker's machine
![Figure 4.1: Launching Reverse Shell on the agent machine](run_reverse_shell.png)

• Step 2: The lsof-monitor service detects new outbound connections, the Wazuh Agent sends log information back to the Wazuh Manager, then analyzes the logs, compares them with IPs in the blacklist, and generates an alert.
![Figure 4.2: Wazuh detects and generates an alert](create_alert.png)

• Step 3: Based on the configuration file, the Wazuh Manager executes appropriate response actions. In this case, the response action will be to disable USB, kill the process, delete the malicious file, and isolate the agent machine from the Internet for deeper investigation.

![Figure 4.3: Killing the Reverse Shell process](kill_process.png)

![Figure 4.4: Deleting the Reverse Shell file and disabling USB](delete_file_and_disable_usb.png)

![Figure 4.5: Isolating the agent machine from the Internet](isolate_host.png)
