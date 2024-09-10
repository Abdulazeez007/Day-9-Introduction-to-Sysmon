# Day-9-Introduction-to-Sysmon

In today’s cybersecurity landscape, having robust visibility into your endpoints is crucial. Without proper monitoring, it can be challenging to understand what happened on an endpoint during a potential compromise. For Windows endpoints, logging is enabled by default, but the settings don’t capture all critical events, such as process creation. To address this, we can configure auditing settings or install Sysmon — a powerful tool that provides detailed insights during investigations.

## What is Sysmon?

Sysmon (System Monitor) is part of the Microsoft Sysinternals Suite and offers extensive telemetry data that enhances your ability to detect malicious activities. It can monitor a wide range of events, including process creation, network connections, file creation, and more. Sysmon is highly customizable, allowing you to control what events should be logged using a configuration file.

The latest version of Sysmon, **15.15**, supports 30 different event IDs, each providing detailed information about specific system activities. Below are some of Sysmon’s key capabilities.

## Key Capabilities of Sysmon

- **Process Creation Logging**: Logs process creation events with full command lines for both current and parent processes. Sysmon also provides a unique Process GUID for correlating related events.
- **File Hashing**: Captures SHA1, MD5, SHA256, and IMPHASH of process image files, enabling security teams to perform OSINT to gain additional context.
- **Session GUIDs**: Each event includes a session GUID, allowing easy correlation of actions within the same logon session.
- **DLL and Driver Loading**: Monitors the loading of DLLs and drivers, including their signatures and hashes to detect suspicious or unsigned modules.
- **Disk and Volume Access**: Logs raw read access to disks and volumes, potentially indicating low-level attacks.
- **Network Connection Monitoring**: Logs network connections, capturing source processes, IP addresses, ports, and hostnames. This is disabled by default but can be enabled in the configuration file.
- **File Creation Time Monitoring**: Detects changes in file creation timestamps, a common tactic used by malware to tamper with evidence.
- **Dynamic Configuration Reload**: Automatically reloads configuration changes from the registry without restarting Sysmon.
- **Rule-Based Filtering**: Supports dynamic rule filtering to include or exclude specific events, focusing on the most relevant data.
- **Boot Process Monitoring**: Captures early boot process events, detecting advanced kernel-mode malware activity.

![insert image here](image.jpg)

**Sysmon Event IDs and Descriptions**

### The Power of Process GUID

One of the key fields that Sysmon provides is the **Process GUID**, a unique identifier used to correlate events across different logs. This offers a clear picture of an attacker’s movements within the system. For example, if a Command and Control (C2) process establishes a connection to an external IP using a non-standard port, you can trace which process made the connection using the Process GUID.

### Important Event IDs in Sysmon

Understanding Sysmon Event IDs helps you focus on critical activities for threat hunting. Some key Event IDs include:

- **Event ID 1: Process Creation**  
  Tracks newly created processes, including full command lines. If malware is executed, Sysmon Event ID 1 will be generated, tracking the activity. The file hash is also logged, aiding security teams in gathering more information about the malicious file.

- **Event ID 3: Network Connection**  
  Disabled by default and must be enabled via the configuration file. It tracks network connections initiated by processes, including source and destination IP addresses and ports. This is invaluable for identifying suspicious outbound connections.

- **Event IDs 6, 7, 8: Driver/Image Load and Create Remote Thread**  
  These events help detect defense evasion techniques like process injection, where an attacker injects code into another process to evade detection. Event ID 7 (Image Load) is disabled by default and must be enabled if needed.

- **Event ID 10: Process Access**  
  This is crucial for monitoring potential credential access attempts on the LSASS process. Attackers often attempt to read LSASS memory to steal credentials for lateral movement.

## Conclusion

Sysmon is a powerful tool that provides deep visibility into endpoint activities. While its default settings offer robust monitoring, customizing it with a configuration file allows you to focus on critical events. By leveraging Sysmon’s event data — such as process creation, network connections, and DLL loading — security teams can enhance their threat-hunting efforts and improve detection, investigation, and response to advanced threats.

If you’re looking to improve your organization’s endpoint monitoring capabilities, integrating Sysmon into your cybersecurity strategy is a great place to start. With the right configuration and an understanding of its valuable event IDs, Sysmon can be a game-changer in your defense arsenal.
