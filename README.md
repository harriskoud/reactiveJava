# Reporting

The reporting repository which contains the API definitions for the reporting services used in RVD project.

## Architecture - Software Detailed Design (SWDD)

[SWDD](/releases/latest)

## Getting Started

This is a multi project gradle build.
The build logic in buildsrc needs nexus credentials to get the required packages.

* Set `rvdS3MavenAccessKeyId` and `rvdS3MavenSecretKey` in `~/.gradle/gradle.properties`.

## Setting up a microservice

We have a custom gradle plugin for deploying all microservices in the project.
The 3 parts of a microservice are described via a custom dsl in the `build.gradle` scripts.

## Requirements and Specification

Our specification is written in Markdown. The overall build collects all `readme.md` located in `doc/architecture` folders converts them to docbook chapters and makes them available in the `doc/spec/requirements` folder in the root project, where they can be added to the spec via `xinclude`.

Example:

    <xi:include xmlns:xi="http://www.w3.org/2001/XInclude" href="requirements/user_model.xml"
        parse="xml" />

For the syntax regarding requirements check out these files:
[Markdown](doc/spec/Readme.md)
becomes
[Docbook](doc/spec/spec.xml)

## Project Setup and Configuration

Each subproject uses the same settings for formatting and clean-up. Copy the following files to the `.settings` folder of a new subproject:

* `org.eclipse.jdt.core.prefs`
* `org.eclipse.jdt.ui.prefs`

There is only one `.gitignore` file in Reporting, which must also generically handle all subprojects.

## Individual Developer Stage

To be able to deploy to your individual developer stage add the following to your `~/.gradle/gradle.properties` file:

```properties
devstage.prefix=<your_user_name>
devstage.profileName=rvd-test
devstage.region=eu-west-1
devstage.host=<the_host_where_your_api_runs_on>
devstage.binaryPackageBucket=<a_s3_bucket_where_the_binary_packages_will_be_stored>
devstage.stageVariables.stagePrefix=<your_user_name>
devstage.stageVariables.stageSecretKey=asd8jJDF0asdunbdfl7i3kuoo2mdgds53klflll163XMMMu12

devstage.lambdaEnv.BindingProcessAggregator_BindingProcessAggregatorHandler.STAGE = #{deploy.stage}
devstage.lambdaEnv.BindingProcessAggregator_BindingProcessAggregatorHandler.ENDPOINTURL = https://s3-eu-west-1.amazonaws.com/rvd-<your_user_name_without_numbers>-service-discovery/sd.json
devstage.lambdaEnv.BindingProcessAggregator_BindingProcessAggregatorHandler.AUTH_SERVICE = rvdsvc_binding
devstage.lambdaEnv.BindingProcessAggregator_BindingProcessAggregatorHandler.AUTH_PASSWORD_ENCRYPTED = serv1c3

devstage.lambdaEnv.BindingProcessProvider_BindingProcessGetHandler.STAGE = #{deploy.stage}
devstage.lambdaEnv.BindingProcessProvider_BindingProcessGetHandler.ENDPOINTURL = https://s3-eu-west-1.amazonaws.com/rvd-<your_user_name_without_numbers>-service-discovery/sd.json
devstage.lambdaEnv.BindingProcessProvider_BindingProcessGetHandler.AUTH_SERVICE = rvdsvc_binding
devstage.lambdaEnv.BindingProcessProvider_BindingProcessGetHandler.AUTH_PASSWORD_ENCRYPTED = serv1c3

devstage.lambdaEnv.JwtCustomAuthorizer_ReportingAuthorizerHandler.PUBLIC_KEYSTORE_URLS = s3://rvd-<your_user_name_without_numbers>-keys/<your_user_name_without_numbers>/APU/key.jks;s3://rvd-<your_user_name_without_numbers>-keys/<your_user_name_without_numbers>/APS/key.jks;s3://rvd-<your_user_name_without_numbers>-keys/<your_user_name_without_numbers>/APD/key.jks;s3://rvd-<your_user_name_without_numbers>-keys/<your_user_name_without_numbers>/keys/public.jks
devstage.lambdaEnv.JwtCustomAuthorizer_ReportingAuthorizerHandler.KEYSTORE_PASSWORD_ENCRYPTED = WebAS4SS1
devstage.lambdaEnv.JwtCustomAuthorizer_ReportingAuthorizerHandler.KEYSTORE_S3_REGION = eu-west-1

devstage.lambdaEnv.JwtCustomAuthorizer_ReportingAuthorizerHandler.PUBLIC_KEYSTORE_URLS = s3://rvd-<your_user_name_without_numbers>-keys/<your_user_name_without_numbers>/APU/key.jks;s3://rvd-<your_user_name_without_numbers>-keys/<your_user_name_without_numbers>/APS/key.jks;s3://rvd-<your_user_name_without_numbers>-keys/<your_user_name_without_numbers>/APD/key.jks;s3://rvd-<your_user_name_without_numbers>-keys/<your_user_name_without_numbers>/keys/public.jks
devstage.lambdaEnv.JwtCustomAuthorizer_ReportingAuthorizerHandler.KEYSTORE_PASSWORD_ENCRYPTED = WebAS4SS1
devstage.lambdaEnv.JwtCustomAuthorizer_ReportingAuthorizerHandler.KEYSTORE_S3_REGION = eu-west-1

devstage.lambdaEnv.BindingReportProvider_ApplicationBindingReportGetHandler.AUTH_PASSWORD_ENCRYPTED = serv1c3
devstage.lambdaEnv.BindingReportProvider_ApplicationBindingReportGetHandler.STAGE = #{deploy.stage}
devstage.lambdaEnv.BindingReportProvider_ApplicationBindingReportGetHandler.ENDPOINTURL = https://s3-eu-west-1.amazonaws.com/rvd-<your_user_name_without_numbers>-service-discovery/sd.json
devstage.lambdaEnv.BindingReportProvider_ApplicationBindingReportGetHandler.AUTH_SERVICE = rvdsvc_binding

devstage.lambdaEnv.BindingReportAggregator_BindingAppReportAggregatorHandler.AUTH_PASSWORD_ENCRYPTED = serv1c3
devstage.lambdaEnv.BindingReportAggregator_BindingAppReportAggregatorHandler.STAGE = #{deploy.stage}
devstage.lambdaEnv.BindingReportAggregator_BindingAppReportAggregatorHandler.ENDPOINTURL = https://s3-eu-west-1.amazonaws.com/rvd-<your_user_name_without_numbers>-service-discovery/sd.json
devstage.lambdaEnv.BindingReportAggregator_BindingAppReportAggregatorHandler.AUTH_SERVICE = rvdsvc_binding

devstage.lambdaEnv.BindingReportProvider_GlobalBindingReportGetHandler.AUTH_PASSWORD_ENCRYPTED = serv1c3
devstage.lambdaEnv.BindingReportProvider_GlobalBindingReportGetHandler.STAGE = #{deploy.stage}
devstage.lambdaEnv.BindingReportProvider_GlobalBindingReportGetHandler.ENDPOINTURL = https://s3-eu-west-1.amazonaws.com/rvd-<your_user_name_without_numbers>-service-discovery/sd.json
devstage.lambdaEnv.BindingReportProvider_GlobalBindingReportGetHandler.AUTH_SERVICE = rvdsvc_binding

devstage.lambdaEnv.BindingReportProvider_AccountBindingReportGetHandler.AUTH_PASSWORD_ENCRYPTED = serv1c3
devstage.lambdaEnv.BindingReportProvider_AccountBindingReportGetHandler.STAGE = #{deploy.stage}
devstage.lambdaEnv.BindingReportProvider_AccountBindingReportGetHandler.ENDPOINTURL = https://s3-eu-west-1.amazonaws.com/rvd-<your_user_name_without_numbers>-service-discovery/sd.json
devstage.lambdaEnv.BindingReportProvider_AccountBindingReportGetHandler.AUTH_SERVICE = rvdsvc_binding

devstage.lambdaEnv.BindingReportAggregator_BindingGlobalReportAggregatorHandler.STAGE = #{deploy.stage}
devstage.lambdaEnv.BindingReportAggregator_BindingGlobalReportAggregatorHandler.ENDPOINTURL = https://s3-eu-west-1.amazonaws.com/rvd-<your_user_name_without_numbers>-service-discovery/sd.json
devstage.lambdaEnv.BindingReportAggregator_BindingGlobalReportAggregatorHandler.AUTH_SERVICE = rvdsvc_binding
devstage.lambdaEnv.BindingReportAggregator_BindingGlobalReportAggregatorHandler.AUTH_PASSWORD_ENCRYPTED = serv1c3

devstage.lambdaEnv.BindingReportAggregator_BindingAccountReportAggregatorHandler.STAGE = #{deploy.stage}
devstage.lambdaEnv.BindingReportAggregator_BindingAccountReportAggregatorHandler.ENDPOINTURL = https://s3-eu-west-1.amazonaws.com/rvd-<your_user_name_without_numbers>-service-discovery/sd.json
devstage.lambdaEnv.BindingReportAggregator_BindingAccountReportAggregatorHandler.AUTH_SERVICE = rvdsvc_binding
devstage.lambdaEnv.BindingReportAggregator_BindingAccountReportAggregatorHandler.AUTH_PASSWORD_ENCRYPTED = serv1c3

devstage.lambdaEnv.BillingReportProvider_ExtendedLicensesBillingReportGetHandler.STAGE = #{deploy.stage}
devstage.lambdaEnv.BillingReportProvider_ExtendedLicensesBillingReportGetHandler.ENDPOINTURL = https://s3-eu-west-1.amazonaws.com/rvd-<your_user_name_without_numbers>-service-discovery/sd.json
devstage.lambdaEnv.BillingReportProvider_ExtendedLicensesBillingReportGetHandler.AUTH_SERVICE = rvdsvc_binding
devstage.lambdaEnv.BillingReportProvider_ExtendedLicensesBillingReportGetHandler.AUTH_PASSWORD_ENCRYPTED = serv1c3

devstage.lambdaEnv.BillingReportProvider_NewLicensesBillingReportGetHandler.STAGE = #{deploy.stage}
devstage.lambdaEnv.BillingReportProvider_NewLicensesBillingReportGetHandler.ENDPOINTURL = https://s3-eu-west-1.amazonaws.com/rvd-<your_user_name_without_numbers>-service-discovery/sd.json
devstage.lambdaEnv.BillingReportProvider_NewLicensesBillingReportGetHandler.AUTH_SERVICE = rvdsvc_binding
devstage.lambdaEnv.BillingReportProvider_NewLicensesBillingReportGetHandler.AUTH_PASSWORD_ENCRYPTED = serv1c3

devstage.lambdaEnv.BillingReportAggregator_BillingExtendedReportAggregatorHandler.STAGE = #{deploy.stage}
devstage.lambdaEnv.BillingReportAggregator_BillingExtendedReportAggregatorHandler.ENDPOINTURL = https://s3-eu-west-1.amazonaws.com/rvd-<your_user_name_without_numbers>-service-discovery/sd.json
devstage.lambdaEnv.BillingReportAggregator_BillingExtendedReportAggregatorHandler.AUTH_SERVICE = rvdsvc_binding
devstage.lambdaEnv.BillingReportAggregator_BillingExtendedReportAggregatorHandler.AUTH_PASSWORD_ENCRYPTED = serv1c3

devstage.lambdaEnv.BillingReportAggregator_BillingNewReportAggregatorHandler.STAGE = #{deploy.stage}
devstage.lambdaEnv.BillingReportAggregator_BillingNewReportAggregatorHandler.ENDPOINTURL = https://s3-eu-west-1.amazonaws.com/rvd-<your_user_name_without_numbers>-service-discovery/sd.json
devstage.lambdaEnv.BillingReportAggregator_BillingNewReportAggregatorHandler.AUTH_SERVICE = rvdsvc_binding
devstage.lambdaEnv.BillingReportAggregator_BillingNewReportAggregatorHandler.AUTH_PASSWORD_ENCRYPTED = serv1c3

devstage.lambdaEnv.BillingReportAggregator_BillingGlobalReportAggregatorHandler.STAGE = #{deploy.stage}
devstage.lambdaEnv.BillingReportAggregator_BillingGlobalReportAggregatorHandler.ENDPOINTURL = https://s3-eu-west-1.amazonaws.com/rvd-<your_user_name_without_numbers>-service-discovery/sd.json
devstage.lambdaEnv.BillingReportAggregator_BillingGlobalReportAggregatorHandler.AUTH_SERVICE = rvdsvc_binding
devstage.lambdaEnv.BillingReportAggregator_BillingGlobalReportAggregatorHandler.AUTH_PASSWORD_ENCRYPTED = serv1c3

devstage.lambdaEnv.BillingReportProvider_AccountBillingReportGetHandler.STAGE = #{deploy.stage}
devstage.lambdaEnv.BillingReportProvider_AccountBillingReportGetHandler.ENDPOINTURL = https://s3-eu-west-1.amazonaws.com/rvd-<your_user_name_without_numbers>-service-discovery/sd.json
devstage.lambdaEnv.BillingReportProvider_AccountBillingReportGetHandler.AUTH_SERVICE = rvdsvc_binding
devstage.lambdaEnv.BillingReportProvider_AccountBillingReportGetHandler.AUTH_PASSWORD_ENCRYPTED = serv1c3

devstage.lambdaEnv.BillingReportProvider_GlobalBillingReportGetHandler.STAGE = #{deploy.stage}
devstage.lambdaEnv.BillingReportProvider_GlobalBillingReportGetHandler.ENDPOINTURL = https://s3-eu-west-1.amazonaws.com/rvd-<your_user_name_without_numbers>-service-discovery/sd.json
devstage.lambdaEnv.BillingReportProvider_GlobalBillingReportGetHandler.AUTH_SERVICE = rvdsvc_binding
devstage.lambdaEnv.BillingReportProvider_GlobalBillingReportGetHandler.AUTH_PASSWORD_ENCRYPTED = serv1c3

devstage.lambdaEnv.BillingReportAggregator_BillingAccountReportAggregatorHandler.STAGE = #{deploy.stage}
devstage.lambdaEnv.BillingReportAggregator_BillingAccountReportAggregatorHandler.ENDPOINTURL = https://s3-eu-west-1.amazonaws.com/rvd-<your_user_name_without_numbers>-service-discovery/sd.json
devstage.lambdaEnv.BillingReportAggregator_BillingAccountReportAggregatorHandler.AUTH_SERVICE = rvdsvc_binding
devstage.lambdaEnv.BillingReportAggregator_BillingAccountReportAggregatorHandler.AUTH_PASSWORD_ENCRYPTED = serv1c3
```

To deploy, execute in Reporting:

1. From Reporting root folder run the following

````bash
 npm install
````
2. Copy the folder test inside the deployment folder, (Reporting->deployment->Reporting->stages->test) and rename it with the <your_user_name_without_numbers>. Update the files
    *cloudformation.properties
    *stageVariables.properties
    *all files inside the lambda-environment folder
with the developers stage information.

````bash
 ./gradlew <your_user_name>Stage deployApi --parallel
````

### Upload ApiDoc

To upload ApiDoc execute in Reporting: (needs to be run together with `<your_user_name>Stage` task)

    ./gradlew <your_user_name>Stage uploadApiDoc

Link to the Reporting ApiDoc for test stage:

[Reporting ApiDoc](http://rvd-reporting-test-api-doc.s3-website-eu-west-1.amazonaws.com/reporting/index.html)

In order to have individual developer ApiDoc:

* execute above sequence of tasks
* for the S3 `rvd-reporting-<your_user_name>-api-doc` created,
needs to be set some "Bucket Policy" (especially GetObject) which are found under "Permissions" tab of the bucket.
* under "Properties" tab needs to be set this bucket as a host Website

## Service Discovery is used

 To be able to have your individual developer Service Discovery configuration necessarily for `~/.gradle/gradle.properties`, you have to create the `sd.json` file manually (for the moment).

 As a template you can use this: `https://s3-eu-west-1.amazonaws.com/rvd-rahu-service-discovery/sd.json`.
 Please replace the endpoints that you need with your individual developer ones.
 NOTE: "reporting" and "events" have the same endpoint

 Another alternative is to create a `sd.json` template file under the `resources` folder in the root folder. To make this approach more general, this template should contain instead of the api ids, variables that are defined in the `~/.gradle/gradle.properties` file mentioned above.
 * e.g. The file content should look like this: (awsGatewayId represents the reporting api id)

```javascript
     {
    "apd": {
        "endpoint": ""
    },
    "aps": {
        "endpoint": "https://${masterDataAwsGatewayId}.execute-api.eu-west-1.amazonaws.com/${stagePrefix}"
    },
    "binding": {
        "endpoint": ""
    },
    "dcs": {
        "endpoint": ""
    },
    "hdp": {
        "endpoint": ""
    },
    "hdu": {
        "endpoint": ""
    },
    "master_data": {
        "endpoint": "https://${masterDataAwsGatewayId}.execute-api.eu-west-1.amazonaws.com/${stagePrefix}"
    },
    "reporting": {
        "endpoint": "https://${awsGatewayId}.execute-api.eu-west-1.amazonaws.com/${stagePrefix}"
    },
    "vdc": {
        "endpoint": ""
    },
    "events": {
        "endpoint": "https://${awsGatewayId}.execute-api.eu-west-1.amazonaws.com/${stagePrefix}"
    },
    "reports": {
        "endpoint": "https://${awsGatewayId}.execute-api.eu-west-1.amazonaws.com/${stagePrefix}"
    }
}
```

Next, in `build.gradle`, the variable `ext.serviceDiscoveryS3Bucket` contains the value of the s3 bucket where de `sd.json` file is uploaded. In order to verify if the content of the file is correct, the task `setupServiceDiscovery` has to be run, and the resulted file can be found under the `build` folder. If every value is set up, the task that has to be executed in order to have the file uploaded is `deployServiceDiscovery`.

* e.g. `gradlew <your_user_name>Stage deployServiceDiscovery`

## Definition of Done / Checklist for Review (see [PULL_REQUEST_TEMPLATE.md](.github/PULL_REQUEST_TEMPLATE.md)):

- [ ] Requirements were added to `RVD/Reporting/doc/spec/readme.md`,
- [ ] the Swagger API definitions were updated,
- [ ] the `JwtCustomAuthorizer` was extended with the required paths/permissions,
- [ ] a reasonable number of unit tests exist for the implementation,
- [ ] a reasonable number of integration tests exist,
- [ ] a reasonable number of system tests cover the feature,
- [ ] all tests are green,
- [ ] no new Sonar issues were introduced by the implementation,
- [ ] links for requirements tracing were added where needed,
- [ ] the requirements tracing report shows a sufficient coverage of the feature,
- [ ] the architecture description was updated where needed,
- [ ] the review preparation document was updated.

## Release Procedure

Goal: Build artifacts required for a delivery from a tag and deploy it on the test stage.

1. Check [Reporting_test](https://rvd-jenkins.ebcloud.eu/job/Reporting_test/) is OK
1. Check Requirements coverage 100%
1. Check [Sonar](https://rvd-sonar.ebcloud.eu/overview?id=com.elektrobit.rvd%3AReporting) has 0 issues
1. Execute [Reporting_release](https://rvd-jenkins.ebcloud.eu/job/Reporting_release/) for the Git hash that you want to release. The release will be deployed first on the test stage, all tests including system tests are executed here.
1. If the release build was successful, create a tag for the selected Git hash on [GitHub](../../releases).

All released artifacts are available on S3 in [`rvd-releases/Reporting/<version>`](https://console.aws.amazon.com/s3/home?region=eu-west-1#&bucket=rvd-releases&prefix=RvdRelease/).

## Deployment Procedure

Goal: Deploy a released version on the prelive/prod stage.

1. Make sure the software you want to deploy is already released with a version number.
1. When deploying to prelive using CodeBuild, update first the 'componentVersion' value in stageVariables
1. Execute steps described in  [Deployment](https://collaboration.asw.zone/display/PRJRVD/Deployment) with the release package you want to deploy on prelive/prod.
1. Update [Roll-out Matrix](https://collaboration.asw.zone/display/PRJRVD/Roll-out+Matrix)

## Delivery Procedure

Goal: Deliver a released version in the defined [delivery package format](https://collaboration.asw.zone/display/PRJRVD/Contents+and+acceptance+criteria+of+a+delivery) to the official S3 bucket for integration.

1. Make sure the software you want to deliver is already released with a version number.
1. Execute [Reporting_deliver](https://rvd-jenkins.ebcloud.eu/job/Reporting_deliver/) with the version number of the release you want to deliver.
1. Deliver the change log manually according to https://collaboration.asw.zone/display/PRJRVD/Contents+and+acceptance+criteria+of+a+delivery

```bash
aws s3 --profile rvd-incoming cp changelog-reporting-x.y.z.txt s3://rvd-incoming/Elektrobit/Reporting/releases/x.y.z/
```
