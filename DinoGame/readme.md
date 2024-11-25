![image](https://github.com/user-attachments/assets/12d7abc6-a966-40c7-b630-416f4d1539a3)

**Summary :**

We are going to build the chrome dinosaur game (looks like below) and put it on a GitHub repository.

![image](https://github.com/user-attachments/assets/82d29b8c-cc41-45f6-87c1-77b87cb14e9c)

This GitHub repository is connected to AWS S3 via a continuous deployment pipeline using AWS Code Pipeline.

Any changes to the GitHub repository will be automatically exported and deployed to the connected AWS S3 bucket where it will be hosted as a static website.

This website will be publicly accessible for anyone to access via the S3 endpoint and play.

**AWS Services used:** S3, AWS Code Pipeline

**Cost Involved:** S3 is free, if your account is less than 12 months old, otherwise it’s still very cheap.

Code Pipeline would cost you a few cents. It’s a good practice to delete the resources as soon as you are done building the project.

**The Code:**

Learning how to code games is not the intention of this project. So, the source code is available at the below GitHub repository:

https://github.com/Anshu083/chrome-dino-game

The game uses web technologies like HTML, CSS, JavaScript and images.

Once you fork the repository and copy it into your own GitHub, we will proceed with setting up the AWS side of things.

**This project will contain the following stages:**

1.      Create an S3 bucket to host the website and configure for public access

2.      Create a code pipeline to bring code from GitHub to S3 bucket and deploy it

**Create an S3 bucket to host the website:**

Only static websites can be hosted on AWS S3 , which means websites with no server-side scripting.

Only websites with client-side scripting that doesn’t need any server side processing, are supported by S3 for hosting.

Go to S3 and click create bucket.

This GitHub repository is connected to AWS S3 via a continuous deployment pipeline using AWS Code Pipeline.

Any changes to the GitHub repository will be automatically exported and deployed to the connected AWS S3 bucket where it will be hosted as a static website.

This website will be publicly accessible for anyone to access via the S3 endpoint and play.

**AWS Services used:** S3, AWS Code Pipeline

**Cost Involved:** S3 is free, if your account is less than 12 months old, otherwise it’s still very cheap.

Code Pipeline would cost you a few cents. It’s a good practice to delete the resources as soon as you are done building the project.

**The Code:**

Learning how to code games is not the intention of this project. So, the source code is available at the below GitHub repository:

https://github.com/Anshu083/chrome-dino-game

The game uses web technologies like HTML, CSS, JavaScript and images.

Once you fork the repository and copy it into your own GitHub, we will proceed with setting up the AWS side of things.

**This project will contain the following stages:**

1.      Create an S3 bucket to host the website and configure for public access

2.      Create a code pipeline to bring code from GitHub to S3 bucket and deploy it

**Create an S3 bucket to host the website:**

Only static websites can be hosted on AWS S3 , which means websites with no server-side scripting.

Only websites with client-side scripting that doesn’t need any server side processing, are supported by S3 for hosting.

Go to S3 and click create bucket.

![image](https://github.com/user-attachments/assets/eb4ecc91-2cea-41a5-b5e2-a4db9ae26010)

Provide a bucket name and enable public access by unchecking the ‘Block all public access’ option.

Otherwise, the deployed website can’t be accessed over internet.

![image](https://github.com/user-attachments/assets/920ea9f4-ec77-4ae9-b186-cbaafed47c7b)

Acknowledge the current settings and leave the other fields unchanged. Click create bucket.

**Configure the S3 bucket:**

Now, the bucket is created and the public access is enabled. However, there are a couple more steps required to make the S3 bucket ready.

Enable static website hosting and provide public read access to all the contents of this bucket through an S3 policy.

Click on the bucket name and go to properties tab.

Go to the bottom of the page and find static website hosting option.

![image](https://github.com/user-attachments/assets/c896337d-4382-4801-9d3f-3a0ade0d8adc)

Click edit and enable static website hosting option. Enter index.html as the index document and save changes.

![image](https://github.com/user-attachments/assets/53fc0fb7-ace0-451d-932b-6a4a30b258e1)

Now navigate to the permissions tab.

![image](https://github.com/user-attachments/assets/82f91b60-8372-4e9d-819b-1ed5df1b72e4)

Edit and add a bucket policy to enable public read access for the bucket.

![image](https://github.com/user-attachments/assets/17509cc3-9331-4756-ad11-8993f6cab1e8)

Now we have setup the code in GitHub and got our S3 bucket ready for website hosting.

**Set up a code Pipeline:**

Navigate to Code Pipeline from services and click create new pipeline.

Select ‘Build from Custom Pipeline’ and click next.

Name the pipeline (e.g. game-pipeline) and select superseded as the execution mode.

![image](https://github.com/user-attachments/assets/5e95af9f-9236-40ee-97d3-3a40581dcda1)

Create a new service role and accept the auto populated name.

Click next and select the source provider (where the code lives) as GitHub(Version 2).

Click connect to GitHub and create a connection.

![image](https://github.com/user-attachments/assets/247b3608-0477-41a3-8de9-656085f57a87)

Provide a connection name and click ‘Install a new app’.

Enter GitHub login details when asked.

Once you login successfully, select your Git repository as below.

![image](https://github.com/user-attachments/assets/5ea3286e-fcb4-44f0-9346-0d786f2623d9)

Select the default branch as master. Keep the trigger setting unchanged and include main branch. Click next.

![image](https://github.com/user-attachments/assets/368b1f13-aa25-415f-980d-108ea3d96e1f)

You can skip the build stage for this project. A separate build and compilation phase isn’t required for this small java script project.

In the deploy step, select Amazon S3 as the deploy provider and select the name of the S3 bucket.

Check the ‘Extract file before deploy’ option.

![image](https://github.com/user-attachments/assets/1e93f8c6-4ae7-4022-8330-f422752cfd58)

Click next and review all the configuration.

Click ‘Create pipeline’.

Pipeline created successfully.

![image](https://github.com/user-attachments/assets/e328ffbf-302e-4963-90e6-1215c6d4873b)

In Source phase, it goes to GitHub and grabs the code (Java script, HTML, CSS) and in Deploy phase it deploys the code to our S3 bucket.

Go back to the S3 bucket and under properties navigate all the way to ‘Static website hosting’.

![image](https://github.com/user-attachments/assets/883f8c0f-1a24-4c0a-a213-e79322e36048)

Open the bucket website endpoint on a different browser tab.

The game should be live now.

![image](https://github.com/user-attachments/assets/af1ff4ac-3c62-4767-8c76-29d10a8419cf)

Now to make sure the pipeline is working as expected, make minor changes to the index,html file in GitHub and witness the changes being immediately deployed to S3 via code Pipeline.

We have a fully functional continuous deployment pipeline now.

Empty and delete the S3 buckets and delete the code pipeline to avoid any unwanted charges.

Congratulations on making it till the end.
