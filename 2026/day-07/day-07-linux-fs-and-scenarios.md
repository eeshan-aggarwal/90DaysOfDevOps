<h1>Day 07 Task</h1>

<b>Core directories:</b>
- /(root) - Its the main starting point of everything
- /home - It is the user home directories
- /root - Root user home directory
- /etc - It stores all the configuration files
- /var/log - It stores all the log files
- /tmp - stores the temporary files

<b>Additional Directories:</b>

- /bin - Essential command binaries
- /usr/bin - User command binaries
- /opt - optional apllications

<h2>Performing hands-on task</h2>

<img width="651" height="116" alt="image" src="https://github.com/user-attachments/assets/3ccc1233-bb3f-4778-a381-27d6b8022d95" />

- As command performed it shows /var/log/syslogs is the biggest with 196 Kb.

<img width="381" height="36" alt="image" src="https://github.com/user-attachments/assets/c1d8a23d-7b2f-4b7e-906b-55a1cb6ddf6f" />

- As command performed it shows the content of configuration file hostname in /etc.

<img width="452" height="163" alt="image" src="https://github.com/user-attachments/assets/ee6de96f-4d37-4ade-ae8d-28d22a79eeec" />

- It shows the content of home directory

<b>Part 2: Scenario-Based Practice</b>

Question: How do you check if the 'nginx' service is running?

Command to check - systemctl status nginx
If service not present - apt-get install ngnix


<b>Scenario 1: Service Not Starting</b>

A web application service called 'myapp' failed to start after a server reboot.
What commands would you run to diagnose the issue?
Write at least 4 commands in order.

Step 1: systemctl status myapp
Why: show the current status of the application

Step 2: systemctl is-enabled myapp 
Why: Check whether service is enabled or disabled

Step 3: systemctl start myapp
Why: If service is stopped, this command will start the service

Step 4: journalctl -u app -n 50
Why: To check the logs of the application with last 50 lines

<b>Scenario 2: High CPU Usage</b>

Your manager reports that the application server is slow.
You SSH into the server. What commands would you run to identify
which process is using high CPU?

Step 1: top 
Why: Show the process using high CPU and it refreshes every second.

Step 2: ps aux --sort=-%cpu| head -n 10
Why: Show the process using high CPU but not refresh every second

Step 3: htop
Why: Same as top, just better and colorful interface.



<b>Scenario 3: Finding Service Logs</b>

A developer asks: "Where are the logs for the 'docker' service?"
The service is managed by systemd.
What commands would you use?

Step 1: systemctl status docker
why: check status of docker

Step 2: journalctl -u docker -n 50 
why: show the logs of docker with last 50 lines

Step 3: journalctl -u docker -f
why: show the logs of docker with live updates

<b>Scenario 4: File Permissions Issue</b>

A script at /home/user/backup.sh is not executing.
When you run it: ./backup.sh
You get: "Permission denied"

What commands would you use to fix this?

Step 1: ls -lrt /home/user/backup.sh
Why: show the permissions on file

Step 2: chmod 777 /home/user/backup.sh
Why: Added read, write and execute permission

