## How to setup Cisco Packet Tracer on a remote server

%[https://youtu.be/JZQOX3Bj9dY]

Step Zero : Requirements
------------------------

*   An [AWS account](https://aws.amazon.com/getting-started/)
*   A Cisco [Network Academy](http://netacad.com) account
*   A RDP client of your choice

Step 1 : Launch an EC2 instance
-------------------------------

**Launch a Windows instance:**
- Navigate to EC2 in the AWS Console.
- Click **Launch Instance**.
- Select a free-tier eligible **Windows** image.
- Click **Next** - leave the **Instance Type** panel as is.
- Click **Next** - leave the **Instance Details** panel as is.
- Click **Next** - leave the **Storage** panel as is.
- Click **Add Tag**. Set key to **Name** and value to the name you choose to your instance. (Optional step)
- Click **Next**.

![aws-ec2-create-instance.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658774131786/chESLjlc-.png align="left")

**Create a Security Group:**
- Assign a security group: **Create a new security group**
- Set the security group name and description as you choose.
- Type: **RDP**
- Protocol: **TCP**
- Port Range: **3389**
- Source: **My IP**
- Description: (optional)
- Click **Review and Launch**.
- Click **Launch**.

![aws-ec2-sg-rdp.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658774112254/tkC4nXHa2.png align="left")

**Create a Key Pair:**
- Select: **Create a new key pair**
- Set the key pair name as you choose.
- Click **Download Key Pair**
- Click **Launch Instances**

![aws-ec2-keypair.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658774092728/XlB7rNcTEq.png align="left")

**Connect to instance:**
- Back to EC2 Instances panel in the AWS Console.
- Select the instance.
- Click **Connect**.
- Connection method: **A standalone RDP client**
- At the RDP client of your choice, input the details provided.
- Target: **Public DNS**
- User name **Administrator**
- Password: Click **Get Password**
- Key Pair Path: Click **Browse** to select the keypair downloaded on the previous step.
- Click **Decrypt Password**
- **Connect**.

![aws-ec2-connect-rdp.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658774068360/memCqWA27.png align="left")

Step 2 : Install Cisco Packet Tracer on the instance
----------------------------------------------------

**Download/Install Cisco Packet Tracer:**
- Inside the server, open a browser and login to: **netacad.com**
- Click **Resources**
- Click **Download Packet Tracer**
- Download the **Windows 64 Bit** version.
- **Run** the file downloaded.
- Accept the agreement. Click **Next**; **Next**; **Next**; **Next**; **Install**; **Finish**

Step 3 : Enjoy!
---------------

Now you have the Cisco Packet Tracer installed and ready to go!

![aws-ec2-windows-pt.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658774005790/auL_P3lh5.png align="left")

Step 4 : But before you go... save your work!(and some money)
-------------------------------------------------------------

Don't leave your instance running without any purpose. Save your instance (all configured and tweaked) to use it whenever you're up to lab again.

**Save your files:**

Install the AWS CLI as instructed on the [User Guide](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-windows.html)

**Create a S3 bucket:**

```
aws s3 mb s3://mybucket/
```

Upload the files to the bucket:

```
aws s3 cp local-file s3://mybucket/
```

You can also pull files from the bucket:

```
aws s3 cp s3://mybucket/remote-file /local-folder/
```

**Create an AMI**
- Back to EC2 Instances panel in the AWS Console.
- Select the instance.
- Click **Actions**; **Image**; **Create Image**

Your AMIs will be available on the EC2 Images panel in the AWS Console.

![aws-ec2-ami.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658774353026/_d9C_KhRR.png align="left")

**Don't forget to terminate your instance!**

- Back to EC2 Instances panel in the AWS Console.
- Select the instance.
- Click **Actions**; **Instance State**; **Terminate**
- Click **Yes, Terminate**