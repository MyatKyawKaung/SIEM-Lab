<h2 align="left"> Download and Configure Splunk Add-on Apps </h2>

Download and install Snort 3 JSON Alerts
![image01](https://github.com/user-attachments/assets/333331e1-5b60-4fe3-a64c-1f6fe4ad4449)
![image02](https://github.com/user-attachments/assets/dcccf48f-2209-4739-ba8c-73c6a9d152d6)

Download and install Cybercheft App (to covert the b64_data fields into readable text)
![image03](https://github.com/user-attachments/assets/f0795402-ba28-4c32-aaed-71ac8a927ef7)

### Configure the Snort 3 JSON Alerts add-on
To tell Splunk where the log files are stored that Snort 3 generated so Splunk can ingest them.
```
sudo mkdir /opt/splunk/etc/apps/TA_Snort3_json/local 
sudo touch /opt/splunk/etc/apps/TA_Snort3_json/local/inputs.conf 
sudo nano /opt/splunk/etc/apps/TA_Snort3_json/local/inputs.conf
```

Enter the following configs into this inputs.conf file
```
[monitor:///var/log/snort/*alert_json.txt*] 
sourcetype = snort3:alert:json
```
![image04](https://github.com/user-attachments/assets/e1802e53-1399-4d73-b390-dbbcb7676df0)

**Restart the Splunk** so when it starts, it will scan the /var/log/snort directory for json files, assign them sourcetype of "snort3:alert:json", and ingest them so we can search them.
```
cd /opt/splunk/bin/
./splunk restart
```

