Hello everyone! kitty writeup tryhackme 

Reconnaissance :

nmap -A ```ip``` -vv


We get back the following result showing that 2 ports are open :


* Port 80 running Apache httpd 2.4.41

* Port 22 running OpenSSH 8.2p1

---

```Bash

Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-04-07 07:17 EDT
NSE: Loaded 156 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 07:17
Completed NSE at 07:17, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 07:17
Completed NSE at 07:17, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 07:17
Completed NSE at 07:17, 0.00s elapsed
Initiating Ping Scan at 07:17
Scanning 10.10.106.166 [4 ports]
Completed Ping Scan at 07:17, 0.13s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 07:17
Completed Parallel DNS resolution of 1 host. at 07:17, 0.08s elapsed
Initiating SYN Stealth Scan at 07:17
Scanning 10.10.106.166 [1000 ports]
Discovered open port 22/tcp on 10.10.106.166
Discovered open port 80/tcp on 10.10.106.166
Completed SYN Stealth Scan at 07:17, 1.87s elapsed (1000 total ports)
Initiating Service scan at 07:17
Scanning 2 services on 10.10.106.166
Completed Service scan at 07:17, 6.23s elapsed (2 services on 1 host)
Initiating OS detection (try #1) against 10.10.106.166
Retrying OS detection (try #2) against 10.10.106.166
Retrying OS detection (try #3) against 10.10.106.166                                                                                                                  
Retrying OS detection (try #4) against 10.10.106.166                                                                                                                  
Retrying OS detection (try #5) against 10.10.106.166                                                                                                                  
Initiating Traceroute at 07:17                                                                                                                                        
Completed Traceroute at 07:17, 0.10s elapsed
Initiating Parallel DNS resolution of 2 hosts. at 07:17
Completed Parallel DNS resolution of 2 hosts. at 07:17, 0.08s elapsed
NSE: Script scanning 10.10.106.166.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 07:17
Completed NSE at 07:17, 3.44s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 07:17
Completed NSE at 07:17, 0.43s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 07:17
Completed NSE at 07:17, 0.00s elapsed
Nmap scan report for 10.10.106.166
Host is up, received echo-reply ttl 63 (0.10s latency).
Scanned at 2024-04-07 07:17:35 EDT for 24s
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE REASON         VERSION
22/tcp open  ssh     syn-ack ttl 63 OpenSSH 8.2p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 b0:c5:69:e6:dd:6b:81:0c:da:32:be:41:e3:5b:97:87 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCt6N8QTFPNouL2D0RrOP0gWnq3c+3uxXxxo3WkwE+Z+8KF8ox+bJRYWzbPk1RmEQv1ZFKDBNgbdrddpeP0SiC1y/tOQRb//1vy2ZqNtWyvDtHssObe62/F6yCl8eHC4jcbwLuzpEkAPEPbD/pPq9H5mueKqoIDAH2MAeuSf/XX/FQEhM51Bs+ADizyDeC2SfHa0W/U99ZyHFvqxlIYz5ZT43HVDiKmT9Di/9wclWmpwkpXgY6GtYjhrEez1+686rhVdWx8AJ5GRr5mvsM/VfiikTeNaLhaMVgT1BvfB4lOyeQ57Jiv+2xKd0Bx1fQ1fb2UiUFVRjXUEQVLqa7bOK1jcyuGw5KFXVoYfQcsgvllOxW3fJIMbnPYxxNgYhbYKv58cA13C1k5pgqyXxTep4lHAlFCaA1pcBZfPp2PTQET7cdtkJxmNyWWHfI1IqsyAZ4OQwKX0SxLEGdlviWn8GtZlF1l35LEeYu0YX4Mz847wX+9sf/dBWJNefPJgdqgVCs=
|   256 6c:65:ad:87:08:7a:3e:4c:7d:ea:3a:30:76:4d:04:16 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBAWsc0tSRz6I0J/ap+bL8NzXIAM8Qb/CnghvNICsIfjYrgd8dFCNAcbRDu0G3PC2L81wjcHAdkERcgNr5OzETmE=
|   256 2d:57:1d:56:f6:56:52:29:ea:aa:da:33:b2:77:2c:9c (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIOKiCZ2jVlW9/4CE63CtF8LcLBR+TJpEXonlXaj0LRE+
80/tcp open  http    syn-ack ttl 63 Apache httpd 2.4.41 ((Ubuntu))
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-title: Login
|_http-server-header: Apache/2.4.41 (Ubuntu)
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.94SVN%E=4%D=4/7%OT=22%CT=1%CU=35978%PV=Y%DS=2%DC=T%G=Y%TM=66128
OS:0E7%P=x86_64-pc-linux-gnu)SEQ(SP=101%GCD=1%ISR=10B%TI=Z%CI=Z%II=I%TS=A)O
OS:PS(O1=M508ST11NW7%O2=M508ST11NW7%O3=M508NNT11NW7%O4=M508ST11NW7%O5=M508S
OS:T11NW7%O6=M508ST11)WIN(W1=F4B3%W2=F4B3%W3=F4B3%W4=F4B3%W5=F4B3%W6=F4B3)E
OS:CN(R=Y%DF=Y%T=40%W=F507%O=M508NNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F
OS:=AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5
OS:(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z
OS:%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=
OS:N%T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%
OS:CD=S)

Uptime guess: 21.391 days (since Sat Mar 16 21:55:08 2024)
Network Distance: 2 hops
TCP Sequence Prediction: Difficulty=257 (Good luck!)
IP ID Sequence Generation: All zeros
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 110/tcp)
HOP RTT       ADDRESS
1   104.42 ms 10.9.0.1
2   104.47 ms 10.10.106.166

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 07:17
Completed NSE at 07:17, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 07:17
Completed NSE at 07:17, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 07:17
Completed NSE at 07:17, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 24.68 seconds


```



------------------------------------------------------------------

Next > i will run a feroxbuster scan to enumerate the directory since we are dealing with php, lets add extention ```php``` 

However, feroxbuster didn’t find anything interesting for now :

![feroxbuster](https://github.com/Renat9s/tryhackme/assets/126417250/ddb4151d-4b45-420a-bd6f-ec5f9870f9b8)


------------------------------------------------------------------

Enumeration :

As usual, I always start with enumerating HTTP first, in this case i only have a login page, so test a simple SQL injection.

* using kitty user mentioned it's about a kitty website, after trying some sql queries, looks like we have a POC for SQLi :



![or](https://github.com/Renat9s/tryhackme/assets/126417250/53ea7a51-20a3-40cd-b895-9776e16a27cd)

![detect](https://github.com/Renat9s/tryhackme/assets/126417250/110aacaa-e347-4bf7-afe2-bfb29a5abf0e)


----------------------------------------------------------------------------------------------------------


![and](https://github.com/Renat9s/tryhackme/assets/126417250/e735ea5c-79bc-4dc0-b402-805c40c2ac55)


![confirm sqli](https://github.com/Renat9s/tryhackme/assets/126417250/fb4e70e9-7b95-4177-9082-c0960be711cc)


 it’s detecting SQLi when there’s ‘ OR ‘ in the username field but doesn’t detect on ‘ AND,

 So there are some SQL Injection filters on the login page.

* confirms that we defenitly have a SQL Injection.

"this means we can perform a boolean based injection, with the 302 response beeing True and the 200 response beeing False."


200 - > false


302 - > true


After we have logged in with the kitty user, ended up being a dead end. 

so i need to know the password so maaaaybe i could ssh into the machine.

-------------------------------------------------------------------
now it’s time to grab the data manually :

database name from boolean sqli :

Im gonna use 'burpsuite' intercept it then send it to repeater and test :
first, we need to find out how many columns the sql query from the backend is returning, we can do that with the UNION SELECT ;

![columns](https://github.com/Renat9s/tryhackme/assets/126417250/ffb6317c-3d27-4fd3-80eb-64a9fa3f68f7)

* We have 4 columns. Done.
---------------------------------------------------------------------


enumerating the database name :

1 :



![database](https://github.com/Renat9s/tryhackme/assets/126417250/9e965ee6-25fb-4696-b5ab-a947c3d30f5b)


2 :


![database2](https://github.com/Renat9s/tryhackme/assets/126417250/b043dad1-fc98-495e-9d12-feb3f6c7f7ed)



3 :



![database3](https://github.com/Renat9s/tryhackme/assets/126417250/5a98bc0d-4366-4b2a-99a2-90970b1978ca)


4 :



![database4](https://github.com/Renat9s/tryhackme/assets/126417250/2e19bd6c-9b8d-4b81-a0dc-af509bb9a3bd)



We have the database name!

---------------------------------------------------------------------

Same thing on Table :



![table](https://github.com/Renat9s/tryhackme/assets/126417250/bfe1f4ea-81d6-41b2-8c8b-9946f0fc88a7)




![table name](https://github.com/Renat9s/tryhackme/assets/126417250/6edf7f6d-b709-4459-87c7-ef438155d4d4)



Got the table name.
----------------------------------------------------------------------
Lets grab the password since we already know the user : )
First create a password.txt contain a-z , 0-9 ;
make the query, then set your payload for two, the first payload for numbers choose from 1 to 32 by step 1. first one done,

move to second: payload set simple list ; then add to your payload sitting the password.txt we make it before then hit start attack < 3

* Remember we need to focus on response 302 only .



![password](https://github.com/Renat9s/tryhackme/assets/126417250/4b86bbf4-206b-4605-af37-b1ee49dbfb4e)


Here i got it, but cannot log in via ssh, not correct!
but i notice i get everything in lowercases letter : ) !
if i want it t obe match case-sensitively, cast the value as BINARY! and add it to 'password.txt ' dont forget to add also 

--->>> (- _ @ # $ %,...) then hit strat attack : )


Cool! now i have everything gonna see if i can use it to access ssh :

Gret!! im in :d
sweet sweet userflag < 3


![vmware_ZegGmtLXpE](https://github.com/Renat9s/tryhackme/assets/126417250/d928b92d-5a2e-4593-b7d1-722344483f43)





 Privilege Escalation :


we dont have sudo privileges.

going to use [linpeas.sh](https://github.com/peass-ng/PEASS-ng/tree/master/linPEAS)
open python http server from my machine, and from the target 


mine :



![vmware_mzI4WgrHIc](https://github.com/Renat9s/tryhackme/assets/126417250/a28e2fe8-28e8-4ec6-80bc-04c459ebc241)




target :



![vmware_8anpdczsC8](https://github.com/Renat9s/tryhackme/assets/126417250/2bafb0a4-964a-4361-b376-891d5bc6a4c8)


Run it 



![vmware_bQS7ZTY2Jt](https://github.com/Renat9s/tryhackme/assets/126417250/6387c1c0-4495-46c1-aa74-8adfe352d5e9)




thanks a lot to this tool <3333333



![vmware_PtdHITA2Xw](https://github.com/Renat9s/tryhackme/assets/126417250/6a74ca13-fafa-4872-89a9-ad7ae5f969d3)




lets go to mysql, i just want to see whether there are any other db.

```mysql -u kkitty -p ```


![vmware_rIgEZrprwq](https://github.com/Renat9s/tryhackme/assets/126417250/94653abf-2541-4612-895e-42359272e234)


we have devsite but nothing there, unfortunately it has the same user and password.
Lets navigate to the ```/var/www```


![vmware_l2kXPqPCPY](https://github.com/Renat9s/tryhackme/assets/126417250/7f683fd8-cd6b-4414-9987-0ad83b5da627)

interesting that evverything is owned by root!


the only difference between them in ```/development``` is that this is logged! we probably keep this in mind.

ok check for everything, unill reached for ```/opt```
* always check for ```/opt``` folder there's always stuff in this folder.



![vmware_R9PV8X64hD](https://github.com/Renat9s/tryhackme/assets/126417250/cf08325e-ff33-4c39-9058-28ea853ca7da)




Ok! this is a red flag here! there is a command execution and executing echo on this ip and then outputting to root loged and the input is /var/www/development,,,.........

i searched everywhere took a long long lolololong time to find out this :


```php
$ cat index.php 


...
$evilwords = ["/sleep/i", "/0x/i", "/\*\*/", "/-- [a-z0-9]{4}/i", "/ifnull/i", "/ or /i"];
foreach ($evilwords as $evilword) {
        if (preg_match( $evilword, $username )) {
                echo 'SQL Injection detected. This incident will be logged!';
                $ip = $_SERVER['HTTP_X_FORWARDED_FOR'];
                $ip .= "\n";
                file_put_contents("/var/www/development/logged", $ip);
                die();
        } elseif (preg_match( $evilword, $password )) {
                echo 'SQL Injection detected. This incident will be logged!';
                $ip = $_SERVER['HTTP_X_FORWARDED_FOR'];
                $ip .= "\n";
                file_put_contents("/var/www/development/logged", $ip);
                die();
        }
}
...

```

in the script it uses filtering kyeword! thats why SQLi was detected to evilWords, So im thinking maybe we able to manipulate the $ip to give us a root shell,


you can see its writing the header to the file,
"So, all we have to do in order to manipulate the value of $ip in the log_checker script is to make a request that contains an evil word, and change the value of the X-FORWARDED-FOR header to include “;” followed by a command.""

* Now just query that endpoint using cURL on the machine itself.


```bash
curl 127.0.0.1:8080/index.php -d 'username=sleep' -H 'X-Forwarded-For: test'
```



![vmware_APMGS210bR](https://github.com/Renat9s/tryhackme/assets/126417250/29a53785-d19b-4edc-86df-1e4e19bac773)




there is some data in logged now which is nice! and our test data is in here, this is going to be passed into that script, thats working : )

again, again :)

![vmware_TwRofSb26V](https://github.com/Renat9s/tryhackme/assets/126417250/e38cbc58-7df0-4421-8a14-857fea185141)



finally giving us a root shell <3


" So whenever you do SQL injection you need understand and check for what the application is returning in terms of, when we turn some results some valid results we're going to get a 302 in this case!

and when we dont turn valid results in this case we get a 200. and this is differnt from application to application, because like for example you might be on an application dosent return valid results and it might do be like a 302 to sonmething else like 'get back here' or.... So you just need to map what true and false looks like and thats basically the foundations of stealing data from databases, thats why we have the 200, 302.
i know the 302 is a vails response. "


##What is SQL Injection?

" SQL Injection is a type of vulnerability that allows attackers to run their own sql queries on the database using web software.
It usually allows an attacker to view data that they would not normally be able to access.
This sensitive data; may contain data belonging to other users or other data that the application itself has access to. "

if you want to know it more better and for practices i i recommend [portswigger](https://portswigger.net/web-security/sql-injection)

Thanks, Welcome.
