### In this demo, I follow the official Splunk documentation as a reference. 
https://docs.splunk.com/Documentation/Forwarder/8.2.6/Forwarder/InstallaWindowsuniversalforwarderfromaninstaller

Splunk Universal Forwarder download link;
Windows 10, 11  && Windows Server 2019, 2022 (64bits)

You can directly download Universal Forwarder by using following PowerShell cmdlets
```
Invoke-WebRequest -Uri "https://download.splunk.com/products/universalforwarder/releases/9.3.0/windows/splunkforwarder-9.3.0-51ccf43db5bd-x64-release.msi" -OutFile "C:\Users\MyatKyawKaung\Downloads\splunkforwarder-9.3.0-51ccf43db5bd-x64-release.msi"
```
![image01](https://github.com/user-attachments/assets/5fb3088f-6d63-4a27-84fd-b2c0360782e3)

You will see your downloaded Splunk Universal Forwarder installer

![image02](https://github.com/user-attachments/assets/8cdde7c0-2de8-44d7-a4e8-2ec99f743b78)

Right Click your installer and Set up wizard will pop up, Check License Agreement and Check below as shown in figure

![image03](https://github.com/user-attachments/assets/2f092d65-4daa-44e9-ab54-a07b512511c1)

Provide credentials for your universal forwarder

![image04](https://github.com/user-attachments/assets/dc3e1803-7f92-4dd7-9e26-a73860a34946)

Enter your Splunk Deployement Server's IP (In this case, I leave the everything and hit next since my lab doesn't include deployment server)

![image05](https://github.com/user-attachments/assets/1974aa0a-ce97-470e-a493-09c8285f8d9d)

Specify your Splunk Indexer's IP and Port where your Splunk server is listening on. (Yours will be different than mine)

![image06](https://github.com/user-attachments/assets/3be34bc9-87ec-4dd1-8fb8-7738733f8e61)

Click Install and wait untill Set up Wizard finish

![image07](https://github.com/user-attachments/assets/84e41758-0d8e-4374-b6b0-9e7b481ca7a5)
![image08](https://github.com/user-attachments/assets/5776c0d4-b849-49ba-b5da-5952dd20f59e)

Press **Windows+R** > Enter **services.msc**

![image09](https://github.com/user-attachments/assets/e82b54c3-f9a9-4f39-a4e1-4f6350f5dd18)

Search for Splunk Forwarder service, Right click and hit **restart**

![image10](https://github.com/user-attachments/assets/af3b040a-c10b-454d-aefe-2254ef8f47db)



