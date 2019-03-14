---

copyright:
  years: 2017, 2018, 2019
lastupdated: "2019-03-03"

keywords: create, VPC, CLI, resources, plugin, SSH, key, hello, world, provision, instance, subnet

subcollection: vpc

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:table: .aria-labeledby="caption"}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}

# Creating a VPC using the IBM Cloud CLI
{: #creating-a-vpc-using-the-ibm-cloud-cli}

This guide shows you how to create {{site.data.keyword.cloud}} Virtual Private Cloud resources using the IBM Cloud CLI.

## Pre-requisites:

1. Install the [IBM Cloud CLI](https://cloud.ibm.com/docs/cli/index.html#overview).

2. Install or update the `infrastructure-service` plugin to the IBM Cloud CLI.

  To install:

  ```
  ibmcloud plugin install infrastructure-service
  ```
  {: pre}

  To update:

  ```
  ibmcloud plugin update
  ```
  {: pre}

  To view installed plugins and versions:

  ```
  ibmcloud plugin list
  ```
  {: pre}


3. Generate a public SSH key to provision Virtual Server Instances (VSIs).

You may have a public SSH key already. Look for a file called ``id_rsa.pub`` under an ``.ssh`` directory under your home directory, for example, ``/Users/<USERNAME>/.ssh/id_rsa.pub``. The file starts with ``ssh-rsa`` and ends with your email address.

If you do not have a public SSH key or if you forgot the password of an existing one, generate a new one by running the ``ssh-keygen`` command and following the prompts.


To learn how to create a Virtual Private Cloud in different IBM Cloud regions, see our [Regions](/docs/infrastructure/vpc/vpc-regions.html) topic.
{: tip}


## Step 1: Log in to IBM Cloud.

If you have a federated account:
```
ibmcloud login -sso
```
{: pre}

otherwise

```
ibmcloud login
```
{: pre}

## Step 2: Create a VPC and save the VPC ID.

Use the following command to create a VPC named _helloworld-vpc_.

```
ibmcloud is vpc-create helloworld-vpc
```
{: pre}

You should see output like this:

```
Creating VPC helloworld-vpc in resource group Default under account <Account Name> as user <User>...

ID        ba9e785a-3e10-418a-811c-56cfe5669676   
Name      helloworld-vpc   
Default   no   
Created   1 second ago   
Status    available   
```
{:screen}

Save the ID in a variable so we can use it later, for example:

```
vpc="ba9e785a-3e10-418a-811c-56cfe5669676"
```
{: pre}

## Step 3: Create a subnet and save the subnet ID.

Let's pick the `us-south-2` zone for the subnet's location and call the subnet _helloworld-subnet_.

```
ibmcloud is subnet-create helloworld-subnet $vpc us-south-2 --ipv4-address-count 8
```
{: pre}

You should see output like this:

```
Creating Subnet helloworld-subnet in resource group Default under account <Account Name> as user <User>...

ID               50ba0da9-279a-4791-b7cb-cd3d7b2bc14d   
Name             helloworld-subnet   
IPv*             ipv4   
IPv4 CIDR        10.240.64.0/29  
IPv6 CIDR        -   
Addr available   3   
Addr Total       8   
Gen              -   
ACL              allow-all-network-acl-ba9e785a-3e10-418a-811c-56cfe5669676(e9c2790b-cee2-465a-8539-d8cd90d33621)   
Gateway          -   
Created          now   
Status           pending   
Zone             us-south-2   
VPC              helloworld-vpc(ba9e785a-3e10-418a-811c-56cfe5669676)   
```
{:screen}

Save the ID in a variable so we can use it later, for example:

```
subnet="50ba0da9-279a-4791-b7cb-cd3d7b2bc14"
```
{: pre}

Note that the status of the subnet is `pending` when it first is created. Before you can proceed, the subnet needs to move to `available` status, which takes a few seconds. To check the status of the subnet, run this command:

```
ibmcloud is subnet $subnet
```
{: pre}

## Step 4: Attach a public gateway

Attach a public gateway to the subnet to allow all attached resources to communicate with the public internet. 

To create a public gateway, run the following command:

```
ibmcloud is public-gateway-create my-gateway $vpc us-south-2
```
{: pre}

Save the ID in a variable so you can use it later, for example:

```
gateway="f94a91c7-95db-42f2-9949-93a7e8fb63fb"
```
{: pre}

To attach the public gateway to your subnet, run the following command:
```
ibmcloud is subnet-update $subnet --public-gateway-id $gateway
```
{: pre}


Only one public gateway per zone is allowed in a VPC, but that public gateway can be attached to multiple subnets in the zone. To find the public gateway for a zone, run the 'ibmcloud is public-gateways` command and look for the particular VPC and Zone values.
{: tip}

## Step 5: Create an SSH Key in IBM Public Cloud.

You'll use the key to provision a virtual server instance. You can use the same key to provision multiple virtual server instances.

To see the available keys in your IBM Cloud account, run this command:

```
ibmcloud is keys
```
{: pre}

To create a key, run the following command. Substitute the path to your `id_rsa.pub` file.

```
ibmcloud is key-create helloworld-key @$HOME/.ssh/id_rsa.pub
```
{: pre}

You should see output like this:

```
Creating key helloworld-key in resource group Default under account <Account Name> as user <User>...

ID               859b4e97-7540-4337-9c64-384792b85653   
Name             helloworld-key   
Type             rsa   
Length           2048   
FingerPrint      SHA256:hkcAOGB5z7QXqZLHd0kGqhj735qrfMjZLH9PxS/42vA   
Key              ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC9i2joQ8eiFVdJ7pOlC6h5+IoBL6wFFygkk9Na3gV8Bi52dv44YOAjSJ2oduguHEtLp5r4eh4+5jiEBkFYkHNUhE0MxlcVZABTYWePXx4QnlmGr99xyOfi6DAHhSRQiSBhmhjcGjbADavDuIgoyKpVXbU9O1If3P0miNpaouaZmr+d68OHt4yPvNnztlluV3JBISJgqJ7pzg6wFF0SrjqtEYKBd8oxwogHu+rmRgT7IF09oSiKpKZRF0VfeLFz+REh9RuKa4Jh63aa2PRIgDKq6HO7MEdfOtGzCzoqqlFKgpl+VgGyT0b5BjQEnWv13cwx02bv5QCwma/GeAOpW0CD user@email.com   

Created          now   
```
{:screen}

Save the ID in a variable so we can use it later, for example:

```
key="859b4e97-7540-4337-9c64-384792b85653"
```

## Step 6: Select a profile and image for the virtual server instance.

To list all available instance profiles, run the following command:

```
ibmcloud is instance-profiles
```
{: pre}

To list all available images, run the following command:

```
ibmcloud is images
```
{: pre}

Let's pick instance profile `b-2x8` and image `ubuntu-16.04-amd64`. To get the image ID of `ubuntu-16.04-amd64`, run the following command:

```
image=$(ibmcloud is images | grep "ubuntu-16.04-amd64" | cut -d" " -f1)
```
{: pre}

## Step 7: Provision a Virtual Server Instance.

```
ibmcloud is instance-create helloworld-vsi $vpc us-south-2 b-2x8 $subnet 1000 --image-id $image --key-ids $key
```
{: pre}

You should see output like this:

```
Creating instance helloworld-vsi in resource group Default under account <Account Name> as user <User>...

ID                4562c5c0-9cf7-4406-bc90-ab4baea91057   
Name              helloworld-vsi   
Gen                  
Profile           b-2x8   
CPU Arch          amd64   
CPU Cores         2   
CPU Frequency     2000   
Memory            8   
Primary Intf      primary(2e850924-b5d7-4386-a778-03556d5850c1)   
Primary Address   10.240.64.4  
Image             ubuntu-16.04-amd64(7eb4e35b-4257-56f8-d7da-326d85452591)   
Status            pending   
Created           5 seconds ago   
VPC               helloworld-vpc(ba9e785a-3e10-418a-811c-56cfe5669676)   
Zone              us-south-2   
```
{:screen}

Save the ID of the primary network interface `Primary Intf` in a variable so we can use it later, for example:

```
nic="2e850924-b5d7-4386-a778-03556d5850c1"
```
{:pre}

Note that the status of the instance is `pending` when it first is created. Before you can proceed, the instance needs to move to `running` status, which takes a few minutes. To check the status of all instances, run this command:

```
ibmcloud is instances
```
{: pre}


## Step 8: Create a Floating IP address.

You need a Floating IP address so you can log in to the virtual server instance (VSI) from the internet.

```
ibmcloud is floating-ip-reserve helloworld-fip --nic-id $nic
```
{: pre}

You should see output like this:

```
Creating floating ip helloworld-fip in resource group Default under account <Account Name> as user <User>...

ID               b9d1cc1f-67db-40e3-81de-9228465170a5   
Address          169.61.181.53   
Name             helloworld-fip   
Target           primary(2e850924-.)   
Target Type      intf   
Target IP        10.0.1.5   
Created          now   
Status           available   
Zone             us-south-2   
```
{:screen}

Save the `Address` in a variable so we can use it later:

```
address=169.61.181.53
```
{: pre}

## Step 9: Add a rule to the default security group for SSH

Find the security group for the VPC:

```
ibmcloud is vpc-sg $vpc
```
{: pre}

You should see output like this:
```
Getting default security group of vpc ba9e785a-3e10-418a-811c-56cfe5669676 under account <Account Name> as user <User>...

ID               2d364f0a-a870-42c3-a554-000000981149
Name             errand-drastic-imperial-retail-unlocked-jester
Created          1 week ago
VPC              helloworld-vpc(ba9e785a-3e10-418a-811c-56cfe5669676)
Resource Group   -
Tags             -

Rules
ID                                     Direction   IPv*   Protocol                  Remote
b597cff2-38e8-4e6e-999d-000002031345   inbound     ipv4   all                       errand-drastic-imperial-retail-unlocked-jester(2d364f0a-.)
b597cff2-38e8-4e6e-999d-000002031527   outbound    ipv4   all                       -

```
{:screen}

Save the ID in a variable so we can use it later:

```
sg=2d364f0a-a870-42c3-a554-000000981149
```
{: pre}

Now create the rule to allow SSH:

```
ibmcloud is sg-rulec $sg inbound tcp --port-min=22 --port-max=22
```
{: pre}

You should see output like this:

```
Creating rule for security group 2d364f0a-a870-42c3-a554-000000981149 under account <Account Name> as user <User>...

ID          b597cff2-38e8-4e6e-999d-000001949921
Direction   inbound
IPv*        ipv4
Protocol    tcp
Min Port    22
Max Port    22
Remote      -
```
{:screen}

## Step 10: Log in to your virtual server instance using your private SSH key.

For example, you can use a command of this form:

```
ssh -i $HOME/.ssh/id_rsa root@$address
```
{:pre}

You'll receive a response similar to the example that follows. When you're prompted to continue connecting, type `yes`.

```
The authenticity of host '169.61.181.53 (169.61.181.53)' can't be established.
ECDSA key fingerprint is SHA256:9MczXIwJq892DYwu0sZpQZOXORdvNXeP1aFioZpQDsM.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '169.61.181.53' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 16.04.5 LTS (GNU/Linux 4.4.0-133-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.


The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

root@helloworld-vsi:~#
```
{:screen}

## Step 11: Hello, World!

Run the following command in the terminal window:

```
echo `hostname` says "Hello, World!"
```
{:pre}

You should see the following output:

```
helloworld-vsi says Hello, World!
```
{:screen}

## Congratulations!

You've successfully provisioned and connected to your Virtual Private Cloud instance using the IBM Cloud CLI. To try out more CLI commands, explore the full reference:

* [CLI Reference for VPC](/docs/cli/reference/ibmcloud?topic=infrastructure-service-cli-vpc-reference#vpc-reference)
