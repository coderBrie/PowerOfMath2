## AWS Project - Architect and Build an End-to-End AWS Web Application
In this hands-on project, I’ll walk you through how to design and build a simple web application from scratch.  We’ll pick five different services—Amplify, Lambda, IAM, API Gateway and DynamoDB—and talk about why/where to use them, and how to get them to work with each other.  As we go, we’ll build out each of the services, resulting in a fully-functional math web application.

![Screenshot](/images/img_1.png)

### [🌐 LIVE SITE](https://dev.dov7jejtaezo6.amplifyapp.com/)


What do we need?

- A way to create/host a webpage
- A way to involke the math functionality
- A way to do some math
- Somewhere to store/return the math result
- A way to handle permissions

## Step 1: Create an index.html page from scratch in a text editor
Open your text editor, create an index.html file and paste the code below:

 ```bash
        <!DOCTYPE html>
        <html>
            <head>
                <meta charset="UTF-8">
                <title>To the Power of Math!</title>
            </head>

            <body>
                To the Power of Math!
            </body>
        </html>

   ```

## Step 2: Deploying and hosting a web page with AWS Amplify
what we need to do is zip just the index.html file, now we're going to use amplify to deploy it.

In the aws console navigate to  amplify, click Get Started on Amplify Hosting:
![Screenshot](/images/img_2.png)

Select Deploy without Git Provider:
![Screenshot](/images/img_3.png)

Give the app a name, i'm going to call mine "power of math", the environment name i'm going to use "dev" and we want to drag and drop that zip file that we created:
![Screenshot](/images/img_4.png)

## Cost
All services used are eligible for the [AWS Free Tier](https://aws.amazon.com/free/).  However, charges will incur at some point so it's recommended that you shut down resources after completing this tutorial.
