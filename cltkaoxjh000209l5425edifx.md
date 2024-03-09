---
title: "Blue Team Level 1 Notes"
seoTitle: "Blue Team Level 1 Notes"
datePublished: Sat Mar 09 2024 16:23:36 GMT+0000 (Coordinated Universal Time)
cuid: cltkaoxjh000209l5425edifx
slug: blue-team-level-1-notes
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1710001333141/22e6e8a2-7121-4eb2-b20b-9eeacff27b1a.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1710001372786/2725cef5-fa5e-4a12-8c23-d5a3830a12fd.jpeg
tags: hacker, cybersecurity-1, blueteam, ferdibirgul

---

## **Common Ports**

| Port | Service | Description |  |
| --- | --- | --- | --- |
| 20,21 | FTP | File Transfer Protocol used to transfer files b/w systems. |  |
| 22 | SSH | Secure Shell Protocol allows users to securely connect to a remote host. |  |
| 23 | Telnet | Used before SSH, allows users to connect to a remote host, doesn’t offer encryption. |  |
| 25 | SMTP | Simple Mail Transfer Protocol used to send emails between servers within the network, or over the internet. |  |
| 53 | DNS | Domain Name System converts human-readable domain names to machine-readable IP address. |  |
| 67,68 | DHCP | Dynamic Host Configuration Protocol assign IP address-related information to any hosts on the network automatically. |  |
| 80 | HTTP | Hypertext Transfer Protocol allows browsers (Chrome, Firefox, etc) to connect to web servers and request contents. |  |
| 443 | HTTPS | Hypertext Transfer Protocol Secure is a secure version of HTTP Protocol which allows browsers to securely connect to web servers and request contents. |  |
| 514 | Syslog | Syslog server listens for incoming Syslog notifications, transported by UDP packets. | \*\*\* |

## **Phishing Analysis**

---

### **Gathering Artifacts (IOCs)**

**Email Artifacts** -

* Sender Address
    
* Reply-To Address
    
* Sending Server IP
    
* Reverse DNS
    
* Recipient Address
    
* Subject Line
    
* Date & Time
    

**Web-based Artifacts** -

* Full-URLs (sanitized)
    
* Domain Names
    

**File-based Artifacts** -

* Filename & Extension
    
* MD5/SHA1/SHA256 Hash Values
    

### **Artifacts Analysis**

1. **Visualization Tools** - [URL2PNG](https://www.url2png.com/), [URLScan](https://urlscan.io/)
    
2. **URL Reputation Tools** - [VirusTotal](https://www.virustotal.com/gui/), [URLScan](https://urlscan.io/), [URLhaus](https://urlhaus.abuse.ch/), [WannaBrowser](https://www.wannabrowser.net/)
    
3. **File Reputation Tools** - [VirusTotal](https://www.virustotal.com/gui/), [Talos File Reputation](https://www.talosintelligence.com/talos_file_reputation)
    
4. **Malware Sandboxing** - [Hybrid Analysis](https://www.hybrid-analysis.com/)
    

#### **Defanging URL & IP Address**

1. [Defang URL, Defang IP Addresses - CyberChef (gchq.github.io)](https://gchq.github.io/CyberChef/#recipe=Defang_URL(true,true,true,'Valid%20domains%20and%20full%20URLs')Defang_IP_Addresses())
    

## **Digital Forensics**

---

**Data representation can be done in the following ways,**

* Base64
    
* Hexadecimal
    
* Octal
    
* ASCII
    
* Binary
    

### **Metadata**

<table><tbody><tr><td colspan="1" rowspan="1"><p></p></td><td colspan="1" rowspan="1"><p><code># Provided with information such as the read/write permissions, the file name and size, and the times for when the file was last accessed and modified. ls -lisap &lt;file&gt; stat &lt;file&gt; # Received metadata from files # sudo apt-get install exiftool exiftool &lt;file&gt;</code></p></td></tr></tbody></table>

### **File Carving**

<table><tbody><tr><td colspan="1" rowspan="1"><p></p></td><td colspan="1" rowspan="1"><p></p></td><td colspan="1" rowspan="1"><p><code># To choose which file type you want to retrieve you can edit in /etc/scalpel/scalpel.conf # To start retrieving a file using command below scalpel -b -o &lt;output-dir&gt; &lt;disk-image-file&gt;</code></p></td></tr></tbody></table>

### **Hashing**

1. Windows
    
    <table><tbody><tr><td colspan="1" rowspan="1"><p>1</p></td><td colspan="1" rowspan="1"><p><code>Get-FileHash -Algorithm [algorithm-to-use] [file]</code></p></td></tr></tbody></table>
    
2. **Linux**
    
    <table><tbody><tr><td colspan="1" rowspan="1"><p></p></td><td colspan="1" rowspan="1"><p><code>md5sum &lt;file&gt; sha1sum &lt;file&gt; sha256sum &lt;file&gt;</code></p></td></tr></tbody></table>
    

### **Data Acquisition**

* **FTK Imager** - import `.img` file in FTK Imager. [Download](https://accessdata.com/product-download/ftk-imager-version-4-5)
    
* **KAPE** - uses for fast acquisition of data. [Download](https://www.kroll.com/en/services/cyber-risk/incident-response-litigation-support/kroll-artifact-parser-extractor-kape)
    

#### **Windows Investigation**

**LNK Files** -

* These files can be found at
    
    <table><tbody><tr><td colspan="1" rowspan="1"><p>1</p></td><td colspan="1" rowspan="1"><p><code>%userprofile%\Appdata\Roaming\Microsoft\Windows\Recent</code></p></td></tr></tbody></table>
    
* [Windows File Analyzer](https://www.mitec.cz/wfa.html) can be used to view these files in form of human-readable format.
    

**Prefetch Files** -

* These files can be found at
    
    <table><tbody><tr><td colspan="1" rowspan="1"><p>1</p></td><td colspan="1" rowspan="1"><p><code>C:\Windows\Prefetch</code></p></td></tr></tbody></table>
    
* [Prefetch Explorer Command Line](https://ericzimmerman.github.io/#!index.md) can be used to view these files in form of human-readable format a.k.a. `PEbatch.exe`.
    
    <table><tbody><tr><td colspan="1" rowspan="1"><p></p></td><td colspan="1" rowspan="1"><p><code># Using PEbatch requires administrator privilege PEbatch.exe -f [path-to-file].pf PEbatch.exe -k "string-to-match" -d [path-to-prefetch-folder]</code></p></td></tr></tbody></table>
    

**Jump List** -

* These files can be found at
    
    <table><tbody><tr><td colspan="1" rowspan="1"><p></p></td><td colspan="1" rowspan="1"><p><code>C:\Users\% USERNAME%\AppData\Roaming\Microsoft\Windows\Recent\AutomaticDestinations C:\Users\%USERNAME%\AppData\Roaming\Microsoft\Windows\Recent\CustomDestinations</code></p></td></tr></tbody></table>
    
* [JumpList Explorer](https://ericzimmerman.github.io/#!index.md) could be used to analyze these files.
    

**Browsers Artifacts** -

* **KAPE** — [Download](https://www.kroll.com/en/insights/publications/cyber/kroll-artifact-parser-extractor-kape)
    
* **Browser History Viewer** — [Download](https://www.foxtonforensics.com/browser-history-viewer/)
    
* **Browser History Capturer** — [Download](https://www.foxtonforensics.com/browser-history-capturer/)
    

**Event Logs** -

* **Event ID** 4624 - Successful Logon
    
* **Event ID** 4625 - Failed Logon
    
* **Event ID** 4672 - Special Logon *(with administrative privileges logs in)*
    
* **Event ID** 4634 - Logoff from the current session
    
* **Event ID** 4720 - User account was created
    
* **Event ID** 4726 - User account was deleted
    
* **Event ID** 4732 - A member was added to a security-enabled local group
    

These event logs could be found at

<table><tbody><tr><td colspan="1" rowspan="1"><p></p></td><td colspan="1" rowspan="1"><p><code>C:\Windows\System32\winevt\Logs</code></p></td></tr></tbody></table>

#### **Linux Investigation**

* `/etc/passwd` — contains a list of user accounts on the system, and their permissions.
    
* `/etc/shadow` — contains encrypted passwords of existing users on the system.
    
* `unshadow /etc/passwd /etc/shadow > <new-file>` to combine the passwd and shadow together.
    
* `/var/lib/dpkg/status` — includes list of all installed software packages on debian-based systems.
    
* `.bash_history` — contains a list of commands that have been run by the specific user.
    
* **Hidden Files and Directories** — usually prefix with `.`
    
* **Clear Files** — the file that is accessible by standard means. *i.e. browser, terminal*
    
* **Steganography** — a practice of concealing messages or files within other non-secret text or data.
    

**Volatility — Memory Analysis** -

<table><tbody><tr><td colspan="1" rowspan="1"><p><code>1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24</code></p></td><td colspan="1" rowspan="1"><p><code># Determine the suggested profile for analysis volatility -f memdump.mem imageinfo # Print a list of processes to the terminal volatility -f memdump.mem --profile=&lt;PROFILE&gt; pslist # Print a process tree to the terminal volatility -f memdump.mem --profile=&lt;PROFILE&gt; pstree # View command line of the specific process with PID XXXX volatility -f /path/to/file.mem --profile=PROFILE dlllist -p XXXX # Print all available processes, including hidden ones often used by malware volatility -f memdump.mem --profile=&lt;PROFILE&gt; psscan # Dumping the process with a specific PID XXXX volatility -f /path/to/file.mem --profile=PROFILE procdump -p XXXX -D /home/ubuntu/Desktop # Print expected and hidden processes volatility -f memdump.mem --profile=&lt;PROFILE&gt; psxview # View any active or closed network connections volatility -f memdump.mem --profile=&lt;PROFILE&gt; netscan # Create a timeline of events from the memory image volatility -f memdump.mem --profile=&lt;PROFILE&gt; timeliner # Pull internet browsing history volatility -f memdump.mem --profile=&lt;PROFILE&gt; iehistory # Identify any files on the system from the memory image volatility -f memdump.mem --profile=&lt;PROFILE&gt; filescan # Retrieve files from the memory image volatility -f memdump.mem --profile=&lt;PROFILE&gt; dumpfiles -n --dump-dir=&lt;path-to-dump&gt;</code></p></td></tr></tbody></table>

## **Security Information and Event Management**

---

### **Splunk**

> * Make sure you turn searching query time to **All Times** to see all the events
>     
> * To quickly identify sourcetype (don’t look through every single log) make sure to turn **Event Sampling** to `1:100 or 1:1000 or etc.`
>     

All queries must start by referencing the dataset

<table><tbody><tr><td colspan="1" rowspan="1"><p></p></td><td colspan="1" rowspan="1"><p><code>index=&lt;dataset&gt;</code></p></td></tr></tbody></table>

To search for a source ip address

<table><tbody><tr><td colspan="1" rowspan="1"><p></p></td><td colspan="1" rowspan="1"><p><code>index=&lt;dataset&gt; src="x.x.x.x"</code></p></td></tr></tbody></table>

To search for a destination ip address that made a connection with, i.e. locahost (127.0.0.1)

<table><tbody><tr><td colspan="1" rowspan="1"><p></p></td><td colspan="1" rowspan="1"><p><code>index=&lt;dataset&gt; src="127.0.0.1" dst="x.x.x.x"</code></p></td></tr></tbody></table>

## **Incident Response**

---

### **Network Traffic Analysis**

Using **Wireshark** to analyze network traffic capture files including, `.pcap`, `.cap`, `.pcapng`, etc.

### **Command Prompt to assist with incident response**

* List network configuration information in local system
    
    <table><tbody><tr><td colspan="1" rowspan="1"><p>1</p></td><td colspan="1" rowspan="1"><p>ipconfig /all</p></td></tr></tbody></table>
    
* Print a list of running processes and programs
    
    <table><tbody><tr><td colspan="1" rowspan="1"><p>1</p></td><td colspan="1" rowspan="1"><p>tasklist</p></td></tr></tbody></table>
    
* Display running processes and associated binary file that was executed to create the process
    
    <table><tbody><tr><td colspan="1" rowspan="1"><p>1</p></td><td colspan="1" rowspan="1"><p>wmic process get description, executablepath</p></td></tr></tbody></table>
    
* Print a list of all local system users
    
    <table><tbody><tr><td colspan="1" rowspan="1"><p>1</p></td><td colspan="1" rowspan="1"><p>net user</p></td></tr></tbody></table>
    
* Print a list of all users that are resided in an administrators user group
    
    <table><tbody><tr><td colspan="1" rowspan="1"><p>1</p></td><td colspan="1" rowspan="1"><p>net localgroup administrators</p></td></tr></tbody></table>
    
* Print all users reside in a RDP group
    
    <table><tbody><tr><td colspan="1" rowspan="1"><p>1</p></td><td colspan="1" rowspan="1"><p>net localgroup "Remote Desktop Users"</p></td></tr></tbody></table>
    
* List all services and detailed information about each one
    
    <table><tbody><tr><td colspan="1" rowspan="1"><p>1</p></td><td colspan="1" rowspan="1"><p>sc query | more</p></td></tr></tbody></table>
    
* List all open ports on a system
    
    <table><tbody><tr><td colspan="1" rowspan="1"><p>1</p></td><td colspan="1" rowspan="1"><p>netstat -ab</p></td></tr></tbody></table>
    

### **Powershell to help extracted valuable information**

* To get network-related information from the system
    
    <table><tbody><tr><td colspan="1" rowspan="1"><p>1 2</p></td><td colspan="1" rowspan="1"><p>Get-NetIPConfiguration Get-NetIPAddress</p></td></tr></tbody></table>
    
* List all local users on the system
    
    <table><tbody><tr><td colspan="1" rowspan="1"><p>1 2 3</p></td><td colspan="1" rowspan="1"><p>Get-LocalUser # To get more information about a specific user Get-LocalUser -Name BTLO | select *</p></td></tr></tbody></table>
    
* To identify running services on the system and show the results in a nice windows
    
    <table><tbody><tr><td colspan="1" rowspan="1"><p>1</p></td><td colspan="1" rowspan="1"><p>Get-Service | where Status -eq "Running" | Out-GridView</p></td></tr></tbody></table>
    
* List the running processes and group it by their priority value
    
    <table><tbody><tr><td colspan="1" rowspan="1"><p>1</p></td><td colspan="1" rowspan="1"><p>Get-Process | Format-Table -View priority</p></td></tr></tbody></table>
    
* Get specific information from a service
    
    <table><tbody><tr><td colspan="1" rowspan="1"><p>1 2 3 4</p></td><td colspan="1" rowspan="1"><p># specific information by including their name Get-Process -Name 'namehere' # specific information by including their id and piping for collected all properties Get-Process -Id 'idhere' | Select *</p></td></tr></tbody></table>
    
* List tasks that are set to run after certain conditions are met
    
    <table><tbody><tr><td colspan="1" rowspan="1"><p>1</p></td><td colspan="1" rowspan="1"><p>Get-ScheduledTask</p></td></tr></tbody></table>
    
* Dig more deeper by specifying the task we’re interested in and piping for all properties
    
    <table><tbody><tr><td colspan="1" rowspan="1"><p>1</p></td><td colspan="1" rowspan="1"><p>Get-ScheduledTask -TaskName 'PutANameHere' | Select *</p></td></tr></tbody></table>
    
* Change the Execution Policy applied to specific user
    
    <table><tbody><tr><td colspan="1" rowspan="1"><p>1</p></td><td colspan="1" rowspan="1"><p>Set-ExecutionPolicy Bypass -Scope CurrentUser</p></td></tr></tbody></table>
    

1. **DeepBlueCLI** is a tool that was created by SANS to aid the investigation and triage of Windows Event Logs
    

* Run the command to a specific local log file
    
    <table><tbody><tr><td colspan="1" rowspan="1"><p>1</p></td><td colspan="1" rowspan="1"><p>./DeepBlue.ps1 ../Log1.evtx</p></td></tr></tbody></table>
    
* Run the command to analyze the system we are currently on
    
    <table><tbody><tr><td colspan="1" rowspan="1"><p>1 2 3 4</p></td><td colspan="1" rowspan="1"><p># to analyze a live security log ./DeepBlue.ps1 -log security # to analyze a live system log ./DeepBlue.ps1 -log system</p></td></tr></tbody></table>
    

## **Appendix A — Logs Information Details**

---

### **Logon Type (Event ID: 4624)**

| Type | Description |
| --- | --- |
| 2 | Interactive (interactively logged on, meaning a physical logon to the device) |
| 3 | Network (accessed system via network) |
| 4 | Batch (started as an automated batch job) |
| 5 | Service (a Windows service started by service controller) |
| 6 | Proxy (proxy logon; not used in Windows NT or Windows 2000) |
| 7 | Unlock (unlock workstation - think Interactive logon, but unlocking to resume a previous session) |
| 8 | NetworkCleartext (network logon with cleartext credentials) |
| 9 | NewCredentials (used by RunAs when the `/netonly` option is used) |

### **NETLOGON LOG ERROR CODE (Event ID: 4625)**

| NETLOGON log error code | Description |
| --- | --- |
| 0xC0000064 | The specified user does not exist |
| 0xC000006A | The value provided as the current password is not correct |
| 0xC000006C | Password policy not met |
| 0xC000006D | The attempted logon is invalid due to a bad username |
| 0xC000006E | User account restriction has prevented successful login |
| 0xC000006F | The user account has time restrictions and may not be logged onto at this time |
| 0xC0000070 | The user is restricted and may not log on from the source workstation |
| 0xC0000071 | The user account’s password has expired |
| 0xC0000072 | The user account is currently disabled |
| 0xC000009A | Insufficient system resources |
| 0xC0000193 | The user’s account has expired |
| 0xC0000224 | User must change his password before he logs on the first time |
| 0xC0000234 | The user account has been automatically locked |

### **Linux Logs**

* `/var/log/auth.log` — contains system authorization information. i.e. user logins.
    
* `/var/log/dpkg.log` — contains information that is logged when a package is installed or remove using *dpkg*.
    
* `/var/log/btmp` — contains information about failed login attempts.
    
* `/var/log/cron` — logs information about cron job.
    
* `/var/log/secure` — contains information related to authentication and authorization.
    
* `/var/log/faillog` — contains user failed login attempts.