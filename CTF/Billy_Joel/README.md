<h1>BILLY JOEL'S BLOG - TRYHACKME</h1>

Started with our usual NMAP scan on target to identify opened ports
![Port scanning](https://user-images.githubusercontent.com/105601553/214822639-9605abd6-7fe6-491c-82be-672f6cf8322a.png)

Discovered four opened ports...22,80,139 and 445

I accessed the SMB port to see if I could find interesting files.
Fortunately, I found these files but it was a rabbit hole.
![SMB files](https://user-images.githubusercontent.com/105601553/214823135-6e82de6b-c25f-42a3-9f65-448af223cc19.png)

Checked the web server and it was Billy's blog
![Webpage](https://user-images.githubusercontent.com/105601553/214823609-85ca3d24-99e1-4c70-a5c6-fb99706358b3.png)

<b>NOTE:</b> You need to add <i>blog.thm and the target ip</i> to /etc/hosts

There wasn't anything interesting either on the blog.
Used Gobuster to find sub-domains. And fortunately, I found a login page.
![login](https://user-images.githubusercontent.com/105601553/217844408-3d343bc2-1b12-4ade-9dc6-59eca28aaac1.png)

Enumerated the blog using 'wpscan', and fortunately, I found usernames. Brute forced the password for the usernames and got a result
![password found](https://user-images.githubusercontent.com/105601553/218425621-6a0a1074-5372-4d96-b3c5-9932d4e9f45c.png)

Went back to the login page and logged in successfully with the credentials I found...
![Logged into Dashboard](https://user-images.githubusercontent.com/105601553/218425761-ad602388-03e4-4147-9165-0001d763f6cd.png)

I looked for a way to upload a script to get a reverse shell. But unfortunately, I didn't find a way to do so.
Although, I discovered that all the images in the Media Section were broken. Did a quick CVE search, and I found <a href="https://www.cvedetails.com/cve/CVE-2019-8942/">this</a> page. 

There's a module in Metasploit that we can use to exploit this vulnerability.
So I fired up Metasploit, searched for the exploit 'wp_crop_rce'. Loaded the exploit (exploit/multi/http/wp_crop_rce)
![found payload](https://user-images.githubusercontent.com/105601553/218428338-a030f971-a9e5-4098-bd66-b283d44b1261.png)

Set the required options
![set options](https://user-images.githubusercontent.com/105601553/218428560-79e9616b-29c9-4a49-9794-5c78a32f0221.png)

Executed the exploit, and I got a Meterpreter session.
![meterpreter session opened](https://user-images.githubusercontent.com/105601553/218428827-e607c156-45fa-4b84-96a6-af162ea0fd69.png)

And successfully logged in as www-data.
Was unable to get the users flag, so next thing was to escalate privileges before getting the flags.
Since we aren't allowed to run any commands as sudo, I checked the root SUID bits.
![finding suid bits of root user](https://user-images.githubusercontent.com/105601553/218429873-c7b6c52d-f359-43b4-9225-708bb524a97f.png)

Checked the file, and what the file does is search for 'admin' in env variable. If 'admin' is found, we get a shell with UID 0 and if 'admin' is not found. It displays the output 'Not an Admin'. Next thing was to export 'admin' as environment variable.
![created admin env variable](https://user-images.githubusercontent.com/105601553/218430796-3439601b-1a4d-4a2b-850a-1ff1f5b66a58.png)

Then execute the checker file to get a root shell...
![got root](https://user-images.githubusercontent.com/105601553/218431031-872d1298-f2fc-4c02-9264-0c3ddfe4afe7.png)

Find the flags, and you're done...






