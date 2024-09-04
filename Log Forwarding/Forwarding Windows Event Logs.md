### This demonstration will showcase how to ingest Windows Event Logs to Splunk

Check and change default host name for easy investigation. (If you have already changed your host name after Windows installation, you can skip this part)

```
$env:COMPUTERNAME
Rename-Computer -NewName MKK_WINDOWS_VM
```
![image01](https://github.com/user-attachments/assets/b670ad6b-62a2-417d-ba55-08d3a2652bdb)

**Restart your computer**

```
Restart-Computer
```

Before we configuring Splunk forwarder, we need to create Windows Firewalls rule to allow our traffic to Splunk indexer.
## Creating Windows firewall rule for outbound connection to Indexer

Press **Windows+R** and enter **firewall.cpl**

![image02](https://github.com/user-attachments/assets/1c963740-dd14-40c2-aba4-ccfed3af419b)


Go to **Advanced Settings**

![image03](https://github.com/user-attachments/assets/5c5b7099-585f-4e99-a144-c221e1595e00)


In Advanced Settings, Select **Outbound Rules** > **Click New Rule**

![image04](https://github.com/user-attachments/assets/fa4a7ea9-b3cb-42eb-aa0d-9ec74c54bf64)


Select **Port** in Rule Type

![image05](https://github.com/user-attachments/assets/983113ba-19f3-4e8f-a998-b0f1eef159b2)


In Protocol and Ports, Select TCP and Enter the ports your Splunk indexer will be listening on

![image06](https://github.com/user-attachments/assets/9d13cf67-14c3-4470-ab47-7840fbe15fef)


Select **Allow the connection**

![image07](https://github.com/user-attachments/assets/da2d6b96-82df-4517-8773-aee1b5da0567)


In Profile, you can specify where this rule will be affected. (I selected all as a default and hit next)

![image08](https://github.com/user-attachments/assets/8030a32f-1077-4721-84c8-5f608e5be5f7)


Give a name for this rule

![image09](https://github.com/user-attachments/assets/d77834f0-0a27-4c8b-a2ce-807590fcc6f9)



Firewall rule for Universal Forwarder has been created.

![image10](https://github.com/user-attachments/assets/2ff155f1-f5f3-4880-bb2d-cad9aa08a0d4)


## Configuring Splunk Universal Forwarder

Go to Splunk directory where configuration files are located. (C:\\Program Files\\SplunkUniversalForwarder\\etc\\system\\local)

![image11](https://github.com/user-attachments/assets/41f0bff5-2b28-4a58-985c-c060862cb63c)


### Verify Connection to Splunk Server

Ensure that the Universal Forwarder is configured to send data to the correct Splunk server. You can verify this in the forwarder's `outputs.conf` file.

![image12](https://github.com/user-attachments/assets/6a7ccf7d-1fae-4a60-9aa9-5dc39a034c3f)

Ensure that the data inputs on the forwarder are correctly configured. (You will have to manually create `inputs.conf` file, make sure you create the file with extension `.conf` under this directory)

Before we write configs in `inputs.conf` file, we have to set allow permission otherwise we won't be able to save the configuration file.

Right click `inputs.conf`file and click **Properties**

![image13](https://github.com/user-attachments/assets/373641f9-9d29-4376-a2f2-f7b1a4937df7)


Go to **Security** tab, and click **Edit**

![image14](https://github.com/user-attachments/assets/a922211a-18c0-4857-a4cb-c6a58acc8119)


Set permissions as shown in figure.

![image15](https://github.com/user-attachments/assets/9eb12d02-c73c-44cc-9e51-74aa25ebc7a4)

Now we write some configs to forward Windows Event Logs to Splunk server.

```
[WinEventLog://Application] 
disabled = false 
index = windows
sourcetype = WinEventLog:Application 

[WinEventLog://System] 
disabled = false
index = windows 
sourcetype = WinEventLog:System

[WinEventLog://Security] 
disabled = false 
index = windows 
sourcetype = WinEventLog:Security
```
![image16](https://github.com/user-attachments/assets/696cb4fb-e0d2-4da5-a546-341a6da06ece)

Configure deployment server in `deploymentclient.conf` file

```
[deployment-client]
clientName = Windows10_VM 
phoneHomeIntervalInSecs = 60

[target-broker:deploymentServer]
targetUri = 192.168.17.100:8089
```
![image17](https://github.com/user-attachments/assets/3427e085-2ea7-4df3-9dd5-8ac12656a670)


After updating the `deploymentclient.conf` file, you need to restart the Splunk Universal Forwarder service for the changes to take effect.

#### Restart and Verify Splunk Universal Forwarder Service

```
Restart-Service -Name "SplunkForwarder"

Get-Service -Name "SplunkForwarder"
```
![image18](https://github.com/user-attachments/assets/5a80366d-5849-4f7e-a469-e1309d5c63a8)

In Splunk Indexer, create a new index `"windows"` as we configured in our `inputs.conf` file

Go to **Setting** > **Indexes** > **Save**

![image19](https://github.com/user-attachments/assets/6edf0627-da5b-44e5-ab2c-b8e8eb2f1edd)

Now you can see Windows Event Logs are successfully forwarded to Splunk Indexer.

![image20](https://github.com/user-attachments/assets/e799e388-c778-4d53-9b7a-f928afb1d000)
![image21](https://github.com/user-attachments/assets/2e6d6449-a25a-4ffa-90a0-a6fee7079375)


