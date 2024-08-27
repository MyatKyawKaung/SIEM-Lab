## Connect Forwarder to a deployment server 
(In this case, it would be a Splunk instance which I am using as an Indexer)

```
cd /opt/splunkforwarder/bin
./splunk set deploy-poll <your_indexer_ip_address>:8089
```
![image01](https://github.com/user-attachments/assets/77ceecfd-3632-42c9-b9ad-d92442725b2f)

## Confirm deployment client is configured or not by going to this directory
```
cd /opt/splunkforwarder/etc/system/local
nano deploymentclient.conf
```
![image02](https://github.com/user-attachments/assets/f128e9b3-fe2d-4832-a2ca-32fbf6b9c25e)
![image03](https://github.com/user-attachments/assets/6211e4ea-173f-4ccc-b611-a25301c2be8e)


## Set up Splunk Universal Forwarder to send logs to Another Location
```
cd /opt/splunkforwarder/bin/
./splunk add forward-server <your_destination_IP>:9997
```

![4](https://github.com/user-attachments/assets/1772040e-5618-400a-b906-191034e8c8fb)

## Check forwarder configs
```
./splunk list forward-server
```
![image05](https://github.com/user-attachments/assets/e3b2c546-2ca2-459b-a10b-0bb96922ae07)
![image06](https://github.com/user-attachments/assets/5f197461-4f17-4cf7-9b4c-256ea81ea260)

## Example of output.conf single host stanza

![image07](https://github.com/user-attachments/assets/35d4f906-b2fb-4d30-a3b9-7d64642026ba)


## Check forwarder is pushed into deployment server (indexer)

![image08](https://github.com/user-attachments/assets/ee264fe2-c9cc-40c2-a10f-5e0192f4b14a)

## Here you can see my universal forwarder is forwarding logs to indexer

![image09](https://github.com/user-attachments/assets/69388036-55ef-4ea1-a6e6-470429f047e2)


## Confirm ingested logs by running query filtering with my VM HostName
![image10](https://github.com/user-attachments/assets/f5d59d28-131a-4b79-b59c-297882c10370)

