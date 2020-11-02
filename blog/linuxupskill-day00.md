 # Day 0 : Preparing the environment

This is part of the [#LinuxUpSkillChallenge](../challenges/linux-upskill.html). Don't forget to also check out the [Official Instructions](https://github.com/snori74/linuxupskillchallenge/blob/master/00-AWS-Free-Tier.md) and the [Reddit](https://www.reddit.com/r/linuxupskillchallenge/comments/jm8wlz/how_this_works/) posts.

*video*

 ## Objectives of the day
 1. **Sign up to a cloud provider:** you can use [AWS](https://aws.amazon.com/free/), [Google Cloud](https://cloud.google.com/), [Azure](https://azure.microsoft.com/), [Digital Ocean](https://www.digitalocean.com/), [Linode](https://www.linode.com/), etc. I'm already signup with AWS, so I'm using that.
 2. **Launch an Ubuntu instance:** Follow the tutorial [How to launch an EC2 instance](../howtos/howto-aws-ec2-launch-instance.html), select the latest version of Ubuntu and set the security group to **All Traffic / Anywhere**.
 3. **Connect to the instance using SSH:** Follow the tutorial on [Putty Basics](../howtos/basic-putty.html) or (if you're using OpenSSH) simply copy the command from AWS instructions.

## Administrative task: **Update/Upgrade the system**

Once connected, submit the commands:
```
sudo apt update
```
And then:
```
sudo apt upgrade -y
```

**Done!**


For more detail on how I did each day, check out my log on [Reddit](https://www.reddit.com/user/livia2lima). Follow me on [Twitter](https://twitter.com/search?q=%23LinuxUpSkillChallenge%20%40livialimatweets&src=typed_query&f=live) for daily updates.
