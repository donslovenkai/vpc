---

copyright:
  years: 2017, 2018, 2019
lastupdated: "2019-03-03"

keywords: create, VPC, API, IAM, token, permissions, endpoint, region, zone, profile, status, subnet, gateway, floating IP, delete, resource, provision

subcollection: vpc

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}

# Creating a VPC using the REST APIs
{: #creating-a-vpc-using-the-rest-apis}

This guide shows you how to create {{site.data.keyword.cloud}} Virtual Private Cloud resources using the IBM Cloud Regional APIs (RIAS).

## Pre-requisites:

1. Install the [IBM Cloud CLI](https://cloud.ibm.com/docs/cli/index.html#overview).

## Step 1: Log in to IBM Cloud to get an IAM token to use in the API calls.

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

This command returns a URL and prompts for a passcode. Go to that URL in your browser and log in. If successful, you will get a one-time passcode. Copy this passcode and paste it as a response on the prompt. After the authentication steps, you'll be prompted to choose an account. Respond to any remaining prompts to finish logging in.

## Step 2: Get an IBM Identity and Access Management (IAM) Token

The following command calls the IBM Cloud CLI, parses out the IAM token and the `Bearer` token identifier, and stores it in a variable you can use in later commands.

```
iam_token=$(ibmcloud iam oauth-tokens | awk '/IAM/{ print $3 " " $4; }')
```
{: pre}

 To view your IAM token, run the command ``echo $iam_token``.

The result should look like this:

```
Bearer <your token>
```
{: screen}

The Authorization header expects the token to begin with "Bearer". If the result above does not include "Bearer", update the `iam_token` variable to include it. These examples assume that "Bearer" is included in the `iam_token`.

You must repeat the preceding step to refresh your IAM token every hour, because the token expires.
{: important}

## Step 3: Store the API Endpoint as a Variable

Store the API endpoint in a variable so it can be reused later. The API endpoints are per region
and follow the convention `https://<region>.iaas.cloud.ibm.com`. For example, the `us-south` API endpoint is `https://us-south.iaas.cloud.ibm.com`.

```
rias_endpoint=https://us-south.iaas.cloud.ibm.com
 ```
{: pre}

To verify that this variable was saved, run `echo $rias_endpoint` and make sure the response is not empty.

## Step 4: Run the GET Regions API

If you run into unexpected results, add the `--verbose` (debug) flag after the `curl` command to obtain detailed logging information. You also can check out the commonly encountered errors in our [troubleshooting page](/docs/infrastructure/vpc?topic=vpc-troubleshooting-your-ibm-cloud-vpc).
{: tip}

The following command returns the regions available for VPC, in JSON format. At least one object should return.

Note the required `version` query parameter for each API command.
{: note}

```
curl $rias_endpoint/v1/regions?version=2019-01-01 -H "Authorization: $iam_token"
```
{: pre}


## Step 5: Run the GET Zones API

The following command returns the all zones available for VPC in region `us-south`, in JSON format. At least three objects should return.

```
curl $rias_endpoint/v1/regions/us-south/zones?version=2019-01-01 -H "Authorization: $iam_token"
```
{: pre}


## Step 6: Run the GET Profiles API

The following command returns the profiles available for your instances, in JSON format. At least one object should return.

Add ` | json_pp ` after curl command to get readable JSON string
{: tip}


```
curl $rias_endpoint/v1/instance/profiles?version=2019-01-01 -H "Authorization: $iam_token"
```
{: pre}

If the API output is limited by pagination, set the limit higher than the `total_count`, for example:

```
curl "$rias_endpoint/v1/instance/profiles?version=2019-01-01&limit=50" -H "Authorization: $iam_token"
```
{: pre}

## Step 7: Run the GET Images API

The following command returns the images available for your instances, in JSON format. At least one object should return.

```
curl $rias_endpoint/v1/images?version=2019-01-01 -H "Authorization: $iam_token"
```
{: pre}

## Step 8: Run the GET VPCs API

The following command returns the VPCs that have been created under your account (if any), in JSON format.

```
curl $rias_endpoint/v1/vpcs?version=2019-01-01 -H "Authorization: $iam_token"
```
{: pre}

## Step 9: Create a Virtual Private Cloud

Create an IBM Cloud VPC called `my-vpc`.

```bash
curl -X POST $rias_endpoint/v1/vpcs?version=2019-01-01 \
  -H "Authorization: $iam_token" \
  -d '{
      	"name": "my-vpc"
      }'
```
{: pre}

For the rest of the calls, you'll need to know the ID of the newly created IBM Cloud VPC. Paste its ID into the variable, as shown:

Something like this: `vpc="35fb0489-7105-41b9-99de-033fae723006"`

```bash
vpc="<YOUR_VPC_ID>"
```
{: pre}

## Step 10: Create a Subnet

Create a subnet in your IBM Cloud VPC. For example, let's put it in the `us-south-2` zone.

```bash
curl -X POST $rias_endpoint/v1/subnets?version=2019-01-01 \
  -H "Authorization:$iam_token" \
  -d '{
        "name": "my-subnet",
        "ipv4_cidr_block": "10.0.1.0/24",
        "zone": { "name": "us-south-2" },
        "vpc": { "id": "'$vpc'" }
      }'
```
{: pre}

As with the Virtual Private Cloud, save the ID of the subnet in a variable.

```bash
subnet="<YOUR_SUBNET_ID>"
```
{: pre}

## Step 11: Check the Status of your Subnet

To provision resources in your subnet, the subnet must be in `available` status. Query the subnet resource and make sure the status is `available` before you continue. If the status is `failed`, contact [support](/docs/infrastructure/vpc?topic=vpc-getting-help-and-support) with the details. You can attempt to continue by trying to provision another subnet.

```bash
curl $rias_endpoint/v1/subnets/$subnet?version=2019-01-01 -H "Authorization: $iam_token"
```
{: pre}


## Step 12: Create a Public Gateway

To allow virtual server instances in the subnet to have access to the public internet, add a public gateway (PGW) to the subnet.  

```bash
curl -X POST $rias_endpoint/v1/public_gateways?version=2019-01-01 \
  -H "Authorization:$iam_token" \
  -d '{
        "name": "my-gateway",
        "zone": { "name": "us-south-2" },
        "vpc": { "id": "'$vpc'" }
      }'
```
{: pre}

As you did with the Virtual Private Cloud and the subnet, save the ID of the public gateway in a variable.

```bash
gateway="<YOUR_GATEWAY_ID>"
```
{: pre}

## Step 13: Attach the public gateway to the subnet.

```bash
curl -X PUT $rias_endpoint/v1/subnets/$subnet/public_gateway?version=2019-01-01 \
  -H "Authorization:$iam_token" \
  -d '{
        "id": "'$gateway'"
      }'
```
{: pre}


## Step 14: Create an SSH Key

Create a key with your public SSH key. This key is used when creating the virtual server instance, and it is needed to log into the virtual server instance.

Keys only can be added initially as part of creating the VPC in the UI or CLI. No tooling exists to add keys later.
{:tip}

```bash
curl -X POST $rias_endpoint/v1/keys?version=2019-01-01 \
  -H "Authorization:$iam_token" \
  -d '{
        "name": "my-key",
        "public_key": "ssh-rsa AAA....n",
        "type": "rsa"
      }'
```
{: pre}

Save the ID of the key in a variable.

```bash
key="<YOUR_KEY_ID>"
```
{: pre}

## Step 15: Choose a Profile and Image for your Virtual Server Instance

Run the APIs to list all profiles and images available for your virtual server instance, and choose a combination.

```
curl $rias_endpoint/v1/instance/profiles?version=2019-01-01 -H "Authorization:$iam_token"
```
{: pre}

To get additional details about the profiles, you can query the global catalog using the IBM Cloud CLI command `ibmcloud catalog entry <profile-name> --json`. For example,

```
ibmcloud catalog entry b-2x8 --json
```
{: pre}

The following command lists the images available.

```
curl $rias_endpoint/v1/images?version=2019-01-01 -H "Authorization:$iam_token"
```
{: pre}

Save the Name of the profile and the ID of the image in variables, which will be used later to provision a virtual server instance.

```bash
profile_name="<CHOSEN_PROFILE_NAME>"
image_id="<CHOSEN_IMAGE_ID>"
```
{: pre}

## Step 16: Provision a Virtual Server Instance

Provision a virtual server instance in the newly created subnet. Pass in your public SSH key so that you can log in after the instance is provisioned.

```bash
curl -X POST $rias_endpoint/v1/instances?version=2019-01-01 \
  -H "Authorization:$iam_token" \
  -d '{
        "name": "server-1",
        "type": "virtual",
        "zone": {
          "name": "us-south-2"
        },
        "vpc": {
          "id": "'$vpc'"
        },
        "primary_network_interface": {
          "port_speed": 1000,
          "subnet": {
            "id": "'$subnet'"
          }
        },
        "keys":[{"id": "'$key'"}],
        "flavor": {
          "name": "'$profile_name'"
         },
        "image": {
          "id": "'$image_id'"
         },
        "userdata": ""
      }'
```
{: pre}

As you did with the other resources, save the ID of the virtual server instance in a variable.

```bash
server="<YOUR_INSTANCE_ID>"
```
{: pre}

## Step 17: Check the Status of your Virtual Server Instance

Provisioning a Virtual Server Instance may take several seconds to a few minutes. Before continuing, query the status of the server and make sure it is `running`.

```bash
curl $rias_endpoint/v1/instances/$server?version=2019-01-01 -H "Authorization: $iam_token"
```
{: pre}

Also save the ID of the primary network interface of the virtual server instance returned in the above API call.  

```bash
network_interface="<YOUR_NETWORK_INTERFACE_ID>"
```
{: pre}

You can't get the primary network interface until you query the specific instance.
{: note}

## Step 18: Create a Floating IP

Create a floating IP for the virtual server instance, by using the instance's primary network interface as the target for the new floating IP address.

```bash
curl -X POST $rias_endpoint/v1/floating_ips?version=2019-01-01 \
  -H "Authorization:$iam_token" \
  -d '{
        "name": "my-server-floatingip",
        "target": {
            "id":"'$network_interface'"
        }
      }
'
```
{: pre}


Save the ID of the floating IP.

```bash
floating_ip="<YOUR_FLOATING_IP_ID>"
```
{: pre}

## Step 19: SSH into your Virtual Server Instance

To SSH to the server, use the `address` of the Floating IP you created. To get the `address` of the Floating IP, run the following command:

```bash
curl -X GET $rias_endpoint/v1/floating_ips/$floating_ip?version=2019-01-01 \
  -H "Authorization:$iam_token"
```
{: pre}

Use the `address` of the Floating IP to connect to the virtual server instance with SSH:

```bash
ssh -i <private_key_file> root@<floating ip address>
```
{: pre}

SSH access into the virtual server may be prevented by security groups. If SSH access is required, you must use an [appropriate security group](/docs/infrastructure/vpc-network?topic=vpc-network-using-security-groups).
{: note}

See [Connecting to your instance using Linux](/docs/vsi-is/vsi_is_connecting_linux_gc.html) for more information on how to connect to your instance.


## Step 20 (Optional): Delete the Resources

Delete the resources if desired. A resource cannot be deleted if it contains other resources. For example, a Virtual Private Cloud cannot be deleted if it contains subnets, and a subnet cannot be deleted if it contains virtual server instances. On a delete, the API may return quickly but the resource deletion might still be in progress. It is recommended to query the resource to make sure it is deleted prior to deleting other resources.

### Delete the floating IP.

```bash
curl -X DELETE $rias_endpoint/v1/floating_ips/$floating_ip?version=2019-01-01 \
  -H "Authorization:$iam_token"
```
{: pre}

### Delete the virtual server instance.

```bash
curl -X DELETE $rias_endpoint/v1/instances/$server?version=2019-01-01 \
  -H "Authorization:$iam_token"
```
{: pre}

### Delete the key.

```bash
curl -X DELETE $rias_endpoint/v1/keys/$key?version=2019-01-01 \
  -H "Authorization: $iam_token"
```
{: pre}


### Delete the public gateway.

```bash
curl -X DELETE $rias_endpoint/v1/public_gateways/$gateway?version=2019-01-01 \
  -H "Authorization:$iam_token"
```
{: pre}

### Delete the subnet.

```bash
curl -X DELETE $rias_endpoint/v1/subnets/$subnet?version=2019-01-01 \
  -H "Authorization:$iam_token"
```
{: pre}

### Delete the VPC.

```bash
curl -X DELETE $rias_endpoint/v1/vpcs/$vpc?version=2019-01-01 \
  -H "Authorization:$iam_token"
```
{: pre}

A vNIC cannot be deleted from a VSI, so there is no need to make a step for deletion of vNICs.
{: note}

## Congratulations!

You've successfully provisioned a Virtual Private Cloud instance using the REST APIs. To try out more API commands, explore the full reference:

* [API Reference for VPC](https://{DomainName}/apidocs/rias)
