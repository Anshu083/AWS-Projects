**AWS Project: Build a Resume/CV website on AWS**

![image](https://github.com/user-attachments/assets/03425137-1313-4eec-b7af-f4d25c3b8de9)

**Summary:**

Build an interactive resume/CV using HTML, CSS and JavaScript and host this static website on AWS S3. 

A user-friendly website name is issued using Route 53 DNS service and to make the site secure, SSL certificate is used on AWS CloudFront distribution service (CDN) using AWS certificate manager.

CloudFront Content Delivery network (CDN) service is used here for the purpose of binding the SSL certificate, as it can't be bound to S3 bucket directly. However, CloudFront has a lot of other usages in terms of a fully managed CDN service.

The final product will look like below, an interactive resume hosted on your own website.

![image](https://github.com/user-attachments/assets/37db7bd5-bcb5-4dae-b09c-01c74775de71)

**AWS Services used:**

CloudFront (CDN), Route 53 DNS service, AWS certificate Manager (ACM), AWS S3

**Cost involved:** 

S3 - Free to a few cents

CloudFront - Free to a few cents depending on the number of requests made

Route 53 - Free to 10$+ for the domain registration

ACM - Free

**Project Plan:**

Part 1: Build and host a static website on AWS S3

Part 2: Register a custom domain name on Route 53 and point it to AWS S3 bucket endpoint 

Part 3: Incorporate CloudFront and SSL/HTTPS and edit the Route 53 record to point to CloudFront distribution

**Implementation:**

**Part 1:**

Create a resume using HTML, CSS and Java Script.

We can use GenAI tools like chat GPT for the code generation or the code I used is available here: 

Anshu083/MyResume: My Resume website (github.com)

Make necessary changes in the HTML file, like changing your name and other relevant details. Save your photo in the project folder as headshot.jpg.

Create an S3 bucket with the same name as the custom URL you are going to create or might already own. e.g. itsanshuman.com 

Configure the bucket to host static website and create a policy to enable public read access to the bucket.

![image](https://github.com/user-attachments/assets/db13ce73-4eeb-4d83-b141-b867aaf07117)

Upload the website files to the S3 bucket.

Make sure your resume website is available on the S3 bucket endpoint.

**Part 2:**

Go to Route 53 and register a custom domain from Route 53. It would cost around 14$-17$ for one year.

Alternatively, you can use your existing domain name from any other vendor and use it in Route 53.

Amazon Route 53 is a highly available and scalable Domain Name System (DNS) web service from AWS. You can use Route 53 to perform three main functions in any combination: domain registration, DNS routing, and health checking.

A hosted zone needs to be created in Route 53 that associates to your domain.

Create an 'A record' in the hosted zone to point this domain name to your S3 static website endpoint. 

An 'A record' maps a domain name to an IPV4 address/alias name.

Make sure the name of your S3 bucket should match your domain name.

Any request made to the newly acquired domain name should be routed to the S3 website endpoint. 

Now, our resume website should be available on the new domain e.g. itsanshuman.com in my case.

**Part 3:**

Navigate to Certificate Manager and configure the region to be same as your S3 bucket region.

Either request a new certificate or import one from another CA.

If you are requesting a new one (more convenient), enter your domain details and select domain verification and click 'create record in Route 53'.

It will create a new CNAME record in route 53.

Now a new certificate has been issued for the domain, however you can't use the certificate with S3 website.

We need to set up a CloudFront distribution that points to the S3 website and then the certificate goes on CloudFront.

Navigate to CloudFront and create a CloudFront Distribution.

Use the S3 website endpoint as origin domain.

Select your domain as the alternate domain name and choose your newly issued certificate to bind. 

Create the distribution and check details.

Now the resume website should be available at the distribution domain name, and you will see the secure connection or padlock sign on address bar.

However, we want our resume to be available at itsanshuman.com with the padlock sign.

Navigate to route 53 and edit the existing A name record.

Configure it to route traffic to CloudFront distribution instead of S3 website endpoint.

Now, our resume is available on our secure SSL enabled website itsanshuman.com.

Thank you for going through the article.
