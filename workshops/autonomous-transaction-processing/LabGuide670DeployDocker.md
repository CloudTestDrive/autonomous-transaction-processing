[Go to Overview Page](README.md)

![](images/customer.logo2.png)
# Microservices on ATP

## Part 7: Deploy your container on top of your Kubernetes Cluster

#### **Introduction**

In this section we will create a second build job to run the container we created on the Kubernetes Cluster we set up.

Let’s get started! 

### Step 1: Set up your Deploy Build Job

- Navigate to the **Build** tab and hit the **New Job** button.

  - Enter a name, for example OKEDeploy
  - Select your build template, we named it DockerOCIOKE in the previous steps

  ![](images/670/im47.png)

  - Now hit  **Create Job**, and the Job Configuration dialog will pop up. 

- In the Source Control tab, select your git repository.

  ![](images/670/im48.png)

  - Do **not** select the "Automatically perform Build" option for this job, we will link it with the previous job using a pipeline.

- In the Builders tab, add the following Builder steps:

  - Docker Login : use the predefined Repository definition **MyOCIR** as you did in the previous job

  - Unix Shell Builder:

    - launch the script "my script.sh" that is in your repository.  We will edit this script after completing the Build definition to adapt it to your needs.

      ``bash -ex kubescript.sh``

  ![](images/670/im50.png)

- You have finished setting up the Build job !

  ==> Don't forget to **Save** the job !

  

### Step 2: Configure the environment to point to your cloud instance

- Upload the kubeconfig file into the repository.  During the creation of the cluster, a file called **mykubeconfig** was generated.  This file is required to connect to your cluster from within the build job.

  - Copy the file in the home directory of your ATPDocker repository

  - Perform the usual git commands to sync your Developer git repository:

    ```bash
    git add mykubeconfig
    git commit -m "Add kubeconfig"
    git push
    ```

- In the **Git** tab of Developer Cloud, open the file **atp2.yaml**.  This is the deployment profile of your container on the Cluster.  You need to make following changes:

  - Line 17: set the correct image location as you configured it in the BuildContainer job

  - Example for datacenter in Frankfurt (**fra**), tenancy name **mytenancy**, repo path **oowhol** and image name joduatp2:latest container name: 

    `fra.ocir.io/mytenancy/oowhol/joduatp2:latest`

    ![](images/670/edit_yaml.png)

  - Use the **Commit** button to save your changes.

  

### Step 3: ***Optional*** - Personalize the deployment on the cluster

<u>In case you are sharing an instance with other participants</u>, you need to make sure your deployment can be distinguished from the ones belonging to your colleagues.  You can perform the below steps to achieve this:

- In the **Git** tab of Developer Cloud, re-open the file **atp2.yaml**.  You need to make following extra changes:

  - Line 4, 8, 13, 16, 25 and 33 : replace the string **atp2** with a string containing your initials, for example for "jle" : **jle-atp2**

  ![](images/670/edit_yaml2.png)

  - Hit **Commit** to save your changes.

  

- In the **Git** tab of Developer Cloud, open the file **kubescript.sh** by clicking on it, and go into editing mode by clicking on the small pencil in the upper right

  - On line 4 and 6, add your initials in front of the strings beginning with **atp2**
  - ![](images/670/kubescript.png)
  - Hit **Commit** to save the changes
  - As you can see, this shell script refers to the actual Kubernetes deployment configuration file **atp2.yaml**.  

### Step 4: Execute and validate your new job

- In the **Builds** menu, select the job you just created and hit the **Build Now** button.

- Wait for the job to finish, then check the build log:

  ![](/Users/jleemans/dev/github/EventLabs/AppDev/devcs-docker/images/image067.png) 

- Inspect the build job log file to validate correct execution

  - **ATTENTION : image to be updated**

  ![](images/670/log_deploy.png)

- Although we included a few commands in the build job to show the resulting state of the cluster, the best way to visualize this is by launching the **kubernetes Dashboard**.  This is explained in the next step.

### Step5: Installing Kubectl

This step covers how to install the Kubernetes command line interface and connect to your Kubernetes cluster

Choose the section that corresponds to your machine:

#### **MacOS**

Download the latest release with the following `curl` command:

```
$ curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/darwin/amd64/kubectl
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 49.9M  100 49.9M    0     0  4289k      0  0:00:11  0:00:11 --:--:-- 4150k
```

Make the kubectl binary executable.

```
$ chmod +x ./kubectl
```

Move the binary in to your PATH.

```
$ mv ./kubectl /usr/local/bin/kubectl
```

Verify the installation using the version command.

```
$ kubectl version
Client Version: version.Info{Major:"1", Minor:"8", GitVersion:"v1.8.4", GitCommit:"9befc2b8928a9426501d3bf62f72849d5cbcd5a3", GitTreeState:"clean", BuildDate:"2017-11-20T05:28:34Z", GoVersion:"go1.8.3", Compiler:"gc", Platform:"linux/amd64"}
The connection to the server localhost:8080 was refused - did you specify the right host or port?
```

At this step the server connection failure is normal. For easier usage it is recommended to setup the autocomplete for bash.

```
$ source <(kubectl completion bash)
```

#### **Linux machines**

For Linux, use the same sequence as described above for Linux, only replace the CURL command with the following:

```
$ curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 49.9M  100 49.9M    0     0  4289k      0  0:00:11  0:00:11 --:--:-- 4150k
```

 Note the difference: you are using /bin/linux/... instead of /bin/darwin/...  

#### **Windows**

To find out the latest stable version take a look at <https://storage.googleapis.com/kubernetes-release/release/stable.txt>

For example if latest stable version is: **v1.8.4** then construct the download link in the following way: *https://storage.googleapis.com/kubernetes-release/release/VERSION_NUMBER/bin/windows/amd64/kubectl.exe*. Thus in case of **v1.8.4** the link looks like this:

<https://storage.googleapis.com/kubernetes-release/release/v1.8.4/bin/windows/amd64/kubectl.exe>

Once you have the executable binary add to your PATH variable.

```
set PATH=%PATH%;c:\download_folder\kubectl.exe
```

Verify the installation using the version command.

```
C:\Users\pnagy>kubectl version
Client Version: version.Info{Major:"1", Minor:"7", GitVersion:"v1.7.0", GitCommit:"d3ada0119e776222f11ec7945e6d860061339aad", GitTreeState:"clean", BuildDate:"2
017-06-29T23:15:59Z", GoVersion:"go1.8.3", Compiler:"gc", Platform:"windows/amd64"}
Unable to connect to the server: dial tcp 192.168.99.100:8443: connectex: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.
```

------

### Step 6: Verifying the installation

After the successful installation you need to get the kubeconfig configuration file that belongs to your cluster. This file has been generated during the terraform setup of your cluster.

- Copy the file to a location on your local machine (for example the "Downloads" folder)

The *kubeconfig* file contains the necessary details and parameters to connect to Oracle Container Engine (Kubernetes cluster). The *clusters* parameter defines the available clusters. 

When you execute a `kubectl` command first it tries to read the default configuration file: *config* file from default location. On Linux it is `~/.kube` and on Windows it is `c:\Users\<USERNAME>\.kube`. But you can store *config* file at different path and even with different name e.g.*kubeconfig*. Just set the configuration file location as KUBECONFIG environment variable in your command line terminal where you want to execute `kubectl` commands.

Linux & MacOS:

```
export KUBECONFIG=~/Downloads/kubeconfig
```

Windows:

```
set KUBECONFIG=c:\Downloads\kubeconfig 
```

Now `kubectl` is ready to use. Test again using the version option.

```
$ kubectl version
Client Version: version.Info{Major:"1", Minor:"8", GitVersion:"v1.8.4", GitCommit:"9befc2b8928a9426501d3bf62f72849d5cbcd5a3", GitTreeState:"clean", BuildDate:"2017-11-20T05:28:34Z", GoVersion:"go1.8.3", Compiler:"gc", Platform:"linux/amd64"}
Server Version: version.Info{Major:"1", Minor:"7+", GitVersion:"v1.7.4-2+af88312fe58fec", GitCommit:"af88312fe58fec576aed346d707bf58f0132ef2a", GitTreeState:"clean", BuildDate:"2017-10-24T20:06:27Z", GoVersion:"go1.8.3", Compiler:"gc", Platform:"linux/amd64"}
$ 
```

Check the output, now it has to contain the server version information.

### Step 7: Kubectl Web UI (dashboard)

Dashboard is a web-based Kubernetes user interface what is deployed by default on Oracle Container Engine. You can use Dashboard to deploy containerized applications to a Kubernetes cluster, troubleshoot your containerized application, and manage the cluster itself along with its attendant resources. You can use Dashboard to get an overview of applications running on your cluster, as well as for creating or modifying individual Kubernetes resources (such as Deployments, Jobs, DaemonSets, etc).

You can access Dashboard using the kubectl command-line tool by running the following command:

```
$ kubectl proxy
Starting to serve on 127.0.0.1:8001
```

This command runs `kubectl` in a mode where it acts as a reverse proxy. It handles locating the apiserver and authenticating and make Dashboard available at the following link:

<http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/#%21/overview?namespace=default>.

For older versions of K8S, you might have to use this URL: <http://localhost:8001/ui>. Please note the UI can only be accessed from the machine where the proxy command is running.

The default port used by the proxy command is port 8001. If on your laptop this port is already in use by another application you can easily specify to use another port using following syntax:

```
kubectl proxy --port=8333
```

You will be asked to provide the kubeconfig file before you can access the console.

- Choose the Kubeconfig option
- Click on the "Choose kubeconfig file" area and select the kubeconfig file you have downloaded on your machine
- Click "Sign In"

[![alt text](https://github.com/CloudTestDrive/EventLabs/raw/master/AppDev/K8S/images/kubeproxy.png)](https://github.com/CloudTestDrive/EventLabs/blob/master/AppDev/K8S/images/kubeproxy.png)

REMARK: the screen you will get might look slightly different, as this depends on the state of the cluster you are visualizing.

[![alt text](https://github.com/CloudTestDrive/EventLabs/raw/master/AppDev/K8S/images/wercker.application.31.png)](https://github.com/CloudTestDrive/EventLabs/blob/master/AppDev/K8S/images/wercker.application.31.png)



### Step 8: Visualize the Service to obtain the URL of your application

In oder to see the application you just deployed, we need to construct the URL where the container is listening.  Do do this : 

- Navigate to the **Services** menu

- Click on the service called either **atp2** or **(your initials)-atp2**

- Here you can see the IP address and port where your application is running.  In the below example, you can enter the following URL to reach your application

  http://130.61.18.58:32163

  ![alt text](images/670/service_detail.png)

- When you enter this URL in your browser, you should see the below result:

![alt text](images/670/result.png)





You have finished this part of the lab, navigate to the next step to continue!



---
[Go to Overview Page](README.md)