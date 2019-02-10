[Go to the Cloud Test Drive Welcomer Page](https://github.com/CloudTestDrive/EventLabs/blob/master/README.md)

![](images/customer.logo2.png)

# Microservices on Kubernetes and Autonomous Database

## Setting up a CI/CD environment for developing Microservices on an ATP Database, with Developer Cloud

## Introduction

This lab will walk you through the steps to set up a CI/CD environment for developing Microservices, based on the automation possible in Developer Cloud and deploying all components on Oracle's Managed Container platform and the ATP database.

## Prerequisites

To run these labs you will need access to an Oracle Cloud Account.  If you are participating in a live event, your instructor will provide you the required credentials.

If you are running these labs on your own, please check out the instructions on the [Oracle Cloud Adventure page](https://cloudtestdrive.github.io/Trial.html) to learn how to get a [Trial account](https://myservices.us.oraclecloud.com/mycloud/signup?sourceType=:ex:tb:::RC_EMMK181016P00010:Virtual_WS_DEV&SC=:ex:tb:::RC_EMMK181016P00010:Virtual_WS_DEV&pcode=EMMK181016P00010) or how to set up your corporate UC subscription for this lab.

### Preparation steps for this lab exercise - *<u>only for personal tenancies</u>*

In order to run this lab, you need to have a running instance of the Developer Cloud Service and an OKE Container Cluster in your cloud tenancy.  In case you are executing this lab on an environment provided by an instructor, this setup will most likely have been performed already.

In case you are running this lab on your own Cloud Tenancy, you might need to go through the following steps:

- Setting up a Developer Cloud Instance: [click here for a guide](devcsconfig.md) describing these steps in detail.
- Setting up a Container Cluster (OKE): [detailed instructions can be found on this location](tbd)



## Components of this lab

This lab is composed of the steps outlined below.  Please walk through the various labs in a sequential order, as the different steps depend on each other:

- [Provisioning an Autonomous Transaction Processing Database Instance](LabGuide100ProvisionAnATPDatabase.md)  using the OCI Console (manual).

  Note: Creation of the ATP via Terraform is also an option.   detailed instructions will be added in the next iteration*

- [Connecting to your Database](LabGuide200SecureConnectivityAndDataAccess.md) using the secure wallet

- [Setting up your Developer Cloud for this project](LabGuide250Devcs-proj.md)







---

---






## Lab 4: Data Loading into ATP

**Key Objectives**:

- Learn how to use the SQL Developer Data Import Wizard
- Learn how to upload files to the OCI Object Storage
- Learn how to define object store credentials for ATP
- Learn how to create tables in your database
- Learn how to load data from the Object Store

**[Click here to run Lab 4](LabGuide400DataLoadingIntoATP.md)**

## Lab 5: Configure node.js app with ATP

**Key Objectives**:

- Learn how to build a linux node.js application server and connect it to an Oracle ATP database service

**[Click here to run Lab 5](LabGuide500Configurenode.jsAppWithATP.md)**

## Lab 6: Configure Java with ATP

**Key Objectives**:

- Learn how to build a linux Java application server and connect it to an Oracle ATP database service

**[Click here to run Lab 6](LabGuide600ConfigureJavaAppWithATP.md)**

## Lab 7: Working with REST APIs

**Key Objectives**:

- Learn how to generate REST calls to the Oracle Cloud Infrastructure using node.js

**[Click here to run Lab 7](LabGuide700WorkingWithRESTAPIs.md)**

## Lab 8: Building microservices on ATP

**Key Objectives**:

- To build a docker container running node.js microservice
- Deploy it on an ATP service

**[Click here to run Lab 8](LabGuide800BuildingMicroservicesOnATP.md)**

## Lab 9: Configure OCI-CLI

**Key Objectives**:

- Configure Oracle Cloud Infrastructure Command Line Interface
- Run examples using OCI-CLI for Autonomous Transaction Processing database

**[Click here to run Lab 9](LabGuide900ConfigureOCI-CLI.md)**


## Lab 10: Mastering DevOps in the Oracle Cloud

**Key Objectives**:

- Connect Oracle ATP to Python
- Connect Oracle ATP to Java
- Connect Oracle ATP to Node
- Utilize Terraform to control ATP
- Utilize OCI-CLI to control ATP

**[Click here to run Lab 11](LabGuide1000AppDev.md)**

## Appendix

**Key Objectives**:

- Handy docker commands you may need

**[Click here to go through Appendix](Appendix.md)**



---

[Go to the Cloud Test Drive Welcomer Page](https://github.com/CloudTestDrive/EventLabs/blob/master/README.md)
