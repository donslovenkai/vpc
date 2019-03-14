---

copyright:
  years: 2017, 2018, 2019
lastupdated: "2019-03-03"

keywords: limitations, bugs, known, Beta, services, capabilities

subcollection: vpc

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}

# Known limitations
{: #known-limitations}

This document contains short descriptions of known bugs in the current release, descriptions of features and APIs that are not supported, and indications of which features are now offered as Beta services only. Known limitations may be changing as we add capabilities to {{site.data.keyword.cloud}} Virtual Private Cloud, so feel free to check back with this document from time to time. 

## Known bugs

* If you rename a subnet, it could take up to 1 hour to see the new name of your subnet in the server details page, due to cache timing. (#758)

## Summary of features not supported

* Direct Link access to Virtual Private Cloud is supported through [**Classic Access**](/docs/infrastructure/vpc/classic-access.html) only.
* A subset of Private Services Endpoints are available to Virtual Private Cloud, not all endpoints are available. 
* Saving and restoring of images is not supported.

## APIs not supported

For details about what's supported, see the [API Spec](https://{DomainName}/apidocs/rias).

The following APIs are not supported in this release.

| Component | Functions | Comments |
|------|------|--------|
| **Compute:** |   |   |
| Images | Create/Delete not supported | Ubuntu 16.04, CentOS 7.X, Windows 08, Debian|
| Network_Interfaces | Get (no create, delete, update) | |
| Volume_Interfaces | Not supported |   |
| Port_Speed | | Only 100 and 1000 |
| **Storage:** |   |   |
| Volumes | Not supported |   |
| Snapshots | Not supported |  |

## Features and Use Cases not yet supported

This section gives a detailed list of unsupported features and use cases. 

* A Virtual Private Cloud cannot be peered with other Virtual Private Clouds.
* Existing IBM Cloud VSIs or bare metal servers cannot be migrated into a Virtual Private Cloud.
* Custom routes cannot be added to a Virtual Private Cloud. All the subnets in a Virtual Private Cloud can communicate with each other by default.
* IBM Cloud VPC does not support multicast or broadcast domains.
* IBM Cloud VPC does not provide end-to-end encryption. 
* Here are the core IBM Cloud services that can be used from Virtual Private Cloud. Other services are not accessible. 
  * NTP
  * Logging
  * DNS resolvers
* A subnet cannot be on multiple zones.
* A subnet cannot be moved from one zone to another.
* Subnets cannot be resized after they are created.
* Bare metal servers cannot be provisioned in a Virtual Private Cloud.
* IBM Cloud Classic resources cannot be in the same subnet in a Virtual Private Cloud. Connectivity between classic resources and one Virtual Private Cloud in your account is possible using [**Classic Access**](/docs/infrastructure/vpc/classic-access.html).
* IPv6 is not supported.
* You cannot use your own public IP as a Floating IP. The Floating IP pool is provided by IBM.
* A Floating IP is bound to a zone. For example, a Floating IP reserved from a pool in Zone 1 cannot be assigned to a VSI in Zone 2 in the same VPC.
* Private IP addresses cannot be moved between VSIs.
* Network interfaces cannot be moved between VSIs.
* You cannot designate the specific IP address of the VSI. You can only specify the IP range for the subnet. Once you attach a VSI to a subnet, the system assigns a private IP from that subnet.
* IBM Cloud VPC comes with its own Network as a Service tools such as LBaaS, ACLs, and security groups. You cannot use your own network appliances (for example, a Vyatta Gateway or other load balancer) to control any resource in the Virtual Private Cloud. Similarily, you cannot use your own load balancer or security groups services in IBM Cloud Classic Infrastructure to control resources in the IBM Cloud VPC.
* The public gateway does not allow the traffic to be initiated from the Internet to a VSI in the IBM Cloud VPC. For that purpose, a Floating IP must be used.
* ACL is stateless, so return traffic must be allowed explicitly in ACL rules.

## Components or features available as Beta services

* **VPN for IBM Cloud VPC** is available only as a Beta service.
* **LBaaS for IBM Cloud VPC** is available only as a Beta service.
