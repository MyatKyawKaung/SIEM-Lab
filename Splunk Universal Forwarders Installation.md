### In this demo, I follow the official Splunk documentation as a reference. 
https://docs.splunk.com/Documentation/Forwarder/8.2.6/Forwarder/Installanixuniversalforwarder#Install_the_universal_forwarder_on_Linux <br>
https://docs.splunk.com/Documentation/Forwarder/8.2.6/Forwarder/InstallaWindowsuniversalforwarderfromaninstaller

Splunk Universal Forwarder download link;
Windows 10, 11  && Windows Server 2019, 2022 (64bits)
```
wget -O splunkforwarder-9.3.0-51ccf43db5bd-x64-release.msi "https://download.splunk.com/products/universalforwarder/releases/9.3.0/windows/splunkforwarder-9.3.0-51ccf43db5bd-x64-release.msi"
```

4.x+, 5.x+, 6.x+ kernel Linux distributions (64bits)
```
wget -O splunkforwarder-9.3.0-51ccf43db5bd-linux-2.6-amd64.deb "https://download.splunk.com/products/universalforwarder/releases/9.3.0/linux/splunkforwarder-9.3.0-51ccf43db5bd-linux-2.6-amd64.deb"
```
![image01](https://github.com/user-attachments/assets/fc59ff56-59e8-4074-9f9e-283e2467f21e)


### Install a Linux universal forwarder
```
dpkg -i <splunkforwarder package name.deb> /opt/splunkforwarder
```
### Start the forwarder
```
./splunk start
```
![image02](https://github.com/user-attachments/assets/6794dc6d-e676-4290-a198-9986f4d42917)
### Enable automatic starting of the universal forwarder at boot time
```
cd <splunk installation directory>/bin
./splunk enable boot-start
```
![image08](https://github.com/user-attachments/assets/be1b8dfd-b26f-4501-aa04-8f8ee4cfd35d)

### Stop the forwarder
```
./splunk stop
```

## Deploy Universal Forwarder

Before deploying universal fowarders, we need to make sure the connectivity between forwarder and indexer.

## Configure a receiver using Splunk Web

**Log into Splunk Web as a user with the admin role.**

![image03](https://github.com/user-attachments/assets/a6be2386-998f-4c44-a2ed-6d505f3d0ad2)

In Splunk Web, go to **Settings > Forwarding and receiving**.

![image04](https://github.com/user-attachments/assets/a82ab82e-c4a0-43c0-92a9-cb509f4a43af)


Select "Configure receiving."

![image05](https://github.com/user-attachments/assets/5d518f42-79d2-4f10-8e0f-02f6e79528ae)

Verify if there are existing receiver ports open. You cannot create a duplicate receiver port. The conventional receiver port configured on indexers is port `9997`.

Optionally select "New Receiving Port." Add a port number and save.

![image06](https://github.com/user-attachments/assets/a2bd87f4-7b2e-40b1-b46e-0b6e29c54041)


## Configure a receiver using the command line

 Change the path to $SPLUNK_HOME/bin (In this case, my splun_home directory is /opt/splunk)
 
```
cd /opt/splunk/bin
./splunk enable listen 9997 -auth <admin_username>:<password>
```
![image07](https://github.com/user-attachments/assets/a72f16ef-64cf-434f-9148-a14d99570a42)

Restart Splunk software for the changes to take effect.
