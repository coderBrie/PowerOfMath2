## AWS Project - Architect and Build an End-to-End AWS Web Application
In this hands-on project, I’ll walk you through how to design and build a simple web application from scratch.  We’ll pick five different services—Amplify, Lambda, IAM, API Gateway and DynamoDB—and talk about why/where to use them, and how to get them to work with each other.  As we go, we’ll build out each of the services, resulting in a fully-functional math web application.

## The Application Architecture

![Screenshot](/images/app_archi.png)


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

Save and deploy, after the deployement is successfully completed, you can access the link under Domain, open it on a new tab, we now have a live web page that users can navigate to:

![Screenshot](/images/img_5.png)

## Step 3: Creating a Python Lambda function to implement our math functionality
we're going to use a lambda function as you might know a lambdafunction is just a bit of code that runs in response to some trigger for example when you upload a picture to an s3 bucket that could trigger a lambda function to go process the picture into a thumbnail or something like that it's just code or functions really sitting out there that get run when you need them and these are serverless meaning that you don't have to set up and manage servers to run the code it just happens automatically behind the scenes for you
so we'll write some python code and use the python math library to do the calculations that we need.

Back here on the console go ahead and open up new tab this time we're going to navigate to lambda, create a funtion:

![Screenshot](/images/img_6.png)

Then for function name i'm going to do "power of math function", in my case for runtime let's go with the latest version of python 3.11 , you can leave everything else the same and create function down here on the lower right:

![Screenshot](/images/img_7.png)


Fom the Code Source section, copy and replace the lambda function code provided below: 

 ```bash
      # import the JSON utility package
        import json
        # import the Python math library
        import math

        # define the handler function that the Lambda service will use an entry point
        def lambda_handler(event, context):

        # extract the two numbers from the Lambda service's event object
        mathResult = math.pow(int(event['base']), int(event['exponent']))

        # return a properly formatted JSON object
        return {
        'statusCode': 200,
        'body': json.dumps('Your result is ' + str(mathResult))
        }

   ```


   Replace and paste the lambda function code, save the changes and make sure to deploy by cliking the deploy button:

   ![Screenshot](/images/img_8.png)


## Step 4: Testing our Lambda function
let's test to make sure this functions work as we expect, click the little drop down arrow to the
right of test: 

![Screenshot](/images/img_9.png)

Set up a test event this basically lets us pass in some test data to make sure that the function's working, create a new event event name power of math test event, we only have two values to pass in one of them is going to be base and one is going to be exponent and you can choose whatever values you want here i'm going to do 2 to the power of 3, the clik the save button:

![Screenshot](/images/img_10.png)

Run the test by cliking the test button, the base value of 2 to the power of 3 should give us 8 as a result:

![Screenshot](/images/img_11.png)

## Step 5: How to invoke our Lambda function
The way to invoke that math functionality or basically invoke that lambda function so our users obviously aren't going to go into the aws console like we just did and run it so we need a public endpoint or url that can be called to trigger that function to run and for that we're going to use api gateway this is a core service in aws that you can use to build your own apis application programming interfaces whether those are http rest or websocket APIs and it's really the perfect way to
invoke a lambda function.

To Creating a REST API for our Lambda function using API Gateway, on console navigate the API Gateway, create a new one by clicking on the create api button, we're going to use REST API, so click build button:

![Screenshot](/images/img_12.png)


Leave these first two options as they are so this will be rest and a new api and then we need to give it a name
so mine will be "power of math api". you can leave everything else the same and then create api :

![Screenshot](/images/img_13.png)

For the API method to be called, on the left make sure you have resources selected and then make sure you've got the backslash selected and then create method:


![Screenshot](/images/img_14.png)


The type of method will be a post and for integration type we're going to use a lambda function and then the lambda function name itself you'll need to start typing it should be power of math function, click on create method:

![Screenshot](/images/img_15.png)


One other thing we need to do is enable CORS or Cross Origin Resource sharing:


![Screenshot](/images/img_16.png)


Basically what this does is allows a web application running in one origin or domain to be able to access resources on a different origin or domain, because our web application is running on one domain and amplify our lambda function is going to be running in another we need to be able to work across those domains or origins, clik save:


![Screenshot](/images/img_17.png)


Let's deploy the api so we can test it out:  


![Screenshot](/images/img_18.png)


We'll need to set up a new stage you might have different stages for dev test production and so on this one we'll call dev and deploy:


![Screenshot](/images/img_19.png)


You'll need to copy the invoke url on a notepad and we'll need that for later:


![Screenshot](/images/img_20.png)

## Step 5: Creating a new DynamoDB table to store our math result

we're going to be using DynamoDB this is a key value or NOSQL database it's generally going to be
lighter weight than something like a relational database where you have to go set up your schema your relationships and we have to deal with permissions as well specifically we're going to need to give our lambda function permission to write to the database so let's go work on this next.

On the console navigate to DynamoDB, create table: 


![Screenshot](/images/img_21.png)


We want to create table for table name i'll do "power of math database", for partition key we'll say ID
you can leave everything else the same and create table: 


![Screenshot](/images/img_22.png)


We do need to save the Amazon Resource Name or the ARN for this so if you click into that table and under general information and additional info grab the ARN right here and then just paste that into the same notepad or whatever you're using to store your links so this is my arn for the database and we'll come back and get that later: 


![Screenshot](/images/img_23.png)





























## Cost
All services used are eligible for the [AWS Free Tier](https://aws.amazon.com/free/).  However, charges will incur at some point so it's recommended that you shut down resources after completing this tutorial.
