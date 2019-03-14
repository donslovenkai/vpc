---

copyright:
  years: 2017, 2018, 2019
lastupdated: "2019-03-03"

keywords: permissions, infrastructure, VPC, SSH, CLI, API, console

subcollection: vpc

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}

# Getting started with IBM Cloud Virtual Private Cloud Infrastructure
{: #getting-started-with-ibm-cloud-virtual-private-cloud-infrastructure}

IBM will be accepting a limited number of customers to participate in an Early Access program to VPC starting in early April, 2019 with expanded usage being opened in the following months. If your organization would like to gain access to IBM Virtual Private Cloud, please complete this [nomination form](https://cloud.ibm.com/vpc){: new_window} and an IBM representative will be in contact with you regarding next steps.
{: important}

To get started with {{site.data.keyword.cloud}} Virtual Private Cloud Infrastructure:

1. Create a Virtual Private Cloud.
2. Create one or more subnets in the Virtual Private Cloud in one or more zones.
3. Create a public gateway (PGW) on a subnet if you want resources on your subnet to have access to the internet or vice-versa.
4. Select the profiles of virtual server instances (VSIs) you'd like to run, and instantiate them.
5. Reserve a floating IP address, and associate it with a virtual server instance if you want to reach it from the internet.
5. Deploy your service or applications across the virtual server instances.

## Prerequisites

 * **User Permissions**: Be sure that your user has sufficient permissions to create and manage resources in your VPC. For a list of required permissions, see [Granting permissions needed for VPC users](/docs/infrastructure/vpc?topic=vpc-managing-user-permissions-for-vpc-resources).

 * **Have your SSH key ready**: You will use an SSH key to connect to your virtual server instance(s).

   * Look for a file called `id_rsa.pub` under an `.ssh` directory under your home directory, for example, `/Users/<USERNAME>/.ssh/id_rsa.pub`. The file starts with `ssh-rsa` and ends with your email address.

   * Or Generate an SSH Key: If you do not have a public SSH key or if you forgot the password of an existing one, generate a new one by running the `ssh-keygen` command and following the prompts. For example, you can generate an SSH key on your Linux server by running the command `ssh-keygen -t rsa -C "user_ID"`. That command generates two files. The generated public key is in the `<your key>.pub` file.
   
## Use the UI, CLI, or REST API

You can provision and manage all of your VPC resources through the UI, CLI, or REST API.

If you're new to IBM Cloud Virtual Private Cloud, choose any of the links below, which lead you through the process of creating your IBM Cloud VPC and its resources, from start to finish. You can choose whether to get started from the Console UI, the command line (CLI), or the regional infrastructure services (RIAS) API.

* For access through the user interface, log into the [IBM Cloud Console ![External link icon](../../icons/launch-glyph.svg "External link icon")]( https://{DomainName}/vpc){: new_window}. Follow the [UI guide](/docs/infrastructure/vpc?topic=vpc-creating-a-vpc-using-the-ibm-cloud-console) if you need help.
* To use the command line interface, use the [infrastructure-service](/docs/infrastructure-service-cli-plugin/vpc-cli-reference.html) plugin of the [IBM Cloud CLI](https://console.bluemix.net/docs/cli/index.html#overview) and follow the [Hello World](/docs/infrastructure/vpc?topic=vpc-creating-a-vpc-using-the-ibm-cloud-cli) example.
* For more advanced users, you can call the [REST APIs](https://{DomainName}/apidocs/rias) directly. Follow the [example code](/docs/infrastructure/vpc?topic=vpc-creating-a-vpc-using-the-rest-apis) tutorial to get started with the REST APIs.

## Next steps
If you're ready to dig in, go directly to the detailed documentation about **VPC Networking**,  **VSIs for VPC**, and **Block Storage for VPC**:

* [**IBM Virtual Private Cloud Networking**](/docs/infrastructure/vpc-network?topic=vpc-network-getting-started-with-networking-for-virtual-private-cloud)
* [**IBM Virtual Servers for Virtual Private Cloud**](/docs/vsi-is?topic=virtual-servers-is-gettingstartedvsigen)
* [**IBM Block Storage for Virtual Private Cloud**](/docs/infrastructure/block-storage-is?topic=block-storage-is-block-storage-getting-started)

