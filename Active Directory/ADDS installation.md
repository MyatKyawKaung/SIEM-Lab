**Active Directory Domain Service (ADDS)** is used in Windows Server environments to manage domain resources like users, computers, groups, and policies across a network. ADDS enables centralized, secure management of network services, authentication, authorization, and policy enforcement in enterprise environments.

### In this demo, we will be installing ADDS Role on Windows Server and promote it into Domain Controller.

Go to Server Manager, On top right corner you will see `Manage` > `Add Roles and Features` 

![image01](https://github.com/user-attachments/assets/3f6d3bd9-ffd5-4095-a87c-4a9a75bdc59f)

Select `Next`

![image02](https://github.com/user-attachments/assets/a28e03c3-58a1-42cd-ae58-0bc7bd668b43)

Select `Role-based or feature-based installation` > `Next`

![image03](https://github.com/user-attachments/assets/5d35d0a9-2c1d-483b-a829-a414f2bfb184)

If you have multiple servers, they will be listed here. (Since I only have one, choose it and go next)

![image04](https://github.com/user-attachments/assets/29025519-f20f-4a4c-9f71-ba95722a71f7)

Mark `Active Directory Domain Services` and press `Add Features` 

![image05](https://github.com/user-attachments/assets/d3543cee-ab1d-4f2c-8a97-a3e856fdf936)
![image06](https://github.com/user-attachments/assets/7f2da960-9738-4aed-8e71-194cdb9ec2b0)
![image07](https://github.com/user-attachments/assets/f83cc6c3-1ce7-412e-b06d-22c8f0fded77)

Confirm the installation, press `Install` and wait for the installation to finish

![image08](https://github.com/user-attachments/assets/b4fae0dc-f347-4091-893e-58a00de5fa6d)

Once the ADDS installation is finished, you will need to promote it into `Domain Controller`

![image09](https://github.com/user-attachments/assets/393a16e0-3d00-4942-9c49-efef3a531651)

Go back to Server Manager Dashboard, under notification flag > Click `Promote this server to a domain controller` 

![image10](https://github.com/user-attachments/assets/89245761-2bb2-48de-9338-403cd6a435d0)

Create a new forest and give a top level domain name such as `something.com, .net`, etc. (I use TheRadiant.local in this case)

![image11](https://github.com/user-attachments/assets/89a10c2c-2554-4340-85fe-00dba30e1322)

Give a password and hit `Next`. I will leave everything as a default.

![image12](https://github.com/user-attachments/assets/229b4c77-6cfd-44bb-9ed3-ab375bf7d857)
![image13](https://github.com/user-attachments/assets/b0a42e82-d5d1-49ad-b693-e816099674eb)
![image14](https://github.com/user-attachments/assets/8790081b-e50a-4b44-a837-937dfc7eb8af)

FYI, this is the path where `ntds.dit` file lives. It is the core database for the entire Active Directory structure and contains all the Active Directory objects. (If you notice any suspicious activity related to this file, chances are your entire domain is unfortunately compromised.)

![image15](https://github.com/user-attachments/assets/e980b514-5269-4c76-a218-ee280f708d44)

Press `Next` for both Review Options and Prerequisites Check as well.

![image16](https://github.com/user-attachments/assets/d798c301-97b7-4edd-bfec-fc58781f65a7)

![image17](https://github.com/user-attachments/assets/c16c156e-fa77-4ee5-96f5-32118b427dff)


Once the installation is completed, your server will automatically restart.

![image18](https://github.com/user-attachments/assets/2c2d7c42-c2fc-4c34-89cb-c0f54d789f42)

After the restart, you will see the domain name ***TheRadiant\Administrator*** which indicates ADDS i*s* successfully installed and promoted to a domain controller. You can now start adding users and groups to your domain.

![image19](https://github.com/user-attachments/assets/4cb9bc00-c281-4e74-a4ad-5fe3497c1936)
