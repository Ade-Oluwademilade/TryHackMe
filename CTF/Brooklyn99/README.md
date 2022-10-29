Running nmap scan on target IP using -sC flag

![nmap_scan](https://user-images.githubusercontent.com/105601553/198828403-60d33cad-ccfa-4b70-a968-e3954516bd62.png)

Notice FTP allows anonymous login, and it even shows us a file.

![ftp](https://user-images.githubusercontent.com/105601553/198828508-b5bdb799-ee41-4f37-af99-6f8b1657a58a.png)

Logged in via FTP and downloaded the file(note_to_jake.txt)

![ftp login](https://user-images.githubusercontent.com/105601553/198828556-4c77839b-7b3d-4b68-9ccc-518ba7396254.png)

Opened the file and luckily for us, we have the name of 3 users(Amy, Jake, Holt)

![ftp_file](https://user-images.githubusercontent.com/105601553/198828657-77ab1880-894f-4b62-add2-3e8b1cda3284.png)

You can attempt brute forcing the passwords for the users using Hydra. I decided to enumerate further.
Checked the web app running on port 80, but it was just an image with boring messages beneath.

![port80](https://user-images.githubusercontent.com/105601553/198828793-e44168c6-4b08-4205-be74-6caf12e400ae.png)

Checked the page source, it was also boring. Saw a quite interesting comment at the bottom.

![pg_source](https://user-images.githubusercontent.com/105601553/198828949-05711890-f0e3-4116-8911-abd968036844.png)

Looked up what steganography was on google.

![steganography](https://user-images.githubusercontent.com/105601553/198828980-31db5aca-dfa4-4620-9976-ee9c2b22c7c8.png)

Now, I'm guessing there's some sort of information hidden beneath the image on the web.
Downloaded the image to my computer and attempted to find the hidden information using steghide, but it was asking for a 'passphrase'.
Used stegcracker to brute force the passphrase for the picture.

![stegcrack_result](https://user-images.githubusercontent.com/105601553/198829172-7fc652b2-84a1-44b2-9b60-bc965bad835d.png)

Voila! We got the password. Now let's use the password to see what's hidden behind the image.

![steghide](https://user-images.githubusercontent.com/105601553/198829258-633749ef-76ed-432f-80aa-39c7e9f69d31.png)

Got a note.txt file.
Read the file and you've got holts password.

![steg_info](https://user-images.githubusercontent.com/105601553/198829301-351010e2-4d1b-4772-8da7-a812c030e4a8.png)

Log in to holts account using SSH

![ssh_login](https://user-images.githubusercontent.com/105601553/198829349-cae712e5-9dc5-4f4d-b4f1-0bc93d3a897a.png)

And... We're in!!
By the way, the users name is 'holt' not 'holts', so try not to make that mistake.

Read the user.txt file and get your first flag

![usertxt](https://user-images.githubusercontent.com/105601553/198829442-c1e2f87f-cc46-42b8-b883-00d2776067e6.png)

Change directory to root, so we can check for the root flag but unfortunately, Holt doesn't have access to the root directory.
So, let's check for sudo privileges assigned to Holt.

![root](https://user-images.githubusercontent.com/105601553/198829541-2f12d425-2f4a-4b90-8acc-0a944c6736de.png)

Head over to GTFObins to check how to escalate privileges

![gtfo](https://user-images.githubusercontent.com/105601553/198829572-bdf89532-a143-4787-b302-4879cd11e49a.png)

Run the commands and you should be able to get the root flag.

![rootflag](https://user-images.githubusercontent.com/105601553/198829595-161fdcc4-7b0c-4ad0-b1b3-7a88e5b1bf65.png)

THANK YOU!!









