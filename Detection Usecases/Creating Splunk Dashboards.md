**In this demo, I will create custom dashboards in Splunk to monitor and detect suspicious activities in our environment.**

### Dashboard 1: User Login Activity Monitoring Dashboard

**The primary objective of this dashboard is to visualize the success and failure rates of user login activities. We'll focus on key metrics like total login attempts, successful logins and failed logins by filtering with `EventID=4624` (Account Logon) and `EventID=4625` (Account Logoff)**

Firstly, we will need to find out successful login accounts by using SPL query. The following query will show all unique successful authenticated accounts within last 7days.

```markdown
index=windows EventCode=4624 | stats count by Account_Name | sort -count
```

![image01](https://github.com/user-attachments/assets/8ffdf3a3-4b39-4f35-88e5-dd0c3352ab87)

There are some machine accounts and service accounts which we will need to whitelist for less noise. This can be done by removing machine and service accounts using following query

```markdown
index=windows EventCode=4624
| rex field=Account_Name "(?<User_Account>^[^$]+)$"
| search NOT User_Account IN ("SYSTEM", "LOCAL SERVICE", "NETWORK SERVICE", "-")
| search NOT User_Account="DWM-*"
| search NOT User_Account="UMFD-*"
| stats count by User_Account
| sort -count
| head 10
```

![image02](https://github.com/user-attachments/assets/2514dc34-4f22-4dd5-b45a-6632ee0c1431)

After whitelisting, results become more accurate with less noise. We can now save this query as a dashboard. 

Go to `Save As` tab, on the right corner and save the query as `New Dashboard`

![image03](https://github.com/user-attachments/assets/5d9bda1f-176c-4f71-be05-aac8e5f266c4)

Give title for your dashboard and configure settings as your preferences.

![image04](https://github.com/user-attachments/assets/848ba398-e52a-406e-8805-532e3bfa61a0)

On your Splunk App, you will see a new dashboard we’ve just created.

![image05](https://github.com/user-attachments/assets/ae6bb38d-141e-45ef-a375-5fd571b96244)

You can configure dashboards in a visually more presentable format such as piecharts and columns on the right corner of the panel.

![image06](https://github.com/user-attachments/assets/78f80f97-0ca6-4b7f-a26f-372f400aaba8)
![image07](https://github.com/user-attachments/assets/dd864a82-d4c4-498c-ab40-a59f198094e9)

We can create dashboards for authentication failure activities by modifying our previous query with `EventId=4625` 

```markdown
index=windows EventCode=4625
| rex field=Account_Name "(?<User_Account>^[^$]+)$"
| search NOT User_Account IN ("SYSTEM", "LOCAL SERVICE", "NETWORK SERVICE", "-")
| search NOT User_Account="DWM-*"
| search NOT User_Account="UMFD-*"
| stats count by User_Account
| sort -count
| head 10
```
![image08](https://github.com/user-attachments/assets/d2de279b-0aca-4464-ae69-546fac278b38)

### Dashboard 2: Web Traffic Anomaly Dashboard

**The primary objective of this dashboard is to visualize excessive web traffic and identify suspicious user agents. We'll focus on metrics like total web traffic, unique IP addresses, top user agents, and potential anomalies.**

Firstly, we have to generate some web traffics since this is a controlled lab environment and we will not be getting request from public. We will utilize Nmap, Nikto and OWASP Zap to scan our simple HTTP server.

On our Windows_Server VM, host a simple web server using

```markdown
python -m http.server 8000 
```
![image09](https://github.com/user-attachments/assets/d0ad7ba6-e434-413d-955e-6832bea06354)

On our attack machine, port scan using scanning tools

```markdown
nmap -sV -p 8000 192.168.17.200
```
```markdown
nikto -h 192.168.17.200:8000
```
![image10](https://github.com/user-attachments/assets/b7684e41-ff39-440b-a1cd-5ebdbab17056)

I will also use ZAP for automated scan as well.

![image11](https://github.com/user-attachments/assets/ec32463d-f2e3-459f-b535-65f53b4af871)
![image12](https://github.com/user-attachments/assets/e671f80e-3b7f-404d-8395-045846ef6e02)

After generating some network traffics, we can filter our events using sysmon event_id=3 (Network Connection Detected) in Splunk.

![image13](https://github.com/user-attachments/assets/42bfdd99-6a8d-47dc-9410-a1f388d90db1)

```markdown
index=* host="WINDOWS-SERVER" event_id=3
| stats count by src_ip dest_ip dest_port
```
![image14](https://github.com/user-attachments/assets/5079a007-0ec4-4298-abb4-85c8cd4f166b)

We can see internal IPs and loopback IPs are in the events, so we will filter them out by using following query.

```markdown
index=* host="WINDOWS-SERVER" event_id=3
| search NOT src_ip IN ("0:0:0:0:0:0:0:1", "224.0.0.251", "ff02:0:0:0:0:0:0:fb", "127.0.0.1", "fe80:0:0:0:1a41:990a:5957:f872")
| stats count by src_ip dest_ip dest_port
| sort - count
| head 10
```
![image15](https://github.com/user-attachments/assets/10ecddc9-200e-4787-92f6-c515c7e3c409)

After whitelisting internal IPs, the results can be used in creating a network traffic dashboard. Creating a dashboard for web traffic is similar as in dashboard 1.

![image16](https://github.com/user-attachments/assets/081b6dd5-a54b-4370-9ebe-9b3854de2d7c)
