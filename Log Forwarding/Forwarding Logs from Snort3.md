### This demonstration will showcase how to integrate NIDS Logs to enhance security posture using Splunk for Detecting Malicious Activities

**Firstly, you need to specify a directory where you want to forward logs to.** 

(In this case, I want to forward my alert logs that I generated from Snort)

![image01](https://github.com/user-attachments/assets/950d76bd-657f-47a6-b0b0-b1520dac4e24)


**Go to the directory where Splunk universal forwarder binaries are installed. (/opt/splunkforwarder/bin) and run the following command**

```
./splunk add monitor /var/log/snort/snort.alert.fast
```
![2](https://github.com/user-attachments/assets/37cbea7e-632a-46de-b0da-760735baade3)

**We need to configure our Data inputs for UF to where our logs will be forwarded.** This can be done by editing inputs.conf file located under /opt/splunkforwarder/etc/apps/search/local

```
cd /opt/splunkforwarder/etc/apps/search/local/
nano inputs.conf
```
![image03](https://github.com/user-attachments/assets/8a1ba7a6-c4c8-427f-8945-29566311469f)
![image04](https://github.com/user-attachments/assets/297e551d-87c4-413d-a684-8e80e2621ac1)

**Restart Splunk service**

```
cd /opt/splunkforwarder/bin
sudo ./splunk restart
```
![image05](https://github.com/user-attachments/assets/2523b5ac-b1be-42e8-a745-d2a4772438e7)

**Log In to Splunk Web UI and check if Snort Alert logs are forwarded to Indexer**

![image06](https://github.com/user-attachments/assets/49b87be5-17b7-4b49-9fa8-609d1552b5ce)


Our logs are finally here. In order to investigate efficiently and effectively in Splunk, we need to parse the ingested logs into fields. This way, Analysts can investigate logs effectively using SPL.

![image07](https://github.com/user-attachments/assets/2d85f660-a57d-4e8c-8b6e-c9102fb04a26)

We cam extract some important fields from NIDS using Regular Expression or Delimiter. (I will use Regex in this case)

![image08](https://github.com/user-attachments/assets/9e8e38a0-b30c-46d9-9a75-7872bd3d0437)

You can select the fields and name the field as you want. I created field names Src_IP, Src_Port, Dst_IP and Dst_IP. You can see the Regular expression written by Splunk for your extracted fiels as well.  

![image09](https://github.com/user-attachments/assets/12b594d9-2ee0-43a4-82b8-f88570d5f4b9)

Sample Preview of the logs (You can see green check mark on the left which means these following logs will be extracted correctly as intended.)

![image10](https://github.com/user-attachments/assets/1fa50b7e-cef5-4f80-a1b7-1be9c5791a8e)

You can validate the configuration and click **Finish** to save.

![image11](https://github.com/user-attachments/assets/40d2828e-aa11-4d62-ace2-16fadac73a15)

**Now we can see our fields are extracted in raw logs**

![image12](https://github.com/user-attachments/assets/4f7c9aec-1776-45ba-8a10-d633d513fe65)

By parsing the logs, we can finally utilize SPL queries to investigate malicious activities in our environment.

![image13](https://github.com/user-attachments/assets/e2e17871-301b-4285-a5f6-b6b9d717baeb)
