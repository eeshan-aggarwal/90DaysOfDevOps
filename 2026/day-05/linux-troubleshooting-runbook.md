<h1>Day 5 task</h1>

root@ubuntu:/$ uname -a

Linux ubuntu 6.8.0-101-generic #101-Ubuntu SMP PREEMPT_DYNAMIC Mon Feb  9 10:15:05 UTC 2026 x86_64 x86_64 x86_64 GNU/Linux
root@ubuntu:/$ lsb_release -a
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 24.04.4 LTS
Release:        24.04
Codename:       noble

root@ubuntu:/$ cat /etc/os-release
PRETTY_NAME="Ubuntu 24.04.4 LTS"
NAME="Ubuntu"
VERSION_ID="24.04"
VERSION="24.04.4 LTS (Noble Numbat)"
VERSION_CODENAME=noble
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=noble
LOGO=ubuntu-logo

**Observation** - It show Linux OS flavour as Ubuntu and running on which version of kernel


root@ubuntu:~$ mkdir /tmp/runbook-demo
root@ubuntu:~$ cp /etc/hosts /tmp/runbook-demo/host-copy && ls -l /tmp/runbook-demo/
total 4
-rw-r--r-- 1 root root 255 Mar  6 06:51 host-copy

**Observation** - Folder created and file copied using cp command. Permission on file is writable.


root@ubuntu:~$ top
top - 06:56:23 up 24 min,  0 user,  load average: 0.00, 0.00, 0.00
Tasks: 121 total,   1 running, 120 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.3 sy,  0.3 ni, 99.3 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st 
MiB Mem :   1903.2 total,    560.1 free,    460.6 used,   1075.6 buff/cache     
MiB Swap:   1024.0 total,   1024.0 free,      0.0 used.   1442.7 avail Mem 

**Observation** - System is healthy and working as expected.

root@ubuntu:~$ ps -o pid,pcpu,pmem,comm -p 1185
    PID %CPU %MEM COMMAND
   1185  0.0  0.4 sshd

**Observation** - It shows the output of sshd of pid 1185 as the %CPU, %MEM.


root@ubuntu:~$ free -h
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       461Mi       559Mi       1.0Mi       1.1Gi       1.4Gi
Swap:          1.0Gi          0B       1.0Gi

**Observation** - It shows total available memory and how much used and available in swap as well.


root@ubuntu:~$ df -h
Filesystem      Size  Used Avail Use% Mounted on
tmpfs           191M  980K  190M   1% /run
/dev/vda1        19G  5.2G   14G  29% /
tmpfs           952M   84K  952M   1% /dev/shm
tmpfs           5.0M     0  5.0M   0% /run/lock
/dev/vda16      881M  117M  703M  15% /boot
/dev/vda15      105M  6.2M   99M   6% /boot/efi


**Observation** - It shows the plenty of space available on disk and can be used.


root@ubuntu:~$ du -sh /var/log
20M     /var/log

**Observation** - It show log directory size is small and not using much memory

root@ubuntu:~$ ss -tulpn | grep ssh
tcp   LISTEN 0      4096                              0.0.0.0:22         0.0.0.0:*    users:(("sshd",pid=1185,fd=3),("systemd",pid=1,fd=93))
tcp   LISTEN 0      4096                                 [::]:22            [::]:*    users:(("sshd",pid=1185,fd=4),("systemd",pid=1,fd=94))

**Observation** - It showing ssh is listening on port 22 and working as expected.

root@ubuntu:~$ journalctl -u ssh | tail -n 50 
Mar 04 09:05:56 ubuntu sudo[26245]: pam_unix(sudo:session): session closed for user root
Mar 04 09:05:56 ubuntu sudo[26247]:     root : PWD=/run/kc-internal ; USER=root ; COMMAND=/usr/bin/apt-get update
Mar 04 09:05:56 ubuntu sudo[26247]: pam_unix(sudo:session): session opened for user root(uid=0) by (uid=0)
Mar 04 09:05:57 ubuntu sudo[26247]: pam_unix(sudo:session): session closed for user root
Mar 04 09:05:57 ubuntu sudo[26510]:     root : PWD=/run/kc-internal ; USER=root ; COMMAND=/usr/bin/apt-get -y install podman
Mar 04 09:05:57 ubuntu sudo[26510]: pam_unix(sudo:session): session opened for user root(uid=0) by (uid=0)
Mar 04 09:06:02 ubuntu podman[26701]: 2026-03-04 09:06:02.968035456 +0000 UTC m=+0.152536086 system refresh
Mar 04 09:06:06 ubuntu sudo[26510]: pam_unix(sudo:session): session closed for user root
Mar 04 09:06:06 ubuntu sudo[27050]:     root : PWD=/run/kc-internal ; USER=root ; COMMAND=/usr/bin/tee /etc/containers/registries.conf
Mar 04 09:06:06 ubuntu sudo[27050]: pam_unix(sudo:session): session opened for user root(uid=0) by (uid=0)
Mar 04 09:06:06 ubuntu sudo[27050]: pam_unix(sudo:session): session closed for user root
Mar 04 09:06:41 ubuntu php8.3-common[28755]: php_invoke calendar: already enabled for PHP 8.3 cli sapi
Mar 04 09:06:41 ubuntu php8.3-common[28929]: php_invoke ctype: already enabled for PHP 8.3 cli sapi
Mar 04 09:06:41 ubuntu php8.3-common[29103]: php_invoke exif: already enabled for PHP 8.3 cli sapi
Mar 04 09:06:41 ubuntu php8.3-common[29277]: php_invoke fileinfo: already enabled for PHP 8.3 cli sapi
Mar 04 09:06:42 ubuntu php8.3-common[29451]: php_invoke ffi: already enabled for PHP 8.3 cli sapi
Mar 04 09:06:42 ubuntu php8.3-common[29625]: php_invoke ftp: already enabled for PHP 8.3 cli sapi
Mar 04 09:06:42 ubuntu php8.3-common[29799]: php_invoke gettext: already enabled for PHP 8.3 cli sapi
Mar 04 09:06:42 ubuntu php8.3-common[29973]: php_invoke iconv: already enabled for PHP 8.3 cli sapi
Mar 04 09:06:42 ubuntu php8.3-common[30147]: php_invoke pdo: already enabled for PHP 8.3 cli sapi
Mar 04 09:06:42 ubuntu php8.3-common[30321]: php_invoke phar: already enabled for PHP 8.3 cli sapi
Mar 04 09:06:43 ubuntu php8.3-common[30495]: php_invoke posix: already enabled for PHP 8.3 cli sapi
Mar 04 09:06:43 ubuntu php8.3-common[30843]: php_invoke sockets: already enabled for PHP 8.3 cli sapi
Mar 04 09:06:43 ubuntu php8.3-common[31017]: php_invoke sysvmsg: already enabled for PHP 8.3 cli sapi
Mar 04 09:06:43 ubuntu php8.3-common[31365]: php_invoke sysvshm: already enabled for PHP 8.3 cli sapi
Mar 04 09:06:44 ubuntu php8.3-readline[31714]: php_invoke readline: already enabled for PHP 8.3 cli sapi
Mar 04 09:06:44 ubuntu php8.3-opcache[31889]: php_invoke opcache: already enabled for PHP 8.3 cli sapi
Mar 04 09:06:44 ubuntu php8.3-cli[32031]: php_invoke sockets: already enabled for PHP 8.3 cli sapi
Mar 04 09:06:44 ubuntu php8.3-cli[32064]: php_invoke iconv: already enabled for PHP 8.3 cli sapi
Mar 04 09:06:44 ubuntu php8.3-cli[32196]: php_invoke phar: already enabled for PHP 8.3 cli sapi
Mar 04 09:06:44 ubuntu php8.3-cli[32229]: php_invoke shmop: already enabled for PHP 8.3 cli sapi
Mar 04 09:06:44 ubuntu php8.3-cli[32295]: php_invoke fileinfo: already enabled for PHP 8.3 cli sapi
Mar 04 09:06:44 ubuntu php8.3-cli[32328]: php_invoke tokenizer: already enabled for PHP 8.3 cli sapi
Mar 04 09:06:44 ubuntu php8.3-cli[32394]: php_invoke exif: already enabled for PHP 8.3 cli sapi
Mar 04 09:06:44 ubuntu php8.3-cli[32460]: php_invoke ftp: already enabled for PHP 8.3 cli sapi
Mar 04 09:06:44 ubuntu php8.3-cli[32493]: php_invoke pdo: already enabled for PHP 8.3 cli sapi
Mar 04 09:06:44 ubuntu php8.3-cli[32559]: php_invoke ffi: already enabled for PHP 8.3 cli sapi
Mar 04 09:06:44 ubuntu php8.3-cli[32592]: php_invoke posix: already enabled for PHP 8.3 cli sapi
Mar 04 09:06:44 ubuntu php8.3-cli[32625]: php_invoke readline: already enabled for PHP 8.3 cli sapi
-- Boot 118980360b1c455cb10181f20279594b --
Mar 06 06:31:53 ubuntu systemd[1]: Starting ssh.service - OpenBSD Secure Shell server...
Mar 06 06:31:53 ubuntu sshd[1185]: Server listening on 0.0.0.0 port 22.
Mar 06 06:31:53 ubuntu sshd[1185]: Server listening on :: port 22.
Mar 06 06:31:53 ubuntu systemd[1]: Started ssh.service - OpenBSD Secure Shell server.
Mar 06 06:31:53 ubuntu sshd[1186]: Accepted password for kc-internal from 10.244.5.15 port 51482 ssh2
Mar 06 06:31:54 ubuntu sshd[1189]: Accepted password for kc-internal from 10.244.5.15 port 51488 ssh2
Mar 06 06:32:18 ubuntu sshd[1576]: Accepted password for kc-internal from 10.244.5.15 port 52748 ssh2
Mar 06 06:40:37 ubuntu sshd[1625]: Accepted password for kc-internal from 10.244.5.107 port 51196 ssh2
Mar 06 06:40:37 ubuntu sshd[1628]: Accepted password for kc-internal from 10.244.5.107 port 51202 ssh2
Mar 06 06:40:37 ubuntu sshd[1631]: Accepted password for kc-internal from 10.244.5.107 port 51210 ssh2


**Observation**- showing last 50 lines of logs of ssh


<h2>What if situation worse</h2>

- You restart the service by using systemctl restart ssh
- Review logs and filter by grep or awk
