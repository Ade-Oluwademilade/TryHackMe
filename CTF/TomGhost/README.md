WRITE UP FOR TRYHACKME TOMGHOST CTF

1. Fast nmap scan using -F flag

![nmap_scan](https://user-images.githubusercontent.com/105601553/200420915-c456445c-3dbd-4180-93c8-09aefeb57fbe.png)

2. Checked the web server on port 8080

![web server](https://user-images.githubusercontent.com/105601553/200421060-33f26aa4-cb11-44de-8f56-bcf59ed25239.png)

Nothing interesting on web server. Remember the other high port we got from our nmap scan... 8009 which is running ajp service.
Searched for exploit and found one on rapid7 which includes metasploit and one on GitHub which doesn't require metasploit.
I used the one I found on GitHub.

![ajp command](https://user-images.githubusercontent.com/105601553/200421766-bb8e66a8-7973-4d0a-a94b-38c4cd2c2e6d.png)

Below the result, I found credentials of a user.

![creds](https://user-images.githubusercontent.com/105601553/200421970-0564c39e-edbe-4538-a9ed-08b1a895c5a5.png)

SSH into the server using the credentials I found.

![ssh](https://user-images.githubusercontent.com/105601553/200422214-72c9c15e-1059-46cf-849f-5d4dd4313ea2.png)

The first flag is not in the directory of our logged in user but fortunately for us, our current user is permitted to change directory into the directory of the other user(merlin) and get the first flag.

![flag1](https://user-images.githubusercontent.com/105601553/200422525-aecf2d84-4779-4963-94c8-e4fbe7b2cd9a.png)

Checked if our current user has sudo permissions so we could elevate privileges. Unfortunately, he wasn't granted any sudo permissions.

![sudo pems](https://user-images.githubusercontent.com/105601553/200422783-136826bd-1f40-4b3c-bc52-b3c01c9e4122.png)

If you list the files in our logged in users directory. You'll find two files in there.
1. credentials.pgp
2. tryhackme.asc

![2files](https://user-images.githubusercontent.com/105601553/200423106-5de21657-6acb-4c71-878d-c2ce54365cfa.png)

Download these 2 files to your machine.
Imported the .asc file into gpg so it can be used to decrypt the .pgp file.

![import key](https://user-images.githubusercontent.com/105601553/200424067-81333ae6-b8ad-4906-b72e-9a94047eefee.png)

Decrypted the file and output the result into another file.

![output](https://user-images.githubusercontent.com/105601553/200424197-34a6b775-fe25-453b-b685-a147dabd4ecd.png)

Viewed the output and we got credentials of the second user.

![merlin cred](https://user-images.githubusercontent.com/105601553/200424327-1161072e-410b-4916-b1a3-cbe4e5666b23.png)

SSH into the server using the newly found credentials and check for sudo permissions.

![priv](https://user-images.githubusercontent.com/105601553/200424606-2efacb01-13d4-4752-84f5-852aa4645715.png)

Go to GTFOBins and look for how to escalate privileges.
Escalated privileges and we got a root shell

![root](https://user-images.githubusercontent.com/105601553/200424879-3d497224-bae7-4e28-90f2-b629996b8f9b.png)

THANK YOU!









