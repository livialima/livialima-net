## How to build a static website on AWS in 5 easy steps

*Update from July 2022: things changed and I no longer follow this model for my website, but it ran good 2 years very successfully.*

Backstory
---------

I spent so many years procrastinating and failing attempts at blogging. All the beautiful things I could do overwhelmed me. And then I remember how bad I am at keeping the writing pace I was setting up for myself. Inspired by [Nick Russo](http://njrusmc.net/)'s minimalist approach, I finally pushed my content to AWS.

Interestingly enough, I was very pleased to find that I was not the only person doing this. So much that there is a [#CloudResumeChallenge](https://twitter.com/hashtag/CloudResumeChallenge) going around. This is an initiative from [Forrest Brazeal](https://forrestbrazeal.com/2020/04/23/the-cloud-resume-challenge/). He helps people show concrete cloud skills that could land them their next job. Please refer to Forrest's guidelines to take part in the challenge, because this is so cool!

I already have IT experience, which disqualifies me. But since my initial goal was to simply put my website out there, here are the steps I took to get the same results.

NOTE: people tend to forget the official documentation. It is free and available on AWS white pages. If you're a nerd like me and want to learn the details, check out how to [Host a Static Website](https://aws.amazon.com/getting-started/hands-on/host-static-website/) right from the source.

Step Zero : Domain name, content and format
-------------------------------------------

### Purchase a domain name

Nobody will remember that huge public S3 url when trying to access your website. **Not even yourself.**

So get an unique name people can type. Most domains cost $9 to $18 a year and there are plenty of resources available. Google, for example, has its own domain site. It is easy to use with tons of tutorials and an extensive FAQ resources section.

If you want to keep everything within AWS, go with [Route 53](https://aws.amazon.com/route53/). Here you can buy a domain name from inside the AWS console.

### Create and format your content

Create a content. If you don't know what to write, create a resume. It's simple, direct and look a lot cooler than only having a LinkedIn profile.

Format it as you like, but if you are short on HTML/CSS skills, the Internet is full of templates. I recommend you to check out [W3Schools](https://www.w3schools.com/) and [freeCodeCamp](https://www.freecodecamp.org/). Harness the front-end dev that lives in you!

### Create an AWS account for access to S3

Duh.

Step 1 : Create a S3 bucket and configure it as static website
--------------------------------------------------------------

### Create a S3 bucket

Okay, on to the fun part! First thing we need is a S3 bucket.

It is critical that your bucket has the same name as your domain name. If your website domain is _mywebsite.com_, then your bucket name must be _mywebsite.com_.

The reasoning for this has to do with how requests are routed to S3. The request comes into the bucket, and then S3 uses the Host header to route to the appropriate bucket.

```
aws s3 mb s3://mywebsite.com
```

*AWS Console:*
- Navigate to S3 in the AWS Console.
- Click **Create bucket**.
- Input the name for the bucket and choose a region to host it.
- Click **Next** to go to the next panel.
- Click **Next** - leave the **Configure options** panel as is.
- Click **Next** - leave the **Set permissions** panel as is (we'll deal with it later).
- Click **Create bucket** (yeah, it is that easy)

Voilà! Bucket created!

![aws-s3-create-bucket.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658775725313/BLNjNlU-h.png align="left")

### Set the bucket to versioning

This step is kinda optional, but good to do anyway. Versioning your bucket ensures every object there has previous versions available to restore.

```
aws s3api put-bucket-versioning --bucket mywebsite.com --versioning-configuration Status=Enabled
```

*AWS Console:*
- Navigate to S3 in the AWS Console.
- Click into your bucket.
- Click the **Properties** section.
- Click the **Versioning** option.
- Select **Enable Versioning**.
- Click **Save**.

![aws-s3-versioning-bucket.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658775701665/4jbhjIEzn.png align="left")

### Set the bucket as static website

Your S3 bucket should act like a static website, not a normal bucket. Let's set it up as such.

```
aws s3 website s3://mywebsite.com/ --index-document index.html --error-document error.html
```

*AWS Console:*
- Navigate to S3 in the AWS Console.
- Click into your bucket.
- Click the **Properties** section.
- Click the **Static website hosting** option.
- Select **Use this bucket to host a website**.
- Enter _index.html_ as the Index document.
- Click **Save**.

![aws-s3-website-bucket.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658775673918/pDBlMbJBw.png align="left")

You now have an **Endpoint** address. It is a S3 website url like this _http://mywebsite.com.s3-website-us-east-1.amazonaws.com/_.

### Set bucket permissions : public access

Your bucket serves your static website, so it must be accessible to anyone in the world. We call this anonymous access to the bucket.

By default, public access is denied to any new buckets created. Because, you know, public buckets are an unnecessary exposure. Yet, for our static website, we need a public access bucket policy. You must complete this step before adding the bucket policy.

```
aws s3api put-public-access-block --bucket mywebsite.com --public-access-block-configuration '{"BlockPublicPolicy": false, "RestrictPublicBuckets": false}'
```

*AWS Console:*
- Click into your bucket.
- Select the **Permissions** tab at the top.
- Under **Block Public Access**, click **Edit**.
- Turn **off** _"Block public access to buckets and objects granted through new public bucket or access point policies"_
- Turn **off** _"Block public and cross-account access to buckets and objects through any public bucket or access point policies"_
- Leave the other permissions blocked **on**, and **Save**.
- Confirm the operation by typing **confirm** in the alert window and click **Confirm**.

![aws-s3-permission-bucket.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658775639002/6YMNgQo00.png align="left")

### Set bucket permissions : policy

Now let's update the Bucket Policy to allow public read access to anyone in the world. AWS works with JSON format for its configuration. You can have your .json file uploaded from the CLI or add it to the Console.

```
aws s3api put-bucket-policy --bucket mywebsite.com --policy file://policy.json
```

*AWS Console:*
- Still inside the **Permissions** section.
- Select **Bucket Policy**.
- Add the JSON code to the Bucket Policy.
- **Save** and your bucket is now public.

![aws-s3-policy-bucket.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658775610804/SE-1SsHS9.png align="left")

**Bucket policy example:**
```
{
    "Version": "2008-10-17",
    "Statement": \[
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "\*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::mywebsite.com/\*"
        }
    \]
}
```

DISCLAIMER: This policy opens up your bucket to the world. Any object in this bucket is available to the public now. Don’t put anything in this bucket that you’re not willing to share!

### Upload your content to the bucket

Copy all the files for your website into the bucket. The root page of your website (index.html) should be at the root level of the S3 bucket.

```
aws s3 cp local\_folder/mywebsite/ s3://mywebsite.com/ --recursive
```

*AWS Console:*
- Navigate to S3 in the AWS Console.
- Click into your bucket.
- Click the **Upload** button.
- Drag and drop or select **Add files**, add the entire static website directory.
- No need to configure permissions for the files, we did that for the bucket. Click **Upload**.

![aws-s3-upload-files.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658775555557/4OYhTlsc0.png align="left")

### Check if the bucket is accessible

Remember that **Endpoint** address? The one you got when you enabled the static website hosting? You can use it now to check if your website is available.

Step 2 : Create a pipeline for automated deployments
----------------------------------------------------

So far, every time we update a page or write a new blog post, we have to reflect that to our bucket. As fun as it is, uploading files by hand gets old fast!

So why not automate it? Let's setup Git repository with [CodeCommit](https://aws.amazon.com/codecommit/). And then a pipeline in [CodePipeline](https://aws.amazon.com/codepipeline/) to deploy our code to the S3 bucket when we push to Git.

### Setup a repository in CodeCommit

*AWS Console:*
- Make sure to have the [required IAM credentials](https://docs.aws.amazon.com/codecommit/latest/userguide/setting-up-gc.html) to CodeCommit beforehand.
- Navigate to CodeCommit in the AWS Console.
- Click **Create repository**.
- Click **Create**.

![aws-codecommit-create-repo.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658775524634/_o2Q1NkEm.png align="left")

### Setup a pipeline in CodePipeline

AWS Console:
- Navigate to CodePipeline in the AWS Console.
- Click **Create pipeline**.
- Enter a **name** for your pipeline.
- Select **New service role**.
- Role name will fill out with something like _AWSCodePipelineServiceRole-us-east-1-mywebsite-pipeline_
- If not, check the box for **Allow AWS CodePipeline to create a service role**.
- Click **Next**.

![aws-codepipeline-create-pipeline.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658775495817/XUSeawij5.png align="left")

- Select **AWS CodeCommit** as source provider.
- Select the repository name.
- Select the **master** branch.
- Select **CodePipeline** as the option for change detection.
- Click **Next**.

![aws-codepipeline-pipeline-source.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658775470239/jbE4j7n5p.png align="left")

- Selection of a build stage is optional. As we didn't setup any, click **Skip build stage**.
- Select **Amazon S3** as deploy provider.
- Select the same **region** of the S3 bucket.
- Select the bucket name.
- Check the box for **Extract the file before deploy**
- Click **Next** and then **Create pipeline**.

![aws-codepipeline-pipeline-deploy.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658775455669/5iNrIzecr.png align="left")

### Alternative step: use GitHub instead

The steps are the same as with CodeCommit, the difference is the **source** selected.

*AWS Console:*
- Select **GitHub** as source provider.
- Click on the **Connect to GitHub** button. That will connect to your GitHub account.
- Select the repository name.
- Select the **master** branch.
- Select **GitHub webhooks** as the option for change detection.
- Click **Next**.
- Selection of a build stage is optional. As we didn't setup any, click **Skip build stage**.

![aws-codecommit-github-repo.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658775428135/4zICv_sXY.png align="left")

Step 3 : Create a SSL certificate
---------------------------------

We don't want only a website. We want a SECURE website. Don't you feel good seeing the little _"Connection is secure"_ on your address bar? To allow access through HTTPS, we need to create a SSL certificate first.

AWS Console:
- Navigate to Certificate Manager in the AWS Console.
- Click **Request a certificate**.
- Select **Request a public certificate** and then click on **Request a certificate**.
- Add your domain name. Make sure you request a certificate for \*.yourdomain.com so it covers all sub-domains. Click **Next**.
- You must be the owner of this domain, select the **Email validation** to confirm. Click **Next**.
- Give it a "Name" tag to identify the certificate on your dashboard, click **Review**.
- Confirm and request. It can take a few moments to complete the validation.

![aws-create-certificate.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658775395866/AcI3ebkC5.png align="left")

Step 4 : Create a CloudFront distribution
-----------------------------------------

Now we need distribute our content. CloudFront Distribution is here for this.

*AWS Console:*
- Navigate to CloudFront in the AWS Console.
- Click **Create distribution**.
- Select **Web** as the delivery method. Click **Get Started**.
- Origin Domain Name: select your **S3 bucket**.

![aws-cloudfront-origin.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658775376069/JZ82B0sF3.png align="left")

Viewer protocol policy: **Redirect HTTP to HTTPS**.
Allowed HTTP Methods: **GET, HEAD, OPTIONS**.

![aws-cloudfront-cache.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658775362662/Ur9609ZmQ.png align="left")

- Alternating domain names: add your domain name, i.e. _mywebsite.com_
- Select **Custom SSL Certificate** and select the certificate you created. Make sure the certificate is already validated.

**Create Distribution**

![aws-cloudfront-domain.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658775344143/dUeMd2d2Z.png align="left")

Step 5 : Config the DNS management
----------------------------------

We have all the backstage ready, now let's release it to the world! For that, we need to let your domain to pull the content. That's what the DNS is for.

*AWS Console:*
- Navigate to Route53 in the AWS Console.
- Go to Hosted Zone. Click **Create Hosted Zone**
- Enter in your domain name without the www (e.g. example.com). Click **Create**.
- That will give you the default record sets (the cluster of 4 NS-type). You will need to create two more custom record sets.
- Click **Create Record Set**.
- Select **Yes** for Alias.
- Set your Alias Target to point to your **CloudFront distribution** and Create.
- Create another Record Set. Redirect to the same Alias Target. But this time, add _www_ to the "Name" field so it will point to your domain _www.mywebsite.com_.

![aws-route53-create.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658775320674/j2eYoqKdy.png align="left")

### Extra step : Transfer an existing domain to AWS

If you are like me, you may have purchased a domain with Google before you figured out Amazon could do it too. So how to make AWS use the DNS for your domain, then? Tell Google to send all requests to your website in AWS!

- Log into [Google Domains](https://domains.google.com)
- Click on your domain.
- Click on the **DNS** menu.
- Select **Use Custom Name Servers** instead of the default Google Domains.
- Click on the **+** button 3 more times to get a total of 4 text fields.
- Copy and paste each Name Server (NS) from the Route 53-Record Sets panel.

![gcp-domains-custom.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1658775289484/8v3VFXBuh.png align="left")

The site should be available almost immediately. Yet, it can take some time for DNS to propagate around the world.

Bonus : Visitor counter
-----------------------

I didn't put in place a visitor counter yet, that's not my priority right now. But if you are here for the challenge, I recommend you check the [reddit thread](https://www.reddit.com/r/aws/comments/gjl5wi/i_wrote_a_guide_on_building_your_own_resume_site). There are good tips and references there that can help you.

Conclusion
----------

You did it! You’ve got a static website that updates on Git push. And it is served over HTTPs! That will be a nice example of your skills for future employers. Nice!

I hope that this post helped get started with AWS by doing something cool.