# Reporting

To deploy, execute in Reporting:

Before you begin your first deployment, make sure you have working credentials for AWS Console from Conti. To access the AWS Console from a web browser, please visit ADFS, login with your Conti credentials and select Sign-In for Amazon Web Services.

1. From Reporting root folder run the following

````bash
 npm install
````
2. Copy the folder test inside the deployment folder, (Reporting->deployment->Reporting->stages->test) and rename it with the <your_user_name_without_numbers>. Update the files
  * cloudformation.properties
  * stageVariables.properties
  * all files inside the lambda-environment folder
  
with the developers stage information.

3. Run the following

````bash
 ./gradlew build
````

````bash
 ./gradlew <your_user_name>Stage deployApi --parallel
````
