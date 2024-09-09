Forwarding `sysmon` logs to Splunk is identical as forwarding Windows Event Logs. You can see detailed documentation [here](https://github.com/MyatKyawKaung/SIEM-Lab/blob/main/Log%20Forwarding/Forwarding%20Windows%20Event%20Logs.md)

Go to directory where Splunk configuration files are located. (C:\\Program Files\\SplunkUniversalForwarder\\etc\\system\\local)

![image01](https://github.com/user-attachments/assets/c6bebe7b-b0f2-4819-9a74-366941b43a20)

Configure `Inputs.conf` file to log Sysmon and **Save** the file
```
[WinEventLog://Microsoft-Window-Sysmon/Operational] 
disabled = false 
index = sysmon
renderXml = true
sourcetype = XmlWinEventLog:Microsoft-Windows-Sysmon/Operational
```
![image02](https://github.com/user-attachments/assets/e3a8a8ee-6a67-4246-bb3e-614da213be02)

Make sure you restart the splunk forwarder service. Press `Windows+R` > `services.msc`

![image03](https://github.com/user-attachments/assets/dba73cbb-78d1-4c38-8955-f7567b4f1f6c)

Change the splunk forwarder service account from NT/Service to Local System Account

![image04](https://github.com/user-attachments/assets/551415dd-2c40-4e2f-980f-93979a57b937)
![image05](https://github.com/user-attachments/assets/8dfa914a-bdae-4d94-9542-5ccae060e56e)

Restart the Splunk forwarder service

![image06](https://github.com/user-attachments/assets/298e3027-697a-43a2-84e9-e9823359a735)

Verify Sysmon Logs are forwarded to Splunk or not.

![image07](https://github.com/user-attachments/assets/e88515a3-d6c5-443e-8bfe-0a2c88031a62)
