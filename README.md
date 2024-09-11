🛡️ **Day9** - MYDFIR **30DAYSSOCChallenge**: Installing Sysmon on Windows Server 2022 🛡️
---

Today, We took another exciting step in building a robust SOC infrastructure by installing Sysmon (System Monitor) on my Windows Server 2022. Sysmon is a key tool for monitoring and logging critical system events that aid in detecting malicious activity and understanding attack vectors.

🎯 Why Sysmon?
Sysmon extends Windows' logging capabilities, enabling the collection of detailed information about process creations, network connections, and changes to file creation time. It is handy for threat hunting and incident detection in Security Operations Centers (SOC).

Steps to Install Sysmon
🔗 **Download Sysmon**:
I started by downloading Sysmon from the official Microsoft Learn website. You can find the download link here: https://lnkd.in/dGcT8Dey

🗂️ **Extract the Files**:
Once downloaded, I extracted the files to a folder on the Windows Server. The zip contains the executable needed for installation: sysmon.exe.

⚙️ **Run the Installation**:
I installed Sysmon using the following command in PowerShell (as Administrator): **.\Sysmon.exe* -i sysmonconfig.xml*

📝 **Custom Configuration**:
For the configuration, I opted for hashtag#Olaf Sysmon configuration as it is widely recognized and covers key event IDs essential for security monitoring. You can download it from their GitHub repository.

🔍 **Verify the Installation**:
After installation, I verified that Sysmon was running by checking the service status.
 
Additionally, I reviewed the logs generated in Event Viewer under Applications and Services Logs > Microsoft > Windows > Sysmon to ensure the expected event IDs were being captured.
📊 Top Event IDs to Monitor:
Now that Sysmon is up and running, I’ll focus on monitoring these critical event IDs:

---
1️⃣ **Event ID 1**: Process Creation
--
🛡️ **Event ID 1116**: Antimalware Detection
--
⚔️ **Event ID 1117**: Antimalware Action Taken
--
🚨  **Event ID 5001**: Real-Time Protection Disabled
--
🔍 **Event ID 22**: DNS Query and many others as we progress on.
--

🚀 **Next Steps**
With Sysmon fully operational, I'll be integrating it into the ELK stack for centralized log management and analysis. This will enhance our ability to detect and respond to potential threats in real-time.

Stay tuned for more updates as I continue my journey in the MYDFIR SOC Challenge!

CyberSecurity Sysmon SOCChallenge IncidentResponse WindowsServer ThreatDetection **DFIR**
