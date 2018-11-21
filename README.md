# awsreckognition

Preparing Slack

First make sure you're logged in to Slack, then follow these instructions to prep your app:

   1. Create an app 
   2. From the Basic Information tab under Settings take note of the Verification Token as it will be required later
   3. Navigate to the OAuth & Permissions tab under Features
   4. Under the Permissions Scopes section add the following permission scopes
        channels:history
        chat:write:bot
        files:read
        files:write:user
   5. Click Save Changes
   6. Click Install App to Team then Authorize then note the OAuth Access Token as it will be required later



NOTE: This setup will only work in regions where the "Reckognition Service is available"   
 Lambda code
   1. Create an S3 bucket in the proper region
   2. Upload .zip file on the bucket under the name you put in "CodeUri".
      ex. "CodeUri": "s3://<nameofbucket>/<nameoflambdazipfile>.zip"
 



 Running the cloudformation script
   1. Configure your aws cli to the proper region before running the command.
   2. Command example:
      aws cloudformation deploy --region eu-west-1 --template-file hotdog.yaml --stack-name hotdogtest --capabilities       CAPABILITY_NAMED_IAM --parameter-overrides VerificationToken=<vtoken from slack> AccessToken=<Oauth token from slack>
   
   
   Finalize Slack Event Subscription

   1. Navigate to the created stack in the CloudFormation console and note the value for the RequestURL output from the created  stack as it will be required later
   2. Return to the Slack app settings page for the Slack app created earlier
   3. Navigate to the Event Subscriptions tab under Features and enable events
   4. In the Request URL field enter the RequestURL value noted earlier
   5. Click Add Workspace Event and select message.channels
   6. Click Save Changes

  
Aditional security: 
 In the API Gateway console on AWS you can create API key and configure the header request ( in this case POST) to require the 
 API KEY token in order to verify that the API is invoked by a valid user.
  
