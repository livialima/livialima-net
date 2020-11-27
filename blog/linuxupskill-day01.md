 # Day 1 : Accessing your server

 This is part of the [#LinuxUpSkillChallenge](../challenges/linux-upskill.html). Don't forget to also check out the [Official Instructions](https://github.com/snori74/linuxupskillchallenge/blob/master/01.md) and the [Reddit](https://www.reddit.com/r/linuxupskillchallenge/) post.

 *video*

 ## Objectives of the day
 1. **Change your password** if your SSH connection is password-based. Use the command ```passwd```
 2. **More on using SSH**. There are two main methods to login remotely using SSH: password-based & passwordless. Prefer a passwordless connection if possible as it is more secure. Follow the tutorial on [SSH Basics](../howtos/basic-ssh.html) for more details.
 3. **Get to know your server** using some basic commands:

 ```uptime``` - returns information about how long your system has been running.

 ```uname -a``` - print detailed information about the machine name, Operating System and Kernel.

 ```free -h``` - gives information about used and unused memory usage and swap memory of a system.

 ```lscpu``` - returns the number of CPUs, threads, cores, sockets, and other CPU architecture information.

 ```top``` - provides a dynamic real-time view of the running system.

 ```htop``` - better and prettier option to ```top```

 ```df -h``` - show the amount of disk space that is free on file systems.

 ```lsblk``` - prints all block devices (except RAM disks).

 ```tree``` - prints the directory paths and files in each sub-directory in a tree-like format.

 ```du -h``` - provides a summary of harddisk or storage space disk usage.

 ```ncdu``` - better and prettier option to ```du```

 ```netstat -i``` - list out all the network connection in a system.

 ```ifconfig``` - list all network ports and IP addresses associated with them.

 ```ip addr``` - better option to ```ifconfig```, that is being deprecated.

 For more detail on how I did each day, check out my log on [Reddit](https://www.reddit.com/user/livia2lima). Follow me on [Twitter](https://twitter.com/search?q=%23LinuxUpSkillChallenge%20%40livialimatweets&src=typed_query&f=live) for daily updates.
