# Challenge 0: Pre-requisites - Ready, Set, GO! 

**[Home](../README.md)** - [Next Challenge >](./01-containers.md)

## Introduction

A smart cloud solution architect always has the right tools in their toolbox. 

## Description

In this challenge we'll be setting up all the tools we will need to complete our challenges.

- Make sure that you have joined the Teams group for this track. The first person on your team at your table should create a new channel in this Team with your team name.
- Create a Resource Group, Storage account, and access Cloud Shell
- Clone the repo down to your storage account
- Deploy the build machine VM
- **NOTE:** You can start the next challenge even if this one is still running by using the Azure Cloud Shell.
- **Tip:** You can complete almost all of the challenges with the Azure Cloud Shell!  But be a good cloud architect and make sure you have experience installing the tools locally.

- Create your student Resource Group
    - Log into **`https://portal.azure.com`** with your student credentials.
    - Click the hamburger menu (3 horizontal bars) in the upper left corner, then click Resource Groups.
    - Click the **+ Create** button in the upper left
    - For Subscription, select **SUBSCRIPTION_NAME_HERE**
    - For Resource group, enter **RG-WTHyourname**
    - For Region, select the region geographically closest to you.  Remember this region because you will use it throughout the workshop.
    - Click the **Review + create** button at the bottom of the page.
    - Validate the values you've entered are correct, then click **Create** at the bottom

- Create a storage account to use with Cloud Shell
    - In the Azure Portal, click to open your newly create Resource Group from the step above.
    - Click the **+ Create** button in the upper left
    - In the search box, type "storage account" and hit enter
    - In the box for "Storage account" by "Microsoft" click the link to **Create**, then select **Storage accunt**
    - For Subscription, select **SUBSCRIPTION_NAME_HERE**
    - For Resource group, enter **RG-WTHyourname**
    - For Storage account name, enter (all lower case) wthyournamestor01
    - For Region, select the same region you used to create the Resource Group.
    - For Performance, select **Standard**
    - For Redundancy, select **Locally-redundant storage (LRS)**
    - Click **Review + create** at the bottom to skip the remaining options for now.
    - Validate the values you've entered are correct, then click **Create** at the bottom.

- Open Cloud Shell
    - Click the Cloud Shell icon at the top right of the Azure Portal **>_**
    - Click **Bash** at the **Welcome to Azure Cloud Shell** page.
    - Click **Show advanced settings**
    - For Subscription, select **SUBSCRIPTION_NAME_HERE**
    - For Cloud Shell region, select the same region you used to create the storage account and Resource Group.
    - For Resource group, select **Use existing** and choose **RG-WTHyourname**
    - For Storage account, select **Use existing** and choose the storage account you just created.
    - For File share, select **Create new** and enter your username
    - Click **Create storage** button at the bottom
    - In a moment, you should be logged into your cloud shell session and you should see something similar to the following:
    **`Requesting a Cloud Shell.Succeeded.`**
    **`Connecting terminal...`**

    **`Welcome to Azure Cloud Shell`**

    **`Type "az" to use Azure CLI`**
    **`Type "help" to learn about Cloud Shell`**

    **`Student01@Azure:~$`**

- Clone this repo to your storage account
    - At the cloud shell prompt, type **`cd clouddrive`**
    - At the cloud shell prompt, type **`git clone https://github.com/dsmithcloud/WhatTheHack.git`**


- Deploy build machine VM with Linux + Docker using provided ARM Template
    - At the cloud shell prompt, type **`cd WhatTheHack/001-IntroToKubernetes/Student/Resources/Challenge\ 1/build-machine`**
	- **`az deployment group create -g <rgname> -n <deploymentName> --template-file docker-build-machine-vm.json --parameters docker-build-machine-vm.parameters.json`**
- When prompted provide an admin password for your VM.  **DON'T FORGET THE PASSWORD!**
- SSH into the build machine on port 2266 on the public IP of the VM
	- **`ssh -p 2266 wthadmin@12.12.12.12`**
- Get the Fab Medical code from the Student Resources folder for Challenge 1
	- **NOTE:** The FabMedical code files are pre-loaded onto the Linux VM created by the ARM template + script.
- Run the Fab Medical application locally on the VM & verify access
	- Each part of the app (api & web) runs independently.
	- Build the API app by navigating to the content-api folder and run:
    	- `npm install`
	- To start a node app, run:
        - `node ./server.js &`
	- Verify the API app runs by browsing to its URL with one of the three function names, eg: 
    	- `http://localhost:3001/speakers`
	- Repeat for the steps above for the Web app.
	- **NOTE:** The content-web app expects an environment variable named **CONTENT_API_URL** that points to the API app’s URL.
	- The environment variable value should be `http://localhost:3001`
	- **NOTE:** **localhost** only works when both apps are run locally using Node. You will need a different value for the environment variable when running in Docker.
	- **NOTE:** The node processes for both content-api and content-web must be stopped before attempting to run the docker containers in the next step. To do this, use the Linux `ps` command to list all processes running, and then the Linux `kill` command to kill the two Node.js processes.
	- **NOTE:** If you are not familiar with Node.js, find a proctor to help you through this part.
- Dockerfiles for both content-api and content-web are in the Coach Solutions folder for Challenge 1
	- The value of the env URL for content-web should match whatever value is used for the --name parameter when executing docker run on content-api as seen below.
- Build Docker images for both content-api & content-web. 
	- `docker build –t content-api .`
	- `docker build –t content-web .`
- Run the applications in the Docker containers in a network and verify access
	- Create a Docker network named **fabmedical**: 
		- `docker network create fabmedical`
	- Run each container using a name and using the **fabmedical** network. The containers should be run in "detached" mode so they don’t block the command prompt.
		- `docker run -d -p 3001:3001 --name api --net fabmedical content-api`
		- `docker run -d -p 3000:3000 --name web --net fabmedical content-web`
	- **NOTE:** The value specified in the `--name` parameter of the `docker run` command for content-api will be the DNS name for that container on the docker network.  Therefore, the value of the **CONTENT_API_URL** environment variable in the content-web Dockerfile should match it.
	- This is a good time for coaches to discuss the concept of a software defined network within the docker engine.  Explain how if there are more than one container listening on the same port, docker provides a network abstraction layer and the ability to map ports from the VM to ports on the container. For example, two containers listening on port 3001. Docker can map one to the VM’s port 3001 and the other to the VM’s port 3005.
- Be familiar with Docker commands and ready to help attendees who get stuck troubleshooting:
	- `docker ps `
		- lists all container processes running
	- `docker rm `
    	- removes/deletes an image
	- `docker kill `
    	- kills a container
	- `docker image list `
    	- lists all images on the machine
	- `docker image prune `
    	- kills all dangling images
- `sudo netstat -at | less` is useful to see what ports are running. This may help students with troubleshooting.


## Success Criteria

1. You have a bash shell at your disposal (WSL, Mac, Linux or Azure Cloud Shell)
1. Running `az --version` shows the version of your Azure CLI
1. Browsing to http://<public-ip-of-build-machine>:3000 produces the Contoso Neuro 2017 conference website
