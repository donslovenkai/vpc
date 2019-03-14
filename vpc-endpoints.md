---

copyright:
  years: 2017, 2018, 2019

lastupdated: "2019-03-03"

keywords: endpoint, service, DNS, resolver, mirror, object, storage, bandwidth, charges

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

# Service endpoints available for IBM Cloud VPC
{: #service-endpoints-available-for-ibm-cloud-vpc}

When you're ready to run workloads, you can reach some IBM Cloud infrastructure services from a VSI inside your {{site.data.keyword.cloud}} VPC by using certain ADN endpoints. Several types of services are available through private endpoints, which are reachable by VPC customers. By using these internal endpoints, you can avoid the bandwidth charges that could be incurred if you reached the endpoints from the public Internet.

Services you can reach include:

* DNS resolvers
* Mirrors
* Cloud Object Storage
* NTP

## Example endpoint for IBM Cloud Object Storage

For example, to reach a private endpoint for an object storage service on the IBM Cloud private network, replace the "domain" portion of the URL with `objectstorage.adn.networklayer.com`.

## Endpoints for DNS and mirrors

DNS and mirrors use the same 161.26/16 space everywhere. These specific IP endpoints are available at each VPC-enabled site:

* `mirrors.adn.networklayer.com` (161.26.0.6)
* DNS servers (161.26.0.10 and 161.26.0.11)
