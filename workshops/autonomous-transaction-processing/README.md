[Go to the Cloud Test Drive Welcomer Page](https://github.com/CloudTestDrive/EventLabs/blob/master/README.md)

![](images/customer.logo2.png)

# Microservices on Kubernetes and Autonomous Database

## Setting up a CI/CD environment for developing Microservices on an ATP Database, with Developer Cloud

## Introduction

This lab will walk you through the steps to set up a CI/CD environment for developing Microservices, based on the automation possible in Developer Cloud and deploying all components on Oracle's Managed Container platform and the ATP database.

## Prerequisites

To run these labs you will need access to an Oracle Cloud Account.  If you are participating in a live event, your instructor will provide you the required credentials.

If you are running these labs on your own, please check out the instructions on the [Oracle Cloud Adventure page](https://cloudtestdrive.github.io/Trial.html) to learn how to get a [Trial account](https://myservices.us.oraclecloud.com/mycloud/signup?sourceType=:ex:tb:::RC_EMMK181016P00010:Virtual_WS_DEV&SC=:ex:tb:::RC_EMMK181016P00010:Virtual_WS_DEV&pcode=EMMK181016P00010) or how to set up your corporate UC subscription for this lab.

#### **Preparation steps for this lab exercise - *<u>only for personal tenancies</u>***

In order to run this lab, you need to have a running instance of the Developer Cloud Service and an OKE Container Cluster in your cloud tenancy.  In case you are executing this lab on an environment provided by an instructor, this setup will most likely have been performed already.

In case you are running this lab on your own Cloud Tenancy, you might need to go through the following step:

- Setting up a Developer Cloud Instance: [click here for a guide](devcsconfig.md) describing these steps in detail.



## Components of this lab

This lab is composed of the steps outlined below.  Please walk through the various labs in a sequential order, as the different steps depend on each other:

- **Part 1:** [Provisioning an Autonomous Transaction Processing Database Instance](LabGuide100ProvisionAnATPDatabase.md)  using the OCI Console (manual).

  Note: Creation of the ATP via Terraform is also an option.   Detailed instructions will be added in the next iteration

- **Part 2:** [Connecting to your Database](LabGuide200SecureConnectivityAndDataAccess.md) using the secure wallet

- **Part 3:** [Setting up your Developer Cloud for this project](LabGuide250Devcs-proj.md)

- **Part 4:** [Create and populate the Database objects](LabGuide400DataLoadingIntoATP.md) in your ATP database with Developer Cloud

- *Optional Part 5* : [Configure an OCI Compute Instance and set up a node.js application](LabGuide500Configurenode.jsAppWithATP.md) to connect to the ATP database
- *Optional Part 6* : [Configure an OCI Compute Instance and set up Java with ATP:](LabGuide600ConfigureJavaAppWithATP.md) Learn how to build a linux Java application server and connect it to an Oracle ATP database service
- **Part 7:** [Build a Container image with the aone application runing on ATP](LabGuide650BuildDocker.md)
- **Part 8:** [Spin up a Managed Kubernetes environment with Terraform](LabGuide660OKE_Create)
- **Part 9:** [Deploy your container on top of your Kubernetes Cluster](LabGuide670DeployDocker)

- *Optional Part 10* : [Working with REST APIs](LabGuide700WorkingWithRESTAPIs.md): generate REST calls to the Oracle Cloud Infrastructure using node.js

---



[Go to the Cloud Test Drive Welcomer Page](https://github.com/CloudTestDrive/EventLabs/blob/master/README.md)