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

## Lab Instructions

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

- Deploy an Azure VM using provided ARM Template and parameters file
	- The template deployment will ask you to provide an admin password for the VM. The 12-character password must meet 3 out of 4 of these criteria:
	 	- Have lower characters
		- Have upper characters
		- Have a digit
		- Have a special character 
    - At the cloud shell prompt, type **`cd WhatTheHack/001-IntroToKubernetes/Student/Resources/Challenge\ 1/build-machine`**
	- **`az deployment group create -g <rgname> -n <deploymentName> --template-file docker-build-machine-vm.json --parameters docker-build-machine-vm.parameters.json`**
- When prompted provide an admin password for your VM.  **DON'T FORGET THE PASSWORD!**
- SSH into the build machine on port 2266 on the public IP of the VM
	- **`ssh -p 2266 wthadmin@<Public IP of VM>`**


## Success Criteria

1. You have a storage account to use with Azure Cloud Shell
2. You have a bash shell at your disposal (WSL, Mac, Linux or Azure Cloud Shell)
3. You have successfully cloned the workshop materials repo to your clouddrive
4. The build vm is running and you can successfully SSH to it.

**[Home](../README.md)** - [Next Challenge >](./01-containers.md)