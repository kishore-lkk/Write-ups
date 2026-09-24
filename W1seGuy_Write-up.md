# **W1seGuy Write-up**

Woah!!!, this definitely didn’t go as planned. Well this is my first challenge in THM and oh boy, I learned a shit ton of things while solving this box. 

This box has 2 task, 

### Task 1:

In task one, we were given the source code, By analyzing the source code we would be able to understand, that the code, first setup a local server and generate a random 5 - char key for performing XOR encryption, the source code also have the plain-text that is used for XOR encryption.

---

### Task 2:

In task 2 - we need 2 flags to solve the task

We are given VM machine, and told the server is listening on port 1337, which is same as the source code, so we might able to understand that the source code is running on this VM. 

when we connect to the server, we recieve a XORed encoded text

<img width="829" height="67" alt="image" src="https://github.com/user-attachments/assets/2820dd87-8570-4e18-8e95-9dd21cb17395" />

the task is to find the encryption key used.

In XOR, 

<img width="1374" height="874" alt="image" src="https://github.com/user-attachments/assets/096a16e4-71aa-4b6c-9f59-67895c6a3ffb" />

so Plain-Text ⊕ Key → Cipher-Text. We can reverse engineer this by Plain-Text ⊕ Cipher-Text → key to find the key used in the encryption. 

In the task, we were given the Cipher-Text, which is output of XOR and encoded in hex, Here we use cyberchef to decode the data into bytes and do the reverse XOR encryption to find the key :

But to do the reverse XOR we need to know the plaintext (No, the plain text present in the source_code.py is not used), We know that all the THM flags are in `THM{flag}` format, by this we might able to understand the plaintext should have the `“THM{”`[data]`”}"` characters. so, we take the first 4 bytes from the cipher text(which should be `“THM{”`) and do the reverse XOR encryption

<img width="782" height="672" alt="image" src="https://github.com/user-attachments/assets/c4459f99-e394-4f3f-9783-b94eb2690f75" />

we get `EBeb` - the first characters of key, but in the source code, it is mentioned that the key is in 5 characters, so we need to brute force to find the last character

If we measure the cipher text - that is in the length of 40, which means the 5th character of key must be used to encrypt the last character of the plain text which is `“}”`
so we the cyber-chef inbuilt brute force technique to decode the last character of cipher text `“09”` .

so we need to find "key" in this operation: 09 ⊕ key → }

<img width="788" height="894" alt="image" src="https://github.com/user-attachments/assets/377d1f3e-f9d6-4b3c-aaeb-87adccecb709" />

the key is 74(hex), if convert the hex into Unicode we get - “t”

<img width="774" height="656" alt="image" src="https://github.com/user-attachments/assets/4fad255a-d2a8-4f65-8ce2-314ad1ab462d" />

so the complete 5 character key is - `EBebt`, we use this to decrypt the cipher text 

#### Flag_1 :

we need to decrypt the complete cipher text we got from the server.

<img width="786" height="814" alt="image" src="https://github.com/user-attachments/assets/3a9cff67-9991-4343-aa88-6cd03e372478" />

this decrypted string is the answer for flag 1

<img width="932" height="166" alt="image" src="https://github.com/user-attachments/assets/1825b5d5-552e-4bc9-830f-417846d9afbe" />

#### Flag_2 :

by sending this encryption key to the server we get the flag_2 answer,

<img width="882" height="116" alt="image" src="https://github.com/user-attachments/assets/c6104d97-a818-4fef-8fdf-0ab47f73b744" />

<img width="902" height="117" alt="image" src="https://github.com/user-attachments/assets/f2a53d2e-528f-4fb1-88b8-0ef559087243" />

By this, we can close the challenge.

quality of update - No, you can’t reuse my key, as the key is randomly generated. so we have find the key uniquely. 

Thank you so much and keep hacking !!!

By,
Kishore.
