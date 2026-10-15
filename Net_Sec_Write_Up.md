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

!image.png

**Answer : 10121**

---

> Challenge 3
> 

How many TCP ports are open?

with the first challenge output, we can see all the open ports are tcp

!image.png

**Answer : 7**

---

> Challenge 4
> 

On port 80, what is the service version value?

By using the option -sV, we can get the version details of the service running on the port

!image.png

**Answer : THM{MySpecialServer007}**

---

> Challenge 5
> 

What is the flag hidden in the SSH server header?

By using the —script banner we can easily get the server header details 

!image.png

we can also use `nmap -sV <ip> -p 22` to get the server header details

**Answer : thm{946219583339}**

---

> Challenge 6
> 

We have an FTP server listening on a nonstandard port. What is the version of the FTP server?

when we scanned for all the open ports we found a unknown service running on the port 10121, when we tried to enumerate that open port more by -sV, we get the version result of the ftp 

!image.png

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

!image.png

!image.png

| login | password |
| --- | --- |
| eddie | softball |
| quinn | cookie |

with this credentials, we can login to ftp to get the flag

**login 2 : quinn**

eddie user have no files, quinn have file 

!image.png

when we get the ftp_flag.txt and opened the file, we get the answer

**Answer : THM{QUINN_IS_BACK007}**

---

> Challenge 8
> 

Browsing to `http://10.49.163.247:8081` displays a small challenge that will give you a flag once you solve it. What is the flag?

when we opened the website, we get the page

!image.png

so we need to scan the host without IDS detecting us, so we need to do a stealthy scan, after trying multiple options we get to the option

```python
nmap -sN <ip>
```

-sN : this option send the TCP request, without any flag set, so IDS doesn’t track this packet.

!image.png

**Answer : THM{NMAP_CHAMPION001}**

**Answer : 8081**

---

> challenge 2
> 

There is an open port outside the common 1000 ports; it is above 10,100. What is it?

using the first challenge output we can easily find the answer 

![image.png](Net%20Sec/image%201.png)

**Answer : 10121**

---

> Challenge 3
> 

How many TCP ports are open?

with the first challenge output, we can see all the open ports are tcp

![image.png](Net%20Sec/image%202.png)

**Answer : 7**

---

> Challenge 4
> 

On port 80, what is the service version value?

By using the option -sV, we can get the version details of the service running on the port

![image.png](Net%20Sec/image%203.png)

**Answer : THM{MySpecialServer007}**

---

> Challenge 5
> 

What is the flag hidden in the SSH server header?

By using the —script banner we can easily get the server header details 

![image.png](Net%20Sec/image%204.png)

we can also use `nmap -sV <ip> -p 22` to get the server header details

**Answer : thm{946219583339}**

---

> Challenge 6
> 

We have an FTP server listening on a nonstandard port. What is the version of the FTP server?

when we scanned for all the open ports we found a unknown service running on the port 10121, when we tried to enumerate that open port more by -sV, we get the version result of the ftp 

![image.png](Net%20Sec/image%205.png)

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

![image.png](Net%20Sec/image%206.png)

![image.png](Net%20Sec/image%207.png)

| login | password |
| --- | --- |
| eddie | softball |
| quinn | cookie |

with this credentials, we can login to ftp to get the flag

**login 2 : quinn**

eddie user have no files, quinn have file 

![image.png](Net%20Sec/image%208.png)

when we get the ftp_flag.txt and opened the file, we get the answer

**Answer : THM{QUINN_IS_BACK007}**

---

> Challenge 8
> 

Browsing to `http://10.49.163.247:8081` displays a small challenge that will give you a flag once you solve it. What is the flag?

when we opened the website, we get the page

![image.png](Net%20Sec/image%209.png)

so we need to scan the host without IDS detecting us, so we need to do a stealthy scan, after trying multiple options we get to the option

```python
nmap -sN <ip>
```

-sN : this option send the TCP request, without any flag set, so IDS doesn’t track this packet.

![image.png](Net%20Sec/image%2010.png)

**Answer : THM{NMAP_CHAMPION001}**
