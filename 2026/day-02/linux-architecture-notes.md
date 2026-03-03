- The core components of Linux (kernel, user space, init/systemd)

Core Components of Linux are:

 Kernel: Its the heart of linux, which is responsible for CPU scheduling, Memory management, Devices, Filesystems, Networking.
 UserSpace: Its the space where normal program runs. It includes shell(bash), applications, system utilities. It communicates 
            with kernel using system calls
 init/systemd: Its the first process started by kernel and having the PID as 1. Responsible for staring services, handling 
               shutdown and reboot.


- How processes are created and managed

A process is creatred using fork()
Child process may run new program using exec()
Every process has:
PID (Process ID)
PPID (Parent PID)

As coming to Process states:
- Running (R) --> Curently executing 
- Sleeping (S) --> Waiting for event
- Stopped (T) --> Paused
- Zombie (Z) --> Finished but not cleaned by parent
- Idle/Uninterruptible Sleep (D) --> Waiting for I/O



- What systemd Does & Why It Matters ?
Systemd is the init system (PID 1) that starts, stops and manages system services and background processes during boot and runtime.


- 5 Linux Commands used daily

ps -ef --> check running process 
top / htop --> Monitor CPU and memory
systemctl status --> check services health
grep --> filter the output with specific keyword
chmod --> Change the permission of the files
