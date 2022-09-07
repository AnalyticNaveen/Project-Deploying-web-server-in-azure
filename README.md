# Azure Infrastructure Operations Project: Deploying a scalable IaaS web server in Azure

## Introduction

### In this project we are deploying a scalable web server with load balancer.

The project will consist of the following main steps :-

1. Creating a tagging-policy
2. Creating a Packer image
3. Creating a Terraform templet
4. Deployinf the infrastructure 
5. Creating a Readme file

## Getting Started 

You need understanding of Terraform commands
You need Understanding of Packer commands
You need Understanding of Azure CLI 

## Dependencies

1. Create an Azure Account
2. Install the Azure command line interface
3. Install Packer
4. Install Terraform

## Instructions 

### Creating a tagging-policy

We will 1st create a policy that will allow creation of only those resources which has tags.

To create this policy we will use CLI command 

```bash
AZ Policy 
```
We will create our policy in "json" file . For this project i have created policy name "tagging-policy"
Now , To deploy this policy in azure we use below codes.

```python
az policy definition create --name "tagging-policy" --display-name "Allow tagged resource creation " --description "this policy allow the creation of only tagged resources" --rules tagging-policy.json --mode Indexed
az policy assignment create --name "tagging-policy creation " --policy "tagging-policy"
```
Once the policy is deployed we can check the policy using below code

```bash
AZ policy assignment list
```

In below image we can see the policy that i have deployed

![tagging policy details](https://user-images.githubusercontent.com/104189782/188860168-adcfa52d-517d-4e30-9755-db96dea09738.png)

### Creating Packer image 

For this project we have create a ubuntu server 18.04-LTS VM image for deployment 

We will follow below setps to create packer image 

1. Providing authorization 

Packer need authorization to create resource in azure . Instead of providing credential directly we will use service princple for authorization

We can collect client id , subscription id , tenant id and client secreat from azure then use below commnds to export this SP and save to root file.

```bash
export ARM_SUBSCRIPTION_ID="XXXXXXX"
export ARM_TENANT_ID="XXXXXXX"
export ARM_CLIENT_ID="XXXXXX"
export ARM_CLIENT_SECRET="XXXXXX"
```
Use below command to save to root file 

```bash
. ~/.bashrc
```
Check if it is Saved 

```bash
printenv | grep ^ARM*
```

2. 





