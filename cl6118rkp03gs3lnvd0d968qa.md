# How to create your first Linux server in AWS

1\. Go to [https://aws.amazon.com/free/](https://aws.amazon.com/free/) and signup for a **Free Tier Account**.

2\. Once you have your account settled, it should send you to the **AWS Management Console**.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-02-25/cab6429b-841e-4de9-ae43-fcffda2321b6/user_cropped_screenshot.jpeg?tl_px=35,18&br_px=781,438&sharp=0.8&width=560 align="left")

**<mark>Alert! </mark>** <mark>AWS changes its dashboard layout quite frequently! This tutorial was made in </mark> **<mark>February 2023</mark>** <mark> but if you're seeing this in the future, where you click and how things look may have changed.</mark>

3\. Search for EC2

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-02-25/526ff1dd-2bad-467e-aa20-55ed7fabac99/user_cropped_screenshot.jpeg?tl_px=43,40&br_px=789,460&sharp=0.8&width=560&wat_scale=50&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark_default.png&wat_pad=262,139 align="left")

4\. In the EC2 Dashboard, click on Instances

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-02-25/0e0fb79f-37f1-41d5-908b-b987db8725d4/user_cropped_screenshot.jpeg?tl_px=0,7&br_px=746,427&sharp=0.8&width=560&wat_scale=50&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark_default.png&wat_pad=27,139 align="left")

5\. Launch Instance

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-02-25/75f0c45a-8e1d-473e-9712-92ab6ec0fb3d/user_cropped_screenshot.jpeg?tl_px=0,0&br_px=708,395&sharp=0.8&width=560&wat_scale=50&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark_default.png&wat_pad=428,59 align="left")

6\. Give your instance a name (Optional step)

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-02-25/bc33a3ba-3dcf-4ccf-9244-964502b9d923/user_cropped_screenshot.jpeg?tl_px=46,24&br_px=792,444&sharp=0.8&width=560 align="left")

7\. Choose a Linux distribution. We're going with the popular [Ubuntu](https://ubuntu.com/download/) server

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-02-25/99cdcfd6-fff5-4071-bb2f-c4eff1382346/user_cropped_screenshot.jpeg?tl_px=0,21&br_px=746,441&sharp=0.8&width=560&wat_scale=50&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark_default.png&wat_pad=126,213 align="left")

8\. Select a free-tier eligible Ubuntu image, and go for the latest LTS (long-term support) version.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-02-25/63bdaf1b-dc77-4205-9df4-6a7508883c25/user_cropped_screenshot.jpeg?tl_px=181,60&br_px=927,480&sharp=0.8&width=560&wat_scale=50&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark_default.png&wat_pad=448,139 align="left")

9\. Select a free-tier eligible instance type. That will depend on how much machine power you need. For the [Linux Upskill Challenge](https://www.reddit.com/r/linuxupskillchallenge/), Ubuntu runs just fine with a **t2.micro** instance.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-02-25/47510691-17d7-497b-882e-a0e55b14ecb9/user_cropped_screenshot.jpeg?tl_px=39,19&br_px=785,439&sharp=0.8&width=560&wat_scale=50&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark_default.png&wat_pad=368,144 align="left")

10\. Now let's prepare to access this instance later! We need to create a new [key pair](https://www.ssh.com/academy/ssh/public-key-authentication#key-pair---public-and-private).

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-02-25/687bfc0f-cb67-4fa5-b6f6-f4506f5d6bb3/user_cropped_screenshot.jpeg?tl_px=88,35&br_px=834,455&sharp=0.8&width=560&wat_scale=50&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark_default.png&wat_pad=435,139 align="left")

11\. Give the key pair a name easy to remember.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-02-25/8380aa6b-3a5f-4b27-8ca6-b3822ac93cb6/user_cropped_screenshot.jpeg?tl_px=22,11&br_px=768,431&sharp=0.8&width=560 align="left")

12\. The **key pair type** determines what type of [Host key](https://www.ssh.com/academy/ssh/host-key) we're using. Since our host (instance) is Linux, we can use either RSA or ED25519 cryptography. Both are fine for a first instance, but ED25519 keys are known for being more secure and performant than RSA keys.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-02-25/14190981-2f27-43a8-a41e-bafb166f9c11/user_cropped_screenshot.jpeg?tl_px=0,0&br_px=746,420&sharp=0.8&width=560&wat_scale=50&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark_default.png&wat_pad=72,70 align="left")

13\. Now we're getting to the [Client key](https://www.ssh.com/academy/ssh/client), the key you will be using to fire up that connection from your personal computer. This is quite simple: if you are using Windows, choose *.ppk*; if you're using Mac, choose *.pem*

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-02-25/bfef7f5a-ba9c-4b8e-a3c7-58d4a970e56d/user_cropped_screenshot.jpeg?tl_px=0,31&br_px=746,451&sharp=0.8&width=560&wat_scale=50&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark_default.png&wat_pad=92,141 align="left")

14\. All good? Create key pair. The file for your client key will be generated and it will be prompted for download. **Download it NOW!** You won't be prompted again.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-02-25/0e8080ab-3ceb-4c4a-a602-cb0cee5c2c4a/user_cropped_screenshot.jpeg?tl_px=0,0&br_px=661,369&sharp=0.8&width=560&wat_scale=50&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark_default.png&wat_pad=419,242 align="left")

15\. A [**security group**](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-security-groups.html) is a way to control incoming and outgoing traffic to your instance, like a virtual firewall. This is not the same as blocking ports in your server, the security group rules will allow/deny access before you can get to the server.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-02-25/7df900fe-2cd4-48b6-9744-38c39ffb8a16/user_cropped_screenshot.jpeg?tl_px=0,31&br_px=746,451&sharp=0.8&width=560&wat_scale=50&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark_default.png&wat_pad=39,216 align="left")

**<mark>Alert!</mark>** <mark> Rules allowing traffic from anywhere are very open and you'd be bypassing a layer of security AWS provides you. However, this is not the only </mark> [<mark>layer of security</mark>](https://wa.aws.amazon.com/wellarchitected/2020-07-02T19-33-23/wat.pillar.security.en.html) <mark> your instance has.</mark>

For the [Linux Upskill Challenge](https://www.reddit.com/r/linuxupskillchallenge/) students:

* Enable traffic for SSH, HTTP and HTTPS from ANYWHERE
    
* Sounds dangerous but it will give you lots to tweak during the challenge, trust me.
    

16\. You just created a SSH key pair, allow SSH traffic.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-02-25/ab2f9906-45a8-4685-bd16-32deeb4bf4da/user_cropped_screenshot.jpeg?tl_px=0,0&br_px=746,420&sharp=0.8&width=560&wat_scale=50&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark_default.png&wat_pad=30,117 align="left")

17\. If you intent to create serve a website with basic HTTP access, enable HTTP traffic

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-02-25/5987c383-4299-4e2d-b1ab-22d5c4a34ba9/user_cropped_screenshot.jpeg?tl_px=0,26&br_px=746,446&sharp=0.8&width=560&wat_scale=50&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark_default.png&wat_pad=18,171 align="left")

18\. If you intent to create serve a secure website with HTTPS access, enable HTTPS traffic

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-02-25/0103c399-2679-471c-bdc2-0987675a4122/user_cropped_screenshot.jpeg?tl_px=0,17&br_px=746,437&sharp=0.8&width=560&wat_scale=50&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark_default.png&wat_pad=21,139 align="left")

19\. This is automatically filled when you select the instance type, so don't worry about it. Fun fact: although Ubuntu minimum storage requirements doesn't exceed 2GB, AWS needs some room for snapshots and will not allow less than 8GB.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-02-25/c957ba06-c52d-4874-9672-5c42ac65e90e/user_cropped_screenshot.jpeg?tl_px=0,0&br_px=746,420&sharp=0.8&width=560&wat_scale=50&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark_default.png&wat_pad=48,87 align="left")

20\. The type of storage is also picked according to the type of instance, but just so you know, this will be a general purpose SSD.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-02-25/5967d854-26bf-4977-8fc0-4b3ffad16dc7/user_cropped_screenshot.jpeg?tl_px=0,17&br_px=746,437&sharp=0.8&width=560&wat_scale=50&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark_default.png&wat_pad=246,246 align="left")

21\. You can pick the number of instance to launch in the **Summary** section, as also review your setup.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-02-25/f2c5b661-e505-4ac5-8fac-16154e4fcbd9/user_cropped_screenshot.jpeg?tl_px=0,0&br_px=746,420&sharp=0.8&width=560&wat_scale=50&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark_default.png&wat_pad=201,108 align="left")

22\. Launch!

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-02-25/c204c785-fe83-486e-a85b-1208b2b97059/user_cropped_screenshot.jpeg?tl_px=0,0&br_px=640,357&sharp=0.8&width=560&wat_scale=50&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark_default.png&wat_pad=339,247 align="left")

23\. When the instance is done launching, it will receive an instance id and you can click to see it your dashboard.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-02-25/94bb9005-4fed-48ef-8f79-f0c2ee2b4cf7/user_cropped_screenshot.jpeg?tl_px=0,0&br_px=619,346&sharp=0.8&width=560&wat_scale=50&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark_default.png&wat_pad=345,144 align="left")

24\. Click on the instance id to see more details.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-02-25/85068b8a-95cb-4ea2-9575-8489bbe04009/user_cropped_screenshot.jpeg?tl_px=0,0&br_px=694,388&sharp=0.8&width=560&wat_scale=50&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark_default.png&wat_pad=219,165 align="left")

25\. If the instance is good for connection, it will show the instance state as **Running**

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-02-25/e27d7fe9-8e70-4dc8-994b-419aac90db24/user_cropped_screenshot.jpeg?tl_px=72,38&br_px=818,458&sharp=0.8&width=560 align="left")

26\. If it's still showing **Pending**, give it a few minutes and refresh the instance panel by clicking on the refresh button.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-02-25/b420397f-fa73-41a3-b5d9-bf3bb78097f5/user_cropped_screenshot.jpeg?tl_px=157,0&br_px=903,420&sharp=0.8&width=560&wat_scale=50&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark_default.png&wat_pad=262,44 align="left")

27\. When the instance is **Running**, you can now **Connect**.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-02-25/58bbf109-6aa5-4d76-9e5a-5e9480ec6e75/user_cropped_screenshot.jpeg?tl_px=343,0&br_px=1089,420&sharp=0.8&width=560&wat_scale=50&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark_default.png&wat_pad=277,69 align="left")

**Alert!** Not all connection methods will be available for all types of instances and [some methods will require additional configuration](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstances.html).

28\. [**EC2 Instance Connect**](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Connect-using-EC2-Instance-Connect.html) is a very convenient way to connect to your instance, but it [does not support](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-connect-methods.html) all Linux distributions or all AWS regions.

29\. To connect using [**Session Manager**](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/session-manager.html), you have to [set it up first](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager-getting-started.html).

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-02-25/539c09ca-5db9-4414-bae4-d323e34c46c1/user_cropped_screenshot.jpeg?tl_px=95,51&br_px=841,471&sharp=0.8&width=560 align="left")

30\. [**EC2 serial console**](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-serial-console.html) requires [even more setup](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/configure-access-to-serial-console.html), that includes granting account access to the serial console and configuring IAM policies.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-02-25/95f3bf9f-804e-4313-8539-0cc6fc1ae016/user_cropped_screenshot.jpeg?tl_px=43,22&br_px=789,442&sharp=0.8&width=560 align="left")

31\. Now, the good one! Using a [SSH client](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/connection-prereqs.html) you can connect from Mac, Windows or another Linux and it will be the same for all of them.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-02-25/4deb2b7f-4d84-4ac5-8319-425dfac31e28/user_cropped_screenshot.jpeg?tl_px=96,52&br_px=842,472&sharp=0.8&width=560 align="left")

32\. [Locate the private key and set the permissions](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/connection-prereqs.html#connection-prereqs-private-key) so that only you can read the file, for security reasons.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-02-25/31044c8b-fc0d-40c3-9879-9b35178bf73c/user_cropped_screenshot.jpeg?tl_px=0,0&br_px=652,364&sharp=0.8&width=560&wat_scale=50&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark_default.png&wat_pad=73,188 align="left")

33\. And finally, [connect](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstancesLinux.html#AccessingInstancesLinuxSSHClient) to your Linux instance using the [SSH client](https://www.ssh.com/academy/ssh/client) of your choice.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-02-25/6842d3b5-b8cb-4469-a8f5-c784916d8b4c/user_cropped_screenshot.jpeg?tl_px=0,54&br_px=746,474&sharp=0.8&width=560&wat_scale=50&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-labs-public.s3.us-east-2.amazonaws.com/images/watermarks/watermark_default.png&wat_pad=65,214 align="left")

34\. This is what your first Linux server will look like in the terminal:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1677361599822/1dbc56ef-20e5-4676-a599-18b027e562a5.png align="center")

![]( align="left")