[Go to Overview Page](README.md)

![](images/customer.logo2.png)

# Microservices on ATP


## Part 4: Data Loading into ATP
#### **Introduction**

In this lab, you will be creating a few tables and inserting data into the ATP database using the CI/CD features of Developer Cloud.  We'll use the Build engine of DevCS to set up a flow that will create the necessary objects in the database, and insert data into the tables.  In case these elements are changed in the repository, the script will trigger again and re-create the database elements.

In real life, you would want to set up a more sophisticated logic to manage your database objects, see [these blogs on the topic by Shay Schmeltzer](https://blogs.oracle.com/shay/devcs).



#### **Objectives**

- Set up your ATP Wallet in Developer Cloud
- Create and run a Build to create your database objects
- Validate reation via SQLDeveloper



## Steps

### STEP 1: Set up your ATP Wallet in Developer Cloud

- In the ATP Connection For this lab, you downloaded the ATP Connection wallet zip file.  On your laptop, move this file into the folder "ATPDocker" you created when you cloned the git repository.

- Unzip the file, but leave the original zip file in the same location.  You will be needing both the .zip fil as well as the unzipped directory.
- Example result for an ATP database named "ATP2":
- ![](./images/400/wallet.png)

- On the command line, add the new files to the git repository, commit them and push them to the Developer Cloud with the following commands :

```bash
git add .
git commit -m "Add wallet"
git push
```



- Your wallet is now visible in Developer Cloud - you might have to refresh your browser window to see the changes

![](./images/400/wallet_added.png)



### **STEP 2: Create and load your data in the database**

- In Developer Cloud, navigate to the "Builds" tab and select **+Create Job**.
  - Enter a name : **CreateDBObjects**
  - Select the Software Template you created, for example **OKE**
  - Hit **Create Job**

![](./images/400/new_job.png)



- Add a  GIT Source repository

![](./images/400/add_src.png)

- Select your repository from the list
- Do **not** select the Automatic build on Commit



![](./images/400/config_source.png)



- Select the tab **Steps** to add a **SQLcl** build step from the dropdown

 ![](./images/400/add_step.png)



- Fill in the parameters:
  - username of the ATP instance : **admin**
  - password of the ATP instance
  - your wallet .zip file
  - your connect string, for example **atp2_high**, where atp2 is the name of the database in this example
  - the sql file containing the create script: **aone/create_schema.sql**



![](./images/400/step_details.png)

 -   Now save your Build Config and hit the **Build Now** button.  After a successfull build you should see following screen :

![](./images/400/build_result.png)

- You can check the detailed content of the SQL execution in the log file of the build job.

![](./images/400/log_file.png)

- You can now re-connect with SQLDeveloper to your database and verify the objects were created correctly.



### **STEP 3: Set up a DeleteDBObjects job** and automate a Pipeline

- Repeat the steps from the last step to create a second job, called **DeleteDBObjects**.  When hitting the **Create Job** button, you can choose **Copy Existing Job** and select your CreateDBObjects Job.  
- Now just change the script to execute in the DeleteDBObjects job : change **aone/create_schema.sql** into **delete_schema.sql**.
- Run your DeleteDbObjects job manually to check it is working as expected.
- Now go to the "Pipeline" tab and create a new pipeline called **DBObjects**
- Drag and drop first the DeleteDBObjects job, then the CreateDBObjects job onto the canvas, and link them together.  
- You can now edit the DeleteDBObjects to trigger automatically when a change in the repository is detected.  This will trigget the pipeline, recreating the DB objects.



- You are now ready to move to the next lab.





------

[Go to Overview Page](README.md)

