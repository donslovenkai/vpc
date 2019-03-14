---

copyright:
  years: 2017, 2018, 2019
lastupdated: "2019-03-04"

keywords: resources, CLI, commands, VPC, subnet, instance, floating, region, endpoint, zone, storage

subcollection: vpc

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:table: .aria-labeledby="caption"}
{:download: .download}

# Quick reference to CLI commands for resources
{: #quick-reference-to-cli-commands-for-resources}

This quick guide to CLI commands for resources is useful to get going with the {{site.data.keyword.cloud}} CLI for Virtual Private Cloud.

* **To log in**

  * `ibmcloud login [-sso]`

* **To get information about VPCs**

  * `ibmcloud is vpcs`
  
Use the resource's ID to view specific details on the resource.
{: tip}

* **To view VPC details** 

  * `ibmcloud is vpc [vpc_id]` 

* **To get information about subnets** 

  * `ibmcloud is subnets`

* **To get subnet details**

  * `ibmcloud is subnet [subnet_id]`

* **To get information about instances**

  * `ibmcloud is instances` 

* **To view details about instances** 

  * `ibmcloud is instance [instance_id]`

* **To get information about floating IPs** 

  * `ibmcloud is floating-ips`  

* **To view floating IP details**

  * `ibmcloud is floating-ip [floating-ips_id]`

* **To get information about your regions and endpoints**

  * `ibmcloud is regions`

* **To get information about zones** 

  * `ibmcloud is zones [region_name]`
  
* **To get information about all block storage volumes**

  * `ibmcloud is volumes`
  
* **To view details about a block storage volume**

  * `ibmcloud is volume [volume_id]`
