# Reporting

To deploy, execute in Reporting:

1. From Reporting root folder run the following

````bash
 npm install
````
2. Copy the folder test inside the deployment folder, (Reporting->deployment->Reporting->stages->test) and rename it with the <your_user_name_without_numbers>. Update the files
* cloudformation.properties
* stageVariables.properties
* all files inside the lambda-environment folder
with the developers stage information.

````bash
 ./gradlew <your_user_name>Stage deployApi --parallel
````
