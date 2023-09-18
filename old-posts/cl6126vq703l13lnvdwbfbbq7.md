## How to setup and use SSH Server on Linux

Server side : Install OpenSSH
-----------------------------

**Debian / Ubuntu**: `sudo apt-get install openssh-server`

**RHEL / CentOS / Fedora**: `sudo dnf install openssh-server`

Server side : Enable/Start the SSH service
------------------------------------------

**SysVinit**: `sudo /etc/init.d/sshd start`

**SystemD**:
```
sudo systemctl enable sshd
sudo systemctl start sshd
```

If unsure of what which system manager your distro uses, try this:

```
pidof systemd && echo "systemd" || echo "sysvinit"
```

Client side : Install OpenSSH or other SSH client
-------------------------------------------------

OpenSSH client is commonly found already installed in most distros, but here are the steps in case it isn't. You can also use [Putty](https://blog.livialima.net/putty-basics) as it is very popular and user-friendly.

**Debian / Ubuntu**: `sudo apt-get install openssh-client`

**RHEL / CentOS / Fedora**: `sudo dnf install openssh-client`

Test it
-------

Try to login into the server using `ssh user@server-name`

Conclusion
----------

In this tutorial, you learned how to install the OpenSSH server application and how to connect to that using a SSH client.