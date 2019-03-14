---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-03"

keywords: FAQ, faqs, limit, resource, vNIC, VSI, PGW, console, VRF, bandwidth, COS, egress, load balancer

subcollection: vpc

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:faq: data-hd-content-type='faq'}
{:DomainName: data-hd-keyref="DomainName"}


# FAQs
{: #faqs}

## What is the limit on the number of characters in a VPC name?
{:faq}

Currently, the limit is 100. If this limit is exceeded, you might receive an "internal error" message.

## Can any of my VPC resource names begin with a number?
{:faq}

No, although the name can contain numbers, it must begin with a letter.

## Are there restrictions on what characters I can use in a name?
{:faq}

Yes, the UI blocks consecutive double dashes, underscores, and periods from being part of a VSI name.


## During Floating IP assignment in a VPC, a customer must specify the vNIC of the VSI, is that correct?
{:faq}

Yes, and in fact, it must be the primary network interface of a server.

However, if we add an "address" resource in the API under the networking area, we could very well change the association of the floating IP to the address rather than the interface.

## Can a vNIC on a virtual server instance in my VPC have both floating IP and private IP?
{:faq}
 
Yes.

## In the IBM Cloud Console UI for VPC, there is only a ”toggle" for each subnet to attach or detach to or from the Public Gateway. Who creates the PGW? Will the PGW default to be ready when a customer wants to attach the subnet to the PGW in the UI?
{:faq}

The PGW needs to be created explicitly through the API as it stands now, because the API requires an explicit association of a subnet to a particular public gateway.

## Imagine that VSI1 in a VPC has only vNIC1 and it is attached to Subnet1. Subnet1 is attached to a Public Gateway (PGW). Can a customer still assign a Floating IP to VSI1?
{:faq}

Yes, a server can be on a subnet attached to a public gateway and also have a floating IP. The assignment of floating IP to a VSI is not related to whether there is a public gateway attached to the subnet. A floating IP associated to a VSI will take precedence over the public gateway attached to the subnet.

## In my VPC, VSI1 has 2 vNICs, called vNIC1 and vNIC2. Can these two vNICs be attached to the same subnet?
{:faq}
 
Yes, there is no limitation on having multiple network interfaces on the same server attached to the same subnet. However, multiple NICs on a VSI currently are not supported.

## Can a VSI be created without a subnet, just with Floating IP?
{:faq}

No.

## Can a VSI be attached to more than one VPC?
{:faq}

No.

## Can a subnet size be changed after it is created in a VPC?
{:faq}

No.

## During the PGW creation, do I need to reserve the FIP, or does the system automatically reserve the FIP? Will I see that Floating IP when I query all of the Floating IPs?

As the spec is currently defined, RIAS automatically creates a floating IP along with the public gateway if an existing floating IP is not specified. And yes, that floating IP will show up in the list.

## Who enforces that there must be only 1 Public Gateway per zone for a VPC?
{: faq}

The Regional Infrastructure API Service (RIAS) enforces this limit.

## How does VRF affect my other networking capabilities and my subnets?
{:faq}

Caveats for VLANs and VRF:

* Inter-account VLAN spanning is not allowed in the VRF environment.
* IPSec VPN service is limited.

**Note:** VRF does not prevent SSL or PPTP VPN access, but its behavior changes. Without VRF, one VPN connection is enough to see all servers on your account. With VRF, you can only access resources in the market associated with your VPN. So if you connect to the DAL VPN, you can only connect to DAL servers.

## What is the correct way to use the `instance-network-interface-floating-ip-add` subcommand in VPC? Does one create/allocate a floating IP address beforehand?
{:faq}

 You have to allocate a floating IP first, and then provide the FIP address on the interface floating IP `add` command.

 For example: `ibmcloud is floating-ip-reserve FLOATING_IP_NAME (--zone ZONE | --nic NIC_ID)`. Provide the zone.

 ## Why do I need to specify a subnet when I set up my VPN for VPC, and what should I specify?
 {:faq}

When you’re setting up a VPN gateway, you must specify a subnet, so that the VPN gateway can obtain the IP addresses it requires for the VPN service. By specifying the subnet, you retain control over how your VPN traffic is handled, and you have the flexibility to specify a location that’s closer to the resources that utilize the VPN. In this way, you can reduce latency and improve performance. 

## Are there egress bandwidth charges for traffic from VPC to COS?
{:faq}

There are no egress bandwidth charges as long as the ADN endpoint is used to connect from VPC to COS, but API call charges still apply.

## How do I know where my load balancer instances will be deployed?
{:faq}

The subnets chosen determine where the VPC load balancer is going to be deployed. VPC load balancer is a regional resource. The best practice is to choose subnets from different zones under a given region to increase redundancy
