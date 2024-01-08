Hello, today we'll cover this CTF made by [TryHackMe](https://tryhackme.com/room/wgelctf) - Wgel


![image](https://github.com/Renat9s/tryhackme/assets/126417250/0547c2e8-f9da-4dc0-8abe-f823c90b67ad)





## Reconnaissance 


First thing first, start with some enumeration.

```

nmap -A 10.10.221.211


```


* **-A**: this enables OS detection (-O), version scanning (-sV), script scanning
    (-sC)

## Result 

![image](https://github.com/Renat9s/tryhackme/assets/126417250/f69df22b-8707-4217-8b0b-75c00fe3c7ab)

so as we can see ssh and http are open we can use it latter.
-----------------------------------------------------------------------------------------------------

### page source

check out the page’s source code. There is a comment:

![image](https://github.com/Renat9s/tryhackme/assets/126417250/5d7dacf6-0fad-42ab-9b22-d641bf8f6ad5)

take a note may be a username !



* to run a brute-force of extensions on website we use a tool called gobuster.
* You can see more information about the tool [here](https://hackertarget.com/gobuster-tutorial/) -Gobuster
-------------------------------------------------------------------------------------------------------------

```
gobuster dir -u http://10.10.221.211/ -w /usr/share/wordlists/dirb/common.txt
```


# Result

```
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.221.211
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/.htaccess            (Status: 403) [Size: 278]
/.hta                 (Status: 403) [Size: 278]
/.htpasswd            (Status: 403) [Size: 278]
/index.html           (Status: 200) [Size: 11374]
/server-status        (Status: 403) [Size: 278]
/sitemap              (Status: 301) [Size: 316] [--> http://10.10.221.211/sitemap/]
Progress: 4614 / 4615 (99.98%)
===============================================================
Finished
```





so here we go! found something named /sitemap lets check it out with gobuster again



```

gobuster dir -u http://10.10.221.211/sitemap -w /usr/share/wordlists/dirb/common.txt

```



## Result 


```

[+] Url:                     http://10.10.221.211/sitemap
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/.hta                 (Status: 403) [Size: 278]
/.htaccess            (Status: 403) [Size: 278]
/.htpasswd            (Status: 403) [Size: 278]
/.ssh                 (Status: 301) [Size: 321] [--> http://10.10.221.211/sitemap/.ssh/]
/css                  (Status: 301) [Size: 320] [--> http://10.10.221.211/sitemap/css/]
/fonts                (Status: 301) [Size: 322] [--> http://10.10.221.211/sitemap/fonts/]
/images               (Status: 301) [Size: 323] [--> http://10.10.221.211/sitemap/images/]
/index.html           (Status: 200) [Size: 21080]
/js                   (Status: 301) [Size: 319] [--> http://10.10.221.211/sitemap/js/]
Progress: 4614 / 4615 (99.98%)
===============================================================
Finished
```



i found some intresting directory “/.ssh , so let’s see what’s in there.


![image](https://github.com/Renat9s/tryhackme/assets/126417250/54f063b0-455d-4a80-a578-39c59d395592)

its a private key!

the id_rsa can be used to login remotly into SSH, 

we need to set the permissions of the file


```
chmod 600 id_rsa
```
--------------------------------------------------------------------------------------------------------------------


and here we goooo, i logged in with the user i saved it before and the private key into ssh.

![image](https://github.com/Renat9s/tryhackme/assets/126417250/7e623f9e-a471-4993-9260-99cbd5655e09)


now you can move around and search everywhere. then you can find the user_flag.txt easy peasy lemon squeezy.

![image](https://github.com/Renat9s/tryhackme/assets/126417250/a0b98e22-85d5-47ce-b737-b6b8df1a4fc9)
-------------------------------------------------------------------------------------------------------------


after that we have to find the root flag also!

![image](https://github.com/Renat9s/tryhackme/assets/126417250/712a49ff-7445-4b65-84c5-cc967124d36d)


* It can be seen that I can run "wget" as root.
-------------------------------------------------

so, now i know for sure where is my root flag, i have two option either i read it from the machine or i copy it in my machine then read it. i rather read it in target machine.

first to do :

open a netcat listener in my machine

![image](https://github.com/Renat9s/tryhackme/assets/126417250/11d55bc6-e2b7-430a-ae16-f6b43915739e)


Then, let’s run the command on the victim machine:
** you will receive the flag in your terminal machine

![image](https://github.com/Renat9s/tryhackme/assets/126417250/2778df89-4165-4f63-b5da-072e86019bd9)


The End, HAPPY HACKING <3
