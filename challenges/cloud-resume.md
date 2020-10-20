# The Cloud Resume Challenge

The [cloud resume challenge](https://cloudresumechallenge.dev/) is a hands-on challenge created by [Forrest Brazeal](https://forrestbrazeal.com/). The idea is to **create your own resume using essential cloud skills**.

**My Background**: I found this challenge when I was preparing to publish my website and the simplicity was what hooked me. I already have IT experience, which disqualifies me for a referral from Forrest. But since my initial goal was to simply put my website out there, there's no harm in trying.

**My Progress**: The challenge consists of [16 proposed steps](https://cloudresumechallenge.dev/instructions/). I did the first 6 steps to start blogging and, for that, it's good enough. But I wanted to finish the thing, so here we are.

## 13/16 Completed
- [x] **Certification** Your resume needs to have the [AWS Cloud Practitioner](https://aws.amazon.com/certification/certified-cloud-practitioner/) certification on it.
- [x] **HTML** Your resume needs to be written in HTML.
- [x] **CSS** Your resume needs to be styled with CSS.
- [x] **Static S3 Website** Your HTML resume should be deployed online as an Amazon S3 static website.
- [x] **HTTPS** The S3 website URL should use HTTPS for security.
- [x] **DNS** Point a custom DNS domain name to the CloudFront distribution, so your resume can be accessed at something like ```my-c00l-resume-website.com```.
- [x] **Javascript** Your resume webpage should include a visitor counter that displays how many people have accessed the site. You will need to write a bit of Javascript to make this happen.
- [x] **Database** The visitor counter will need to retrieve and update its count in a database somewhere. Use DynamoDB.
- [x] **API** Do not communicate directly with DynamoDB from your Javascript code. Instead, you will need to create an API that accepts requests from your web app and communicates with the database. Use API Gateway and Lambda.
- [x] **Python** You will need to write a bit of code in the Lambda function; use Python – a common language used in back-end programs and scripts – and its boto3 library for AWS.
- [ ] **Tests** You should also include some tests for your Python code.
- [ ] **Infrastructure as Code** You should not be configuring your API resources; the DynamoDB table, the API Gateway, the Lambda function; manually, by clicking around in the AWS console. Instead, define them in an AWS Serverless Application Model (SAM) template and deploy them using the AWS SAM CLI. This is called “infrastructure as code” or IaC.
- [x] **Source Control** You do not want to be updating either your back-end API or your front-end website by making calls from your laptop, though. You want them to update automatically whenever you make a change to the code. (This is called continuous integration and deployment, or CI/CD.) Create a private GitHub repository for your backend code.
- [ ] **CI/CD (Back end)** Set up GitHub Actions such that when you push an update to your Serverless Application Model template or Python code, your Python tests get run. If the tests pass, the SAM application should get packaged and deployed to AWS.
- [x] **CI/CD (Front end)** Create a GitHub repository for your website code. Create GitHub Actions such that when you push new website code, the S3 bucket automatically gets updated.
- [x] **[Blog post](../howtos/howto-static-site-aws-cicd.html)** Finally, in the text of your resume, you should link a short blog post describing some things you learned while working on this project.
