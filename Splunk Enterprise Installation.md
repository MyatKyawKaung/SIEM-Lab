### In this demo, I follow the official Splunk documentation as a reference. 
https://docs.splunk.com/Documentation/Splunk/9.3.0/Installation/InstallonLinux

Splunk Enterprise instance download link;<br>
```
 wget -O splunk-9.3.0-51ccf43db5bd-linux-2.6-amd64.deb "https://download.splunk.com/products/splunk/releases/9.3.0/linux/splunk-9.3.0-51ccf43db5bd-linux-2.6-amd64.deb"

```

Once downloaded, you can see the .deb file in your downloaded directory, (In this case, I downloaded to /home/mkksvr diretory)

![image01](https://github.com/user-attachments/assets/09235dd3-2b45-4aca-b9f4-3d2369a44ca4)

### 1. Install Splunk Enterprise debian package using **dpkg** installer
```
dpkg -i splunk_package_name.deb

```

Confirm Splunk installation status
```
dpkg --status splunk

```
![image02](https://github.com/user-attachments/assets/ac2c30b9-c398-45fc-a605-9185ccb50c6c)

### 2. Start Splunk Enterprise
```
cd <Splunk Enterprise installation directory>/bin
./splunk start
```

Create the Splunk Enterprise admin username & password, after starting Splunk instance.

![image03](https://github.com/user-attachments/assets/72ef322b-df92-433a-86e8-f7c83b37e84c)

After giving your desire username and password for Splunk Enterprise Admin, it will open Splunk web portal at port 8000 
(You will need to identify what your web interface IP by using 'Ifconfig or ip a' commnd)

![image04](https://github.com/user-attachments/assets/00c21c5a-a7f5-4c67-ac6b-3d81bd6cd695)


### 3. Launch Splunk Web portal and Login using the credentials
```
http://<host name or ip address>:8000

```
![image05](https://github.com/user-attachments/assets/37015e4a-465f-403e-8dc9-66e4c447b6cf)
![image06](https://github.com/user-attachments/assets/d9891f7c-fdbc-4611-8267-962fb388fae7)

**If you want to stop Splunk Enterprise**
```
./splunk stop

```
