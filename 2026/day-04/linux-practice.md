You will create a short practice note by actually running basic commands and capturing what you see:

Check running processes
Inspect one systemd service
Capture a small troubleshooting flow

root@ubuntu:/$ ps aux | head
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  1.0  0.6  22108 13296 ?        Ss   11:44   0:03 /sbin/init
root           2  0.0  0.0      0     0 ?        S    11:44   0:00 [kthreadd]
root           3  0.0  0.0      0     0 ?        S    11:44   0:00 [pool_workqueue_release]
root           4  0.0  0.0      0     0 ?        I<   11:44   0:00 [kworker/R-rcu_g]
root           5  0.0  0.0      0     0 ?        I<   11:44   0:00 [kworker/R-rcu_p]
root           6  0.0  0.0      0     0 ?        I<   11:44   0:00 [kworker/R-slub_]
root           7  0.0  0.0      0     0 ?        I<   11:44   0:00 [kworker/R-netns]
root           8  0.0  0.0      0     0 ?        I    11:44   0:00 [kworker/0:0-cgroup_destroy]
root           9  0.0  0.0      0     0 ?        I<   11:44   0:00 [kworker/0:0H-kblockd]


What I learned:

ps aux shows all running processes.

Useful to check which services/processes are running.


root@ubuntu:/$ top

top - 11:53:05 up 8 min,  0 user,  load average: 0.00, 0.09, 0.08
Tasks: 120 total,   1 running, 119 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st 
MiB Mem :   1903.3 total,    891.4 free,    371.7 used,    807.2 buff/cache     
MiB Swap:   1024.0 total,   1024.0 free,      0.0 used.   1531.5 avail Mem 

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND                                                                                                             
      1 root      20   0   22108  13296   9524 S   0.0   0.7   0:03.74 systemd                                                                                                             
      2 root      20   0       0      0      0 S   0.0   0.0   0:00.00 kthreadd                                                                                                            
      3 root      20   0       0      0      0 S   0.0   0.0   0:00.00 pool_workqueue_release                                                                                              
      4 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-rcu_g                                                                                                     
      5 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-rcu_p                                                                                                     
      6 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/

What I learned:

top shows CPU usage, memory usage, and running processes in real time.



SSH Service check

root@ubuntu:/$ systemctl status ssh
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; disabled; preset: enabled)
     Active: active (running) since Thu 2026-03-05 11:44:46 UTC; 10min ago
TriggeredBy: ● ssh.socket
       Docs: man:sshd(8)
             man:sshd_config(5)
    Process: 1174 ExecStartPre=/usr/sbin/sshd -t (code=exited, status=0/SUCCESS)
   Main PID: 1176 (sshd)
      Tasks: 25 (limit: 2237)
     Memory: 552.7M (peak: 729.9M)
        CPU: 23.698s
     CGroup: /system.slice/ssh.service
             ├─1176 "sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups"
             ├─1198 /bin/runtime-scenario-service
             ├─1208 /opt/theia/node /opt/theia/browser-app/src-gen/backend/main.js /root --hostname=0.0.0.0 --port 40205
             ├─1245 /bin/runtime-info-service
             ├─1256 bash -c "while true; do /bin/kc-terminal -p 40200 --writable -t disableLeaveAlert=true bash; done"
             ├─1257 /bin/kc-terminal -p 40200 --writable -t disableLeaveAlert true bash
             ├─1642 bash
             ├─1656 systemctl status ssh
             └─1657 less

Mar 05 11:44:46 ubuntu systemd[1]: Starting ssh.service - OpenBSD Secure Shell server...
Mar 05 11:44:46 ubuntu sshd[1176]: Server listening on 0.0.0.0 port 22.
Mar 05 11:44:46 ubuntu sshd[1176]: Server listening on :: port 22.
Mar 05 11:44:46 ubuntu systemd[1]: Started ssh.service - OpenBSD Secure Shell server.
Mar 05 11:44:46 ubuntu sshd[1177]: Accepted password for kc-internal from 10.244.3.114 port 48986 ssh2
Mar 05 11:44:47 ubuntu sshd[1180]: Accepted password for kc-internal from 10.244.3.114 port 48998 ssh2
Mar 05 11:45:16 ubuntu sshd[1573]: Accepted password for kc-internal from 10.244.3.114 port 47358 ssh2
Mar 05 11:46:27 ubuntu sshd[1576]: Accepted password for kc-internal from 10.244.5.176 port 36114 ssh2
Mar 05 11:46:28 ubuntu sshd[1579]: Accepted password for kc-internal from 10.244.5.176 port 36128 ssh2
Mar 05 11:46:28 ubuntu sshd[1582]: Accepted password for kc-internal from 10.244.5.176 port 36130 ssh2




root@ubuntu:/$ systemctl list-units --type=service | head
  UNIT                                           LOAD   ACTIVE SUB     DESCRIPTION
  apparmor.service                               loaded active exited  Load AppArmor profiles
  apport.service                                 loaded active exited  automatic crash report generation
  blk-availability.service                       loaded active exited  Availability of block devices
  console-setup.service                          loaded active exited  Set console font and keymap
  containerd.service                             loaded active running containerd container runtime
  cron.service                                   loaded active running Regular background program processing daemon
  dbus.service                                   loaded active running D-Bus System Message Bus
  docker.service                                 loaded active running Docker Application Container Engine
  finalrd.service                                loaded active exited  Create final runtime dir for shutdown pivot root


  Above command will list all active running service


  Use of Journalctl 

  root@ubuntu:/$ journalctl -u ssh | tail
Mar 05 11:44:46 ubuntu systemd[1]: Starting ssh.service - OpenBSD Secure Shell server...
Mar 05 11:44:46 ubuntu sshd[1176]: Server listening on 0.0.0.0 port 22.
Mar 05 11:44:46 ubuntu sshd[1176]: Server listening on :: port 22.
Mar 05 11:44:46 ubuntu systemd[1]: Started ssh.service - OpenBSD Secure Shell server.
Mar 05 11:44:46 ubuntu sshd[1177]: Accepted password for kc-internal from 10.244.3.114 port 48986 ssh2
Mar 05 11:44:47 ubuntu sshd[1180]: Accepted password for kc-internal from 10.244.3.114 port 48998 ssh2
Mar 05 11:45:16 ubuntu sshd[1573]: Accepted password for kc-internal from 10.244.3.114 port 47358 ssh2
Mar 05 11:46:27 ubuntu sshd[1576]: Accepted password for kc-internal from 10.244.5.176 port 36114 ssh2
Mar 05 11:46:28 ubuntu sshd[1579]: Accepted password for kc-internal from 10.244.5.176 port 36128 ssh2
Mar 05 11:46:28 ubuntu sshd[1582]: Accepted password for kc-internal from 10.244.5.176 port 36130 ssh2



Inspect and restarted ssh service

root@ubuntu:/$ ps -ef | grep ssh
root        1176       1  0 11:44 ?        00:00:00 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups
root        1667    1642  0 11:59 pts/0    00:00:00 grep --color=auto ssh
root@ubuntu:/$ systemctl restart ssh
root@ubuntu:/$ systemctl status ssh
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; disabled; preset: enabled)
     Active: active (running) since Thu 2026-03-05 12:00:25 UTC; 12s ago
TriggeredBy: ● ssh.socket
       Docs: man:sshd(8)
             man:sshd_config(5)
    Process: 1674 ExecStartPre=/usr/sbin/sshd -t (code=exited, status=0/SUCCESS)
   Main PID: 1676 (sshd)
      Tasks: 25 (limit: 2237)
     Memory: 555.4M (peak: 729.9M)
        CPU: 142ms
     CGroup: /system.slice/ssh.service
             ├─1198 /bin/runtime-scenario-service
             ├─1208 /opt/theia/node /opt/theia/browser-app/src-gen/backend/main.js /root --hostname=0.0.0.0 --port 40205
             ├─1245 /bin/runtime-info-service
             ├─1256 bash -c "while true; do /bin/kc-terminal -p 40200 --writable -t disableLeaveAlert=true bash; done"
             ├─1257 /bin/kc-terminal -p 40200 --writable -t disableLeaveAlert true bash
             ├─1642 bash
             ├─1676 "sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups"
             ├─1677 systemctl status ssh
             └─1678 less

Mar 05 12:00:25 ubuntu systemd[1]: ssh.service: This usually indicates unclean termination of a previous run, or service implementation deficiencies.
Mar 05 12:00:25 ubuntu systemd[1]: ssh.service: Found left-over process 1642 (bash) in control group while starting unit. Ignoring.
Mar 05 12:00:25 ubuntu systemd[1]: ssh.service: This usually indicates unclean termination of a previous run, or service implementation deficiencies.
Mar 05 12:00:25 ubuntu systemd[1]: ssh.service: Found left-over process 1671 (systemctl) in control group while starting unit. Ignoring.
Mar 05 12:00:25 ubuntu systemd[1]: ssh.service: This usually indicates unclean termination of a previous run, or service implementation deficiencies.
Mar 05 12:00:25 ubuntu systemd[1]: ssh.service: Found left-over process 1672 (systemd-tty-ask) in control group while starting unit. Ignoring.
Mar 05 12:00:25 ubuntu systemd[1]: ssh.service: This usually indicates unclean termination of a previous run, or service implementation deficiencies.
Mar 05 12:00:25 ubuntu sshd[1676]: Server listening on 0.0.0.0 port 22.
Mar 05 12:00:25 ubuntu sshd[1676]: Server listening on :: port 22.
Mar 05 12:00:25 ubuntu systemd[1]: Started ssh.service - OpenBSD Secure Shell server.