---

copyright:
  years: 2019
lastupdated: "2019-03-03"

keywords: region, zone, deploy, datacenter, data, center, federated, CLI, API, account

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

# Creating a VPC in a different region
{: #creating-a-vpc-in-a-different-region}

A region is a specific geographical location where you can deploy apps, services, and other {{site.data.keyword.cloud}}} resources. Regions consist of one or more zones, which are physical data centers that host the compute, network, and storage resources and related cooling and power that host services and applications. Zones are isolated from each other, which ensures no shared single point of failure.

Virtual Private Cloud is being rolled out to all of IBM Cloud regions in phases.

|   Location     | Region | API Endpoint | Status |
| ------- | :------: | :------: |:------: |
| Dallas | us-south | `us-south.iaas.cloud.ibm.com`| Available |
| Frankfurt | eu-de | `eu-de.iaas.cloud.ibm.com`| Available |
| Washington DC | us-east | `us-east.iaas.cloud.ibm.com`| Coming Soon |
| Tokyo | jp-tok | `jp-tok.iaas.cloud.ibm.com`| Coming Soon |
| London | eu-gb | `eu-gb.iaas.cloud.ibm.com`| Coming Soon |
| Sydney | au-syd | `au-syd.iaas.cloud.ibm.com`| Coming Soon |

The Regional API (VPC) endpoint is automatically set by the IBM Cloud CLI when you log in to a specific region.
{: note}

## Log in to a specific region using the CLI

When you login to IBM Cloud, you can specify a region or choose it later. For example, to log in to the global API endpoint in the Dallas (`us-south`) region directly, run the following commands, depending whether you have a federated account (SSO) or not.

For a federated account,

```
ibmcloud login -a https://cloud.ibm.com -r us-south --sso
```
{: pre}

For a non-federated account,

```
ibmcloud login -a https://cloud.ibm.com -r us-south
```
{: pre}

To choose the region later, do not specify the `-r <region>` parameter and the CLI will prompt you to choose a region.

Example output:

```
API endpoint: cloud.ibm.com

Get One Time Code from https://identity-2.eu-central.iam.cloud.ibm.com/identity/passcode to proceed.
Open the URL in the default browser? [Y/n]> y
One Time Code >
Authenticating...
OK

Select an account:
1. MyAccount (00a11aa1a11aa11a1111a1111aaa11aa) <-> 1234567
2. TeamAccount (2bb222bb2b22222bbb2b2222bb2bb222) <-> 7654321
Enter a number> 2
Targeted account TeamAccount (2bb222bb2b22222bbb2b2222bb2bb222) <-> 7654321


Targeted resource group Default

Select a region (or press enter to skip):
1. au-syd
2. jp-tok
3. eu-de
4. eu-gb
5. us-south
6. us-east
Enter a number> 5
Targeted region us-south


API endpoint:      https://cloud.ibm.com   
Region:            us-south   
User:              first.last@email.com   
Account:           TeamAccount (2bb222bb2b22222bbb2b2222bb2bb222) <-> 7654321  
Resource group:    Default   
CF API endpoint:      
Org:                  
Space:                

...
```
{: screen}

## Switch regions using the CLI

To get the latest status of the available VPC regions, run the following command:

```
ibmcloud is regions
```
{: pre}

To switch to a different region, run the `ibmcloud target -r <region>` command. For example, to switch to the Frankfurt region, run the following command:

```
ibmcloud target -r eu-de
```
{: pre}

To check which location you are currently in, run the following command:

```
ibmcloud target
```
{: pre}

## Switch regions using the API  

To interact with the Regional API via REST, direct the request to the API endpoint of the region where you want to create resources. The region's API endpoint is shown above in the table. Additionally, you can find the available endpoint for the different regions by running the following command:

```
ibmcloud is regions
```
{: pre}


For example, to get the list of VPCs in the `us-south` region, run the following command:

```
curl https://us-south.iaas.cloud.ibm.com/v1/vpcs?version=2019-01-01 -H "Authorization: $iam_token"
```
{: pre}


## Zones

To get the list of zones available for each region, run the `ibmcloud is zones <region>` command. For example, to get the list of zones in region `us-south`, run the following command:

```
ibmcloud is zones us-south
```
{: pre}
