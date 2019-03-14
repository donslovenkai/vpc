---

copyright:
  years: 2017, 2018, 2019
lastupdated: "2019-03-03"

keywords: quota, resource, classic, access, gateway, address, prefix, VSI, vNIC, floating, SSH, key, security, group, rule, remote, peer, ACL, region, ingress, egress, VPN, policies, load balancer, listener, pool, per

subcollection: vpc

---
# Quotas
{: #quotas}

This document covers quotas and limits for your {{site.data.keyword.cloud}} Virtual Private Cloud and the resources available within it.

## VPC quotas

Accounts have the following quotas:

|   Resource     | Maximum Number |
| ------- | :------: |
| Virtual Private Clouds | 5 per account|
| VPCs with Classic Access | 1 per region, per account |
| Public Gateways (PGWs) | 1 per zone |
| Address prefixes | 5 per VPC per zone |

## Subnet quotas

|   Resource     | Maximum Number |
| ------- | :------: |
| Subnets | 15 per Virtual Private Cloud |


## VSI quotas
|   Resource     | Maximum Number |
| ------- | :------: |
| Virtual Server Instances (VSIs) | 100 per account by default |
| vNICs per VSI | 5 per VSI |
| Floating IP addresses | 1 per VSI |
| SSH Keys | 100 per account |


## Security groups quotas

Some account-based quotas (limits) exist for security groups and their associated rules.

|Resource|Quota|
|--------|-----|
|Security groups|5 per network interface|
|Security groups|500 per account|
|Rules|50 per security group|
|Remote rules |5 per security group|
|Network interfaces|100 per security group|

## ACL quotas

|Resource|Quota|
|--------|-----|
|ACLs| 30 per account|
|ACLs |200 per region |
|Ingress rules|20 per ACL |
|Egress rules |20 per ACL |

## VPN quotas

Here are the current VPN resource limitations per account:

|Resource|Quota|
|--------|-----|
| VPN gateways| 7 per account |
| VPN gateways | 3 per zone |
| VPN connections | 10 per VPN gateway |
| IKE policies | 20 per account |
| IPSec policies | 20 per account |
| Peer subnets on any single VPN gateway | 50 across all VPN connections|
| Peer subnets  | 15 on any single VPN connection|
| Local subnets on any single VPN gateway | 50 across all VPN connections|
| Local subnets |  15 on any single VPN connection |


## Load Balancer quotas

Here are the current load balancer resource quotas:

|Resource|Quota|
|--------|-----|
| Load Balancer | 50 per account |
| Listener | 10 per Load Balancer |
| Pool | 10 per Load Balancer |
| Member | 50 per Pool |
