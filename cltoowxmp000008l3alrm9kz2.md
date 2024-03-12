---
title: "TryHackMe: Mr Robot CTF — Writeup"
seoTitle: "TryHackMe: Mr Robot CTF — Writeup"
seoDescription: "TryHackMe: Mr Robot CTF — Writeup"
datePublished: Tue Mar 12 2024 18:12:49 GMT+0000 (Coordinated Universal Time)
cuid: cltoowxmp000008l3alrm9kz2
slug: tryhackme-mr-robot-ctf-writeup
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1710266920110/169802a7-c24d-4b35-a7b6-0be825ce9a34.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1710267143851/8745fb68-3f77-482a-a95f-94bbc5eee2b0.jpeg
tags: hacker, ctf, cybersecurity-1, tryhackme, ctf-writeup, ferdibirgul

---

Link to tryhackme [https://tryhackme.com/room/mrrobot](https://tryhackme.com/room/mrrobot).  
You can downloaded and deployed locally using the machine provided on vulnhub: [https://www.vulnhub.com/entry/mr-robot-1,151/](https://www.vulnhub.com/entry/mr-robot-1,151/)

No matter you are using tryhackme or vulnhub, our task is to get `3keys.`

## **Nmap Scan**

![](https://miro.medium.com/v2/resize:fit:1050/1*eTHNFiFATJmizaHtS1kh-w.png align="left")

Looking at the result of nmap scan, port 22 ssh is closed. Port 80 http is up and running Apache http. Also port 443 is up.

Visiting ip in browser in reveals an interesting website.

![](https://miro.medium.com/v2/resize:fit:1050/1*Zfj5L1JgXxmxCGJPzZX3uQ.png align="left")

I highly reccomend you to check the website and dig around by entering the commands shown.

![](https://miro.medium.com/v2/resize:fit:1050/1*WEhW6lI61it3kLFaOpH5Aw.png align="left")

Using wappalyzer extension reveals wordpress is running. I used nikto tool to get additional details.

Then I ran gobuster to do some directory fuzzing.

![](https://miro.medium.com/v2/resize:fit:1050/1*5cUoBUvRIW5KGENR88ivOg.png align="left")

Go and visit the different directory revealed by go buster.

Among the result, I am interested in /robots or /robots.txt

![](https://miro.medium.com/v2/resize:fit:1050/1*Z3Vti8wZ6O0-BsDxwkTbcQ.png align="left")

we have `fsocity.dic` and `key-1-of-3.txt` listed under `/robots.txt`

![](https://miro.medium.com/v2/resize:fit:1050/1*PtKIrtFLKi_ueHHpiXebfA.png align="left")

Going into `/key-1-of-3.txt` reveals the 1st key of the challange.

> *073403c8a58a1f80d943455fb30724b9*

![](https://miro.medium.com/v2/resize:fit:1050/1*4-nkP-TePan0qF_x3r5Jow.png align="left")

going into `/fsocity.dic` downloads a dictionary file called `fsocity.dic`

![](https://miro.medium.com/v2/resize:fit:791/1*oDPRX3BRGyYF6VRZ_5LI2g.png align="left")

`fsocity.dic` contains wordlist which we can use to bruteforce username and password.

![](https://miro.medium.com/v2/resize:fit:1050/1*jlDkvV4JYb_F3rxijykfDQ.png align="left")

`/wp-login.php` reveals us login panel of wordpress.

![](https://miro.medium.com/v2/resize:fit:758/1*isUuLmR5CF0p2Ch53kHxpg.png align="left")

Key thing to note is, website gives different response when username is incorrect and different response when username is correct but passoword is incorrect. This is a huge flaw.

We will be using this flaw to get our self username first and then get password.

For that enter any username and password and intercept the request using burpsuite.

![](https://miro.medium.com/v2/resize:fit:1050/1*TebuyAam1BTeYZCILjdSlA.png align="left")

Highlighted section is the part we are concerned about. Using this part we will brute force the username.

![](https://miro.medium.com/v2/resize:fit:1050/1*Hzjcr-FJrJY8YgcJKRlQwQ.png align="left")

We are using hydra to brute force the username.

`hydra -L fsocity.dic -p 123453453 {IP} http-post-form “/wp-login.php:log=^USER^&pwd=^PASS^:Invalid username”`

in above command  
`-L` to Specifiy the username list file  
`-p` to specify password , in this case we are using random password since we are bruteforcing user name.  
`http-post-form` specifies the HTTP post method to use (got from burp result)  
`/wp-login.php` url of login page  
`log=^USER^&pwd=^PASS^` will replace `^USER^` with values from the user list and `^PASS^` will replace from `-p` value.  
NOTE: log and pwd , we got from burp result.  
`:Invalid username`: The error message returned when the login attempt fails

> *Username: Elliot*

![](https://miro.medium.com/v2/resize:fit:995/1*-F18fhfRJk-KHuqy1cTxNg.png align="left")

When we enter correct username but password is incorrect then it is giving different response.

We now have username. Lets bruteforce the password now.  
You can use hydra tool to do this using similar command, in my case hydra was taking very long time so i switched to use `wpscan`

![](https://miro.medium.com/v2/resize:fit:1050/1*nq_fyZrkh9esKVFpvGg18g.png align="left")

![](https://miro.medium.com/v2/resize:fit:1050/1*Ygveuh_h1F4NtQ31d9Uigg.png align="left")

And we got password

> *Username: Elliot, Password: ER28–0652*

lets login with this credentials.

![](https://miro.medium.com/v2/resize:fit:1050/1*ey3WikG2XqskyQwlXx_qrg.png align="left")

we have access to wordpress dashboard.  
What to do next?

Out best step would be to inject or replace the php file to malicious one. So that when the website runs the php we get ourself reverse shell.  
For this i will be using php reverse shell from pentestmonkey [https://github.com/pentestmonkey/php-reverse-shell](https://github.com/pentestmonkey/php-reverse-shell)

![](https://miro.medium.com/v2/resize:fit:1050/1*oltpwG0uizG2i3JdEatiGw.png align="left")

Go to Appearance &gt;&gt; Editor &gt;&gt; 404.php then replace the code with the code from pentestmonkey.  
In $IP field add your ip and you can change the port field if you want.

click update file.

In you attacker machine make netcatlistner ready using  
`nc -lnvp 443` make sure to use same port.

![](https://miro.medium.com/v2/resize:fit:1050/1*ExKQhRdmhAYW5aZ1WAP5CA.png align="left")

After your listener is ready , visit directory which can give 404 error.

![](https://miro.medium.com/v2/resize:fit:1050/1*vmaGziXpcz-83dQCVt29jQ.png align="left")

Looking at our listener, we have a shell

![](https://miro.medium.com/v2/resize:fit:840/1*5WAW2s0cyVmMT-HOXkQ0xA.png align="left")

upgrade you shell using  
`python -c ‘import pty;pty.spawn(“/bin/bash”)’`

![](https://miro.medium.com/v2/resize:fit:930/1*dR5ZSWVurBRSygMMnoXKOQ.png align="left")

looking at the home directory of robot user. We can see to files.  
`key-2-of-3.txt` and `password.raw-md5`

we don’t have access to `key-2-of-3.txt` but we can read `password.raw-md5`  
reading the password file reveals what looks like username and md5 encrypted password.

> *robot:c3fcd3d76192e4007dfb496cca67e13b*

![](https://miro.medium.com/v2/resize:fit:1050/1*BAsTgSHZm44uKkEUStINVw.png align="left")

decrypting the password reveals `abcdefghijklmnopqrstuvwxyz`

lets switch user to `robot`

![](https://miro.medium.com/v2/resize:fit:492/1*JbRfUOD8N09ol7q57yEa8A.png align="left")

![](https://miro.medium.com/v2/resize:fit:461/1*cFxzExxmLgAGw-PRmqkkHw.png align="left")

> *822c73956184f694993bede3eb39f959*

We got 2 keys. One last remaining.

![](https://miro.medium.com/v2/resize:fit:1014/1*JYP0SSYtRRGR_ydXFq80jA.png align="left")

looking at `/etc/passwd` file , there isn’t any other user. So our aim is to get root access.

for this we will be using `linpeas` linux privelege escalation tool. Download `linpeas.sh` from here. [https://github.com/carlospolop/PEASS-ng/tree/master/linPEAS](https://github.com/carlospolop/PEASS-ng/tree/master/linPEAS).

On you downloaded folder setup a http server using python

![](https://miro.medium.com/v2/resize:fit:954/1*_SNLDwPTuxliq18ExNmWYQ.png align="left")

![](https://miro.medium.com/v2/resize:fit:1023/1*DRiIVHE2lcF2nZdBfUnLOg.png align="left")

then go to `/tmp` directory and download linpeas from your attacker machine to mr robot machine using `wget`

![](https://miro.medium.com/v2/resize:fit:1050/1*blgyfB8-eD_s5hhPpfSzrw.png align="left")

give linpeas.sh `executable permission` using `chmod +x linpeas.sh`  
and finally run linpeas using `./linpeas.sh`

![](https://miro.medium.com/v2/resize:fit:1050/1*bn4R4HW7eGHjmrCoutAqCA.png align="left")

Among the result, the eye catchy was, nmap have suid set. Which means we can use nmap to run as root.

Since nmap runs as root, we can use its interactive feature to spawn a shell .which will be root.

![](https://miro.medium.com/v2/resize:fit:1050/1*j8pyUPBuiq-LvwAkzImgpg.png align="left")

[https://gtfobins.github.io/gtfobins/nmap/](https://gtfobins.github.io/gtfobins/nmap/)  
remember to use our handy website gtfobins for more info.

![](https://miro.medium.com/v2/resize:fit:870/1*r8IRSPHrGJo7_wBzhGUbbQ.png align="left")

using the interactive feature we got ourself root access.  
and we can read our final key.

> *04787ddef27c3dee1ee161b21670b4e4*

thank you happy hacking ⚔️