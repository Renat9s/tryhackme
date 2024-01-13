# [RootMe](https://tryhackme.com/room/rrootme)

### A ctf for beginners, can you root me?
--------------------------------
# Enmuration 

* -sC : for Script scanning, Scan with default NSE scripts. Considered useful for discovery and safe.
* -sV : Attempts to determine the version of the service running on port.
* -Pn : Scan without pinging.
* -p- : scan for all ports.
* --open : Show open ports only.

=================================


# Result 

![image](https://github.com/Renat9s/tryhackme/assets/126417250/529ed0f4-8916-4167-9f33-0868b08c3a1b) 

we got 2 open port.
after browser the website nothing interesting was found.

---------------------------------------------------------------------------------------------------
#### Now lets do dir scanning, for hiddin directory, i used ```Gobuster```
![image](https://github.com/Renat9s/tryhackme/assets/126417250/70f9fd84-f3d2-4d46-add4-1c94f117e472)

and there i found something,
-------------------
![image](https://github.com/Renat9s/tryhackme/assets/126417250/2ca0861c-13d8-4691-a73a-dbf3f67c966d)
#### Lets try here to uploud reverse shell,
[PhpReverseShell](https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php) -
* you need to change the port and IP .
i couldnt bypass it with extension php, its not allowed, i tried so many things and came up with ```.php5```
and you could also use extension ```.phtml```
* You can simply change the file extension by using the mv command.
  ------------------
  1 - Now set the netcat as reverse shell listener in my machine,
  
  * Synstax : nc lnvp [ port ].
   
  2 - Go to `/uploads` directory from the previous `gobuster` scan. Checking it, we have our reverse shell, now click on it.
  
  ^ http://ip/uploads/ 
     
 ### keep in your mind you need to put the right ip in the reverse shell file. 
 ![image](https://github.com/Renat9s/tryhackme/assets/126417250/fc4561e2-2511-4ee2-b898-7dbb3b0def8c)
* i also  need to upgrade our shell session to clear the screen. To do this:
```

python3 -c 'import pty; pty.spawn("/bin/sh")'

```

* Navigating to home directory, we found user.txt flag.

----
## Privilege escalation
### you could skip all this and use tool called "linPEAS" for privilege escalation, it save your time, but since he give us the hint for "SUID" lets dig.
------------
##### Use this command:
```

find / -perm -u=s -type f 2>/dev/null

```
 * command can be used to find all binaries on the system that have the SUID 
 
##### Using our next question as a hint we need to search for files with SUID permissions. 
now Checked for SUID files, There was python which unusual and we can run as sudo.
I checked for that on [GTFOBins](https://gtfobins.github.io/) -
* Run the Script. and here we go!

![image](https://github.com/Renat9s/tryhackme/assets/126417250/2454f91d-acb1-43e2-93cf-78ee3889ca6e)


 #### located to /root and there was the root flat 
---------------------------------------------------------------------------

the end <3
