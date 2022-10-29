Started nmap scan on target.

![nmap_scan](https://user-images.githubusercontent.com/105601553/198832045-3a548c95-343b-49d9-bb5d-ae38900c5201.png)

Logged in anonymously via ftp.

![ftp_login](https://user-images.githubusercontent.com/105601553/198832073-41cdd083-f1eb-4fbc-9e30-5cd4339cf449.png)

Downloaded the files found on FTP server

![download files](https://user-images.githubusercontent.com/105601553/198832642-403b3e6b-d3e6-48cf-b4d7-acd6ef163a88.png)


Read the files... Locks files looks like a list of possible passwords.

***

Locks file

![passwords](https://user-images.githubusercontent.com/105601553/198832133-b695a487-2afb-402d-b9bd-1ee562b41ad2.png)

Tasks file contains a list of boring tasks.
Note: It does give us the name of a user

![tasks](https://user-images.githubusercontent.com/105601553/198832255-2a59c33f-87f7-459d-91f8-8512c1311b86.png)

***

We have the users name and a list of possible passwords.
Let's attempt brute forcing the user's password using this list.

![bforce](https://user-images.githubusercontent.com/105601553/198832329-082deae0-0865-4ec3-a87f-1977b48acfde.png)

Now, we have the username and password. Log in via ssh and find the users flag

![usertxt](https://user-images.githubusercontent.com/105601553/198832392-131159cd-266b-470d-a6ed-e3ef7c3a3698.png)

Check sudo privileges

![sudo priv](https://user-images.githubusercontent.com/105601553/198832427-337d4342-87df-462f-96ca-a3f72dae0356.png)

Search on GTFObins how to escalate priviledge.

![esc priv](https://user-images.githubusercontent.com/105601553/198832449-36d0dccd-ccd3-4791-ba53-d0dbdf8d7760.png)

Run the command and you get a root shell

![root](https://user-images.githubusercontent.com/105601553/198832508-d49afc15-f205-4595-988e-663babf8baa2.png)

Find the root flag in the root directory.

THANK YOU!!
