## Introduction

Atomic Red Team is a open-source framework developed by Red Canary for performing security testing and threat emulation. It consists of tools and techniques that can be used to simulate various types of attacks and security threats, such as malware, phishing attacks, credential dumping attacks, Exploitation, etc.. 

In this lab, we will learn how to utilize Atomic Red Team from the perspective of Blue Teamer to see how the threat actors perform their TTPs. </br>
_**Note: If you want to know more, check out their official websites and youtube for more details.**_

https://atomicredteam.io/ </br>
https://www.youtube.com/watch?v=-HEx-qfd54M&list=PL92eUXSF717W9TCfZzLca6DmlFXFIu8p6&index=1
https://github.com/redcanaryco/invoke-atomicredteam/wiki

![image01](https://github.com/user-attachments/assets/8c6c07ef-7450-4a82-a6a4-2f19f0dfe600)

![image02](https://github.com/user-attachments/assets/8a0c5d92-1962-4b9c-9032-ac35182b9e3d)

## Installing Atomic Red Team

You can install Atomic RedTeam according to their installation guide as below

https://github.com/redcanaryco/invoke-atomicredteam/wiki/Installing-Invoke-AtomicRedTeam

### **Install Execution Framework and Atomics Folder**

```bash
IEX (IWR 'https://raw.githubusercontent.com/redcanaryco/invoke-atomicredteam/master/install-atomicredteam.ps1' -UseBasicParsing);
Install-AtomicRedTeam -getAtomics
```

**If the execution framework or the atomics folder are already found on disk you must use the `-Force` parameter during install as follows to erase and replace these folders.**

```bash
IEX (IWR 'https://raw.githubusercontent.com/redcanaryco/invoke-atomicredteam/master/install-atomicredteam.ps1' -UseBasicParsing);
Install-AtomicRedTeam -getAtomics -Force
```
![image03](https://github.com/user-attachments/assets/d60af3f8-3a22-472a-907f-c5eb0eac8fc8)

Once installation is completed, you will see `AtomicRedTeam` folder is created under C: drive.

![image04](https://github.com/user-attachments/assets/fe6c20a0-b5ff-410c-8a85-b23a0afe664a)


![image05](https://github.com/user-attachments/assets/0b3718df-d091-4847-aee9-362f885a5e36)

You can see Atomic test modules associated with MITRE ATT&CK framework under atomics folder.


![image06](https://github.com/user-attachments/assets/bea05d0e-0da8-4f8b-b8ea-efbb9813ea64)

## **Import the Module**

In order make the `Invoke-AtomicTest` function available for use in your current PowerShell session you must import the module

```bash
Import-Module "C:\AtomicRedTeam\invoke-atomicredteam\Invoke-AtomicRedTeam.psd1" -Force
```

After the module has imported, you can start using AtomicRedTeam by listing Technique numbers and test names available for execution.

```bash
Invoke-AtomicTest T1003 -ShowDetailsBrief
```

![image07](https://github.com/user-attachments/assets/427ecf1f-e9ab-4707-8b4f-f5f11080d865)

You can use the `-ShowDetails` switch to show all the test details, including attack commands, input parameters, and prerequisites for a given MITRE ATT&CK technique number.

```bash
Invoke-AtomicTest T1003 -ShowDetails
```
![image08](https://github.com/user-attachments/assets/1ddaca0a-2264-4d07-8e18-66199fc1afa7)

## **Verifying Requirements**

To ensure your system is ready to execute a specific Atomic Red Team test, use the `-CheckPrereqs` switch:

```bash
Invoke-AtomicTest T1003 -TestNumbers 2 -CheckPrereqs
```
![image09](https://github.com/user-attachments/assets/b649aa07-6f5f-4ad1-9f16-1b0942077118)

If your system lacks certain prerequisites, you can attempt to automatically fulfill them using the `-GetPrereqs` switch:

```bash
Invoke-AtomicTest T1003 -TestNumbers 2 -GetPrereqs
```
![image10](https://github.com/user-attachments/assets/a53b4e66-51b5-4975-bc5b-fe8ece19b93f)

## **Cleanup After Executing Atomic Tests**

It is VERY IMPORTANT to clean up the mess of emulating different techniques. Another feature in the Invoke-AtomicRedTeam module is the capacity to perform the cleanup commands to remove each of the tested footsteps.

**Run the Cleanup Commands for the Specified Test**

```bash
Invoke-AtomicTest T1003 -TestNumbers 2 -Cleanup 
```

**Run the Cleanup Commands for all atomic tests under a given Technique number**
![image11](https://github.com/user-attachments/assets/3e5b1c65-5c0e-484c-b825-4e43a10ced33)
