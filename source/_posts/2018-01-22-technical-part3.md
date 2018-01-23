---
layout: blog
title: CS Fundamental(part3 network)
date: 2018-01-22 13:22:25
tags:
- interview
- technical
- faq
- network
---

# Technical Questions

## What is FTP? How is it different from Secure FTP?
### A short answer:
>FTP in its basic form is not secure, while FTP/S (File Transfer Protocol over Secure Socket Layers) or the SFTP(Secure File Transfer Protocol) allows you to have a more secured port(s), but slows down the speed.
<!--more-->

### A long answer:
>**FTP** is developed in the 70s to allow two machines to transfer data over the internet. One act as the server and another as the client to send information back and forth. THe FTP protocol generally uses port 21 means the FTP server will listen for client connection on port 21.

>Once handshake is established(connected), the main connection is called the **Control Connection**. The client will usually authenticate itself with the server by sending username/password, afterward the Control Connection issues command to negotiate a new port called the **Data Connection** which files will be transfer through.

>The **Control Connection** remains idle until the end, when the port reports the file transfer is completed or failed. The data transferred in between client and server are unhashed plain text, and as you can imagine it is very unsecure. A Man-In-the-Middle-Attacker(MITMA) can find their way easily to steal the information.

>You could however use the One Time Password(OTP) protocol to generate hashed unique password for one time used, making harder for MITMA to generate the password

>The need for a data connection is the main drawback of FTP.

>>**FTP/S**

>FTP stands for FTP over SSL, allows for the encreption of both the Control and Data connections either concurrently or independently.
Benefit is that if we are doing FTP over TLS(2048 bit or 1024 bit) it can be time consuming since SSL handshake need to happen twice per connection, one for the Data Connection and one for the Control Connection.

>FTP/S is most commonly on port 990 versus 21, still it is able to est connection on port 21 but the client would have to Explicittly state tehri intention by sending an AUTH
SSL or AUTH TLS command to the serer in order to use SSL for security.

>**SFTP**
>SFTP stands for Secure File Transfer Protocol, a relatively new protocol allowing the transfer of data over a SSH secured channel or connection.
Difference being SFTP is packet-based instead of text-based, and also SFTP transfers are being done over the main Control Connection versus using the Data Connection to transfer data.
SFTP is secured since it runs over SSH, meaning the encreption cannot be triggered or turned off using any AUTH command
Also, SFTP contains much more details about the files such as the permissions, data, time, size, etc.


