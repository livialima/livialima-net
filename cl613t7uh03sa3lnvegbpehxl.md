## How to setup GNS3 on a remote server

%[https://youtu.be/JZQOX3Bj9dY]

Step Zero : Requirements
------------------------

*   An [AWS account](https://aws.amazon.com/getting-started/)
*   A local [GNS3](https://docs.gns3.com/docs/) installation
*   A local [OpenVPN](https://openvpn.net/) installation
*   A SSH client of your choice

DISCLAIMER: I've made this tutorial using linux.

Step 1 : Launch an EC2 instance
-------------------------------

**Launch a Linux instance:**
- Navigate to EC2 in the AWS Console.
- Click **Launch Instance**.
- Select a free-tier eligible **Ubuntu** image.
- Click **Next** - leave the **Instance Type** panel as is.
- Click **Next** - leave the **Instance Details** panel as is.
- Click **Next** - leave the **Storage** panel as is.
- Click **Add Tag**. Set key to **Name** and value to the name you choose to your instance. (Optional step)
- Click **Next**.

![aws-ec2-create-instance.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658774908413/VahIQFrAY.png align="left")

**Create a Security Group:**
- Assign a security group: **Create a new security group**
- Set the security group name and description as you choose.
- SSH connection for admin
- Type: **SSH**
- Protocol: **TCP**
- Port Range: **22**
- Source: **My IP**
- Description: (optional)
- OpenVPN connection port
- Type: **Custom UDP**
- Protocol: **UDP**
- Port Range: **1194**
- Source: **My IP**
- Description: (optional)
- Port to serve VPN config file
- Type: **Custom TCP**
- Protocol: **TCP**
- Port Range: **8003**
- Source: **My IP**
- Description: (optional)
- Click **Review and Launch**.
- Click **Launch**.

![aws-ec2-sg-gns3.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658774875943/yWR0Uq_V_.png align="left")

**Create a Key Pair:**
- Select: **Create a new key pair**
- Set the key pair name as you choose.
- Click **Download Key Pair**
- Click **Launch Instances**

![aws-ec2-keypair.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658774862458/u2faHg8Ut.png align="left")

**Connect to instance:**
- Back to EC2 Instances panel in the AWS Console.
- Select the instance.
- Click **Connect**.
- Connection method: **A standalone SSH client**
- Change the keypair file permissions to **Only Owner Read/Write** as follows: 

`chmod 400 my-key-pair.pem`

Or, if you are using Windows:
- \[File\] Properties - Security - Advanced
-  Set Owner to the key's user
-  Remove all users, groups, and services, except for the key's user, under Permission Entries
-  Set key's user to Full Control

At the SSH client of your choice, input the details provided.
- User name **ubuntu**
- Target: **Public DNS**

Example:

```
ssh -i my-key-pair.pem ubuntu@server-public-dns
```

![aws-ec2-connect-ssh.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658774808017/w1iQ61MWi.png align="left")

Step 2 : Install OpenVPN and GNS3 on the instance
-------------------------------------------------

**Download/Install GNS3:**
- Inside the server: `sudo su`
- Install the GNS3 as instructed by the [Installation Guide](https://docs.gns3.com/docs/getting-started/installation/remote-server/)

```
cd /tmp
curl https://raw.githubusercontent.com/GNS3/gns3-server/master/scripts/remote-install.sh > gns3-remote-install.sh
bash gns3-remote-install.sh --with-openvpn --with-iou --with-i386-repository
```

- Restart the server for the installation to take effect: `reboot now`

Step 3 : Config your OpenVPN client and open the VPN tunnel
-----------------------------------------------------------

**Config OpenVPN client:**

SSH back to the server, copy and **download** the config file provided by the OpenVPN server to your local machine.

![openvpn-client.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658774743767/oLCUZthv3.png align="left")

**Run OpenVPN client:**

At your local machine, **run OpenVPN client** using the file dowloaded:

```
sudo openvpn config-file.ovpn
```

Step 5 : Config your GNS3 client
--------------------------------

Find the tunnel IP address; at the server: 

```
ip addr | grep tun
```

- **ip addr** list all the IP addresses.
- **grep tun** filters the result of 'ip addr' and shows only the records with 'tun' (as in tunnel) in it.

![ubuntu-ip-addr-tunnel.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658774643349/GSsI0zitF.png align="left")

**Config remote main server:**
- Open your local GNS3 client.
- Click **Edit**; **Preferences**; **Server**
- Uncheck "Enable local server"
- Host: **the tunnel IP address**
- Port: **3080**

![gns3-server-pref.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658774625805/UDhRGs-Lp.png align="left")

Step 6 : Enjoy!
---------------

Now you have the GNS3 installed and ready to go!

![gns3-client.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658774607066/Od8XnuOAT.png align="left")

Step 7 : But before you go... save your work!(and some money)
-------------------------------------------------------------

Don't leave your instance running without any purpose. Save your instance (all configured and tweaked) to use it whenever you're up to lab again.

**Create an AMI:**
- Back to EC2 Instances panel in the AWS Console.
- Select the instance.
- Click **Actions**; **Image**; **Create Image**

Your AMIs will be available on the EC2 Images panel in the AWS Console.

![aws-ec2-ami.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658774586953/2eAmPCaFY.png align="left")

**Don't forget to terminate your instance!**
- Back to EC2 Instances panel in the AWS Console.
- Select the instance.
- Click **Actions**; **Instance State**; **Terminate**
- Click **Yes, Terminate**