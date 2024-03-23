Hello people, today's challenge is a CTF by Tryhackme : )


![image](https://github.com/Renat9s/tryhackme/assets/126417250/dc488d5b-18b1-4864-8452-5fdfdb2f45b6)


[Room](https://tryhackme.com/r/room/jokerctf)

#### Lets get started!

### Enumeration :

```

nmap -sC -sV -Pn -p- <ip> --open

```

### Result :

```

PORT     STATE SERVICE REASON         VERSION
22/tcp   open  ssh     syn-ack ttl 63 OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 ad:20:1f:f4:33:1b:00:70:b3:85:cb:87:00:c4:f4:f7 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDL89x6yGLD8uQ9HgFK1nvBGpjT6KJXIwZZ56/pjgdRK/dOSpvl0ckMaa68V9bLHvn0Oerh2oa4Q5yCnwddrQnm7JHJ4gNAM+lg+ML7+cIULAHqXFKPpPAjvEWJ7T6+NRrLc9q8EixBsbEPuNer4tGGyUJXg6GpjWL5jZ79TwZ80ANcYPVGPZbrcCfx5yR/1KBTcpEdUsounHjpnpDS/i+2rJ3ua8IPUrqcY3GzlDcvF7d/+oO9GxQ0wjpy1po6lDJ/LytU6IPFZ1Gn/xpRsOxw0N35S7fDuhn69XlXj8xiDDbTlOhD4sNxckX0veXKpo6ynQh5t3yM5CxAQdqRKgFF
|   256 1b:f9:a8:ec:fd:35:ec:fb:04:d5:ee:2a:a1:7a:4f:78 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBOzF9YUxQxzgUVsmwq9ZtROK9XiPOB0quHBIwbMQPScfnLbF3/Fws+Ffm/l0NV7aIua0W7FLGP3U4cxZEDFIzfQ=
|   256 dc:d7:dd:6e:f6:71:1f:8c:2c:2c:a1:34:6d:29:99:20 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIPLWfYB8/GSsvhS7b9c6hpXJCO6p1RvLsv4RJMvN4B3r
80/tcp   open  http    syn-ack ttl 63 Apache httpd 2.4.29 ((Ubuntu))
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: HA: Joker
| http-methods: 
|_  Supported Methods: POST OPTIONS HEAD GET
8080/tcp open  http    syn-ack ttl 63 Apache httpd 2.4.29
| http-auth: 
| HTTP/1.1 401 Unauthorized\x0D
|_  Basic realm=Please enter the password.
|_http-title: 401 Unauthorized
|_http-server-header: Apache/2.4.29 (Ubuntu)


```




* we have 3 ports, ssh on 22 and apache on 80 and 8080. but 8080 need credentials to access.


![ePoPZhwuDd](https://github.com/Renat9s/tryhackme/assets/126417250/b967d2d1-db2e-4bc1-9750-9383d416361f)


Visiting the web server reveals the following page:

![awbDrTaNPz](https://github.com/Renat9s/tryhackme/assets/126417250/3e3ca129-e35c-4985-844e-14adaa331910)

* we also do a directory scan with ```gobuster``` to find the secret file, and found nothing intersting i also did 1 more time but this time i add extenshion txt,xml and found this :

![vmware_pLpdJGooEB](https://github.com/Renat9s/tryhackme/assets/126417250/aca96fdc-277e-48e3-9195-1ecb11a9f717)

![vmware_KXeDMTw7La](https://github.com/Renat9s/tryhackme/assets/126417250/6eec1aff-d49c-42b4-acd6-8c54a3ceeaa0)

- i have a secret conversation between Batman and the Joker, might be users.
* checking other directories and backend php file info doesn't give us anything for now

  * next thing to do is brute-forcing in port 8080 using the two user from the secret conversation:

![image](https://github.com/Renat9s/tryhackme/assets/126417250/d3aa56e3-584d-4b4b-b923-627f744d94f2)

![vmware_hiTORZ0VQs](https://github.com/Renat9s/tryhackme/assets/126417250/65aeb2be-d6f8-4e85-89d4-82b589fab2b5)



### Another gobuster to search the directory on 8080 with the credentials, and didnt five anything so i have hint from the questions " use nikto " :


![image](https://github.com/Renat9s/tryhackme/assets/126417250/9a5fa74a-d7ca-44b9-b80f-ad06feab6137)

* i gathered  a lot of usefull information, 1 - : first thing to look at backup.zip file, then 2 - : /administrator directory.

1 : 

![vmware_xKNTuO6kRM](https://github.com/Renat9s/tryhackme/assets/126417250/edc6879d-f5ff-4bc0-a751-fb2a66d28648)

* Download the backup.zip and it was encrypted!
![vmware_dwJcrfinN4](https://github.com/Renat9s/tryhackme/assets/126417250/35afdfc1-3104-4d0c-977c-08d88cd84779)


* Now Cracking a zip :

![image](https://github.com/Renat9s/tryhackme/assets/126417250/b1fdb717-a822-4065-ba78-327a79d74224)


* after unzip the file we have two folder " site, db "
* i want to go th ```db``` i think its about database because of his name, inside the db i have joomladb.sql i opened it with ```mousepad```

![vmware_Ofr2KKZLE5](https://github.com/Renat9s/tryhackme/assets/126417250/d2a54739-a078-4db4-8c5d-7d579a7a2b1f)

#### Found this

![vmware_UD6NYchgNS](https://github.com/Renat9s/tryhackme/assets/126417250/73bb9da2-fe75-4d45-8d20-439d3aa33735)

* hash! i copy it into another file named it ```think``` and crack it with ```john```
![image](https://github.com/Renat9s/tryhackme/assets/126417250/0798a1d7-84c4-43ab-a5aa-923a585fc8cd)

* now take this credentials and go to /administrator and login

* after search around i want to try to get a shell.
go to Extensions , Templates, choose beez3. because i can edit the php directorys.
#### choose preview the template to run the code!

from [Here](https://www.revshells.com/) i get the reverseShell

* now i just need to set up a listener and run the shell.

![vmware_79Ddz8eOPs](https://github.com/Renat9s/tryhackme/assets/126417250/ee7ca113-ee8d-4403-b83a-b045e670e8a5)


* im in now!

* now i know the user and the group, first thing got my attention was the group ```lxd```
google about it found [this](https://www.exploit-db.com/exploits/46978) for privilege-escalation.

* follow the steps bellow :
![vmware_msdbSXu0eY](https://github.com/Renat9s/tryhackme/assets/126417250/18220941-88bd-404a-bc0a-7e15f8ee6975)

first thing run the command :


```


wget https://raw.githubusercontent.com/saghul/lxd-alpine-builder/master/build-alpine


```

and it well download new file ```build-alpine```, run :


```

sudo bash build-alpine

```

another file :
![image](https://github.com/Renat9s/tryhackme/assets/126417250/cc45acfb-7e0f-4e83-84c3-66921baa12b3)


after these steps i did it like this :

![image](https://github.com/Renat9s/tryhackme/assets/126417250/2f097706-b039-4617-af1c-3ac285b6eea2)


* run python server to download these file into the victim machine.

* navigate to /tmp 

![vmware_0YqcVK3SLl](https://github.com/Renat9s/tryhackme/assets/126417250/0afdb1be-5aa2-48fb-b13c-82dc6241c5c4)

#### change the permission :

```

$ chmod +x yalla.sh

```



* Now run it like this : )

![image](https://github.com/Renat9s/tryhackme/assets/126417250/4a9f8bf5-3e75-4f5a-a809-65678a85f657)

* search around, navegate to /mnt/root

then do the rest of it : )

Good luck have fun < 3
