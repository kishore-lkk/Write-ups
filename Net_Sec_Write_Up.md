# Net Sec Challenge

whoaaa!!!, This challenge took me lot of time than I expected.

This challenge mainly revolves around nmap. let see how I solved the problems

> Challenge 1
> 

What is the highest port number that is open and less than 10,000?

I ran

```python
nmap -p- <ip>
```

which gave all the open ports, from that we could get the answer easily 

<img width="801" height="332" alt="image 1" src="https://github.com/user-attachments/assets/13321e3b-8287-4ab7-880e-a8a821b60f7a" />


**Answer : 8081**

---

> challenge 2
> 

There is an open port outside the common 1000 ports; it is above 10,100. What is it?

using the first challenge output we can easily find the answer 

<img width="801" height="332" alt="image 1" src="https://github.com/user-attachments/assets/9f78deb3-e128-4a39-8835-bbb05b356225" />


**Answer : 10121**

---

> Challenge 3
> 

How many TCP ports are open?

with the first challenge output, we can see all the open ports are tcp

<img width="801" height="332" alt="image 2" src="https://github.com/user-attachments/assets/0ada0312-4cd7-483e-b3f8-ec11cf9c8067" />



**Answer : 7**

---

> Challenge 4
> 

On port 80, what is the service version value?

By using the option -sV, we can get the version details of the service running on the port

<img width="855" height="403" alt="image 3" src="https://github.com/user-attachments/assets/d0be425a-123d-4c15-9bbb-d18240f05639" />



**Answer : THM{MySpecialServer007}**

---

> Challenge 5
> 

What is the flag hidden in the SSH server header?

By using the —script banner we can easily get the server header details 

<img width="790" height="233" alt="image 4" src="https://github.com/user-attachments/assets/6cb9951a-1e60-4353-afeb-9c34eb17f509" />



we can also use `nmap -sV <ip> -p 22` to get the server header details

**Answer : thm{946219583339}**

---

> Challenge 6
> 

We have an FTP server listening on a nonstandard port. What is the version of the FTP server?

when we scanned for all the open ports we found a unknown service running on the port 10121, when we tried to enumerate that open port more by -sV, we get the version result of the ftp 

<img width="855" height="629" alt="image 5" src="https://github.com/user-attachments/assets/023b25c8-43f3-4ff9-a87a-1cafeeb8d557" />



**Answer : vsftpd 3.0.5**

---

> Challenge 7
> 

We learned two usernames using social engineering: **eddie** and **quinn**. What is the flag hidden in one of these two account files and accessible via FTP?

we know that ftp is on port 10121, we know there are 2 user and we have the username, we need to brute-force to get the password, 

we can use hydra to brute-force,

```python
hydra -l <login> -P /usr/share/wordlists/rockyou.txt -s 10121 ftp://10.49.163.247
```

<img width="816" height="471" alt="image 6" src="https://github.com/user-attachments/assets/d5b036d2-6b6c-4939-a7ce-c89eb1d878bc" />


<img width="824" height="478" alt="image 7" src="https://github.com/user-attachments/assets/346cfca4-46fe-430c-b837-93e85d862c9e" />



| login | password |
| --- | --- |
| eddie | softball |
| quinn | cookie |

with this credentials, we can login to ftp to get the flag

**login 2 : quinn**

eddie user have no files, quinn have file 

<img width="864" height="587" alt="image 8" src="https://github.com/user-attachments/assets/3f685ead-2cff-4dc9-9562-50f5e0c76ad6" />


when we get the ftp_flag.txt and opened the file, we get the answer

**Answer : THM{QUINN_IS_BACK007}**

---

> Challenge 8
> 

Browsing to `http://10.49.163.247:8081` displays a small challenge that will give you a flag once you solve it. What is the flag?

when we opened the website, we get the page

<img width="633" height="554" alt="image 9" src="https://github.com/user-attachments/assets/1e1c9467-7592-4bcd-ac94-ec2c0148727f" />


so we need to scan the host without IDS detecting us, so we need to do a stealthy scan, after trying multiple options we get to the option

```python
nmap -sN <ip>
```

-sN : this option send the TCP request, without any flag set, so IDS doesn’t track this packet.

<img width="941" height="868" alt="image 10" src="https://github.com/user-attachments/assets/3543170c-28ac-46b3-ac15-c839e97680ac" />


**Answer : THM{NMAP_CHAMPION001}**

**Answer : 8081**

---
