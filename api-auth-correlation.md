---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-03"

keywords: resource, policies, authorization, resource type, resource groups, roles, API, CLI, editor, viewer, administrator, operator

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

# Resource authorizations required for API and CLI calls
{: #resource-authorizations-required-for-api-and-cli-calls}

The table below lists the authorizations required to interact with {{site.data.keyword.cloud}} Virtual Private Cloud Infrastructure objects. This information is particularly helpful to know when you're making API calls. Here's what you need to know to use this table:

The terms _attached_ or _unattached_ refer to whether the resource is associated with a VPC or VPCs (either directly or indirectly through the resource's subnets). An unattached floating IP or Network ACL has no subnets, and therefore it is not associated with any VPC, so authorization by VPC is not applicable.

* **View** and **List** actions correspond to the **Viewer** or **Operator** roles.
* **Update** and related actions correspond to **Editor** or **Administrator** roles.
* Resources are protected by authorization, resource reference objects are not (ID, CRN, and so forth).


| Resource | Operation | Required Authorization |
|--------|--------|---------|
| VPC | Create | View authorization on the Resource Group for that VPC, and Update authorization on VPC Resources|
| VPC | Update, Delete |  Update authorization on VPC |
| VPC |  View, List | View authorization on VPC  |
| VPC default ACL, default SG|  View, List | View authorization on VPC |
| VPC address prefixes |  Create, Update, Delete | Update authorization on VPC |
| VPC address prefixes |  View, List | View authorization on VPC  |
|—————|——————|———————|
| Floating IP (unassociated) | Create, Update, Delete | Any Account user and View authorization on all Account Management Services, if the resource is created in the default resource group. Click [here](https://{DomainName}/docs/infrastructure/vpc?topic=vpc-managing-user-permissions-for-vpc-resources#setting-up-viewer-access) for instruction on setting up viewer access. **Note: Associating and disassociating are part of the Floating IP Update operation**|
| Floating IP (unassociated) | View, List | Account user |
| Floating IP (associated) | Update | Update authorization for the associated subnet and its VPC (you cannot Create or Delete a floating IP after it is associated) |
| Floating IP (associated) | View, List | View authorization for the floating IP’s subnet | 
|——————|———————|————————|
| Network ACL (unattached), ACL rules | Create, Update, Delete | Any Account user |
| Network ACL (unattached), ACL rules | View, List | Any Account user |
| Network ACL (attached), ACL rules | Create, Update, Delete | Update authorization on all of the attached subnets and VPC |
| Network ACL (attached), ACL rules | View, List | View authorization on at least 1 of the attached subnets and VPC |
|——————|———————|————————|
| Public gateway | Create, Update, Delete |  Update authorization on the PGW’s VPC |
| Public gateway | View, List | View authorization on the PGW’s VPC |
|—————————|————————|———————————|
| Geography | View, List |  For regions and zones, any Account user |
|———————|————————|—————————|
| SSH key | Create, Update, Delete | Any Account user |
| SSH key | View, List |  Any Account user |
|————————|—————————|————————|
| Subnet | Create, Update, Delete | Update authorization for the subnet’s VPC |
| Subnet | View, List | View authorization for the subnet’s VPC |
| Subnet ACL or PGW | Attach, Detach | Update authorization for the subnet’s VPC |
| Subnet ACL or PGW | View, List | View authorization for the subnet’s VPC |
|——————|—————————|————————|
| Security group, SG Rules | Create, Update, Delete | Update authorization for the security group’s VPC |
| Security group, SG Rules | View, List  | View authorization for the security group’s VPC |
|Security group’s Network interface | Create, Update, Delete | Update authorization for the security group’s VPC (which also is the NIC’s VPC) |
|Security group’s Network interface | View, List  | View authorization for the security group’s VPC (which also is the NIC’s VPC) |
|—————————|—————————|—————————|
| Images | Create, Update, Delete | Any Account user |
| Images | View, List  | Any Account user |
| Instances | Create, Update, Delete | Update authorization for the Instance’s VPC |
| Instances | View, List  | View authorization for the Instance’s VPC |
| Instance actions, NICs, FIPs | Create, Update, Delete | Update authorization for the Instance’s VPC |
| Instance actions, Initialization, NICs, FIPs | View, List  | View authorization for the Instance’s VPC |
|————————|——————|————————|
| VPN gateway | Create, Update, Delete | Update authorization for the VPN |
| VPN gateway | View, List  | View authorization for the VPN |
| VPN gateway connections | Create, Update, Delete | Update authorization for the VPN |
| VPN gateway connections | View, List  | View authorization for the VPN |
| VPN gateway ike_policies, ipsec_policies and connections | Create, Update, Delete | Update authorization for the VPN |
| VPN gateway ike_policies, ipsec_policies and connections|View, List  | View authorization for the VPN |
|————————|——————|————————|
| Load Balancer | Create, Update, Delete | Update authorization for the Load Balancer |
| Load Balancer | View, List  | View authorization for the Load Balancer |
| Load Balancer  pools and listeners | Create, Update, Delete | Update authorization for the Load Balancer |
| Load Balancer pools and listeners | View, List  | View authorization for the Load Balancer |
|————————|——————|————————|
| Volumes | Create, Update, Delete | Update authorization for the Volume
| Volumes | View, List  | View authorization for the volume |
| Volume profiles | View, List  | Any Account user |

