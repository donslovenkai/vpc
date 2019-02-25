---

copyright:
  years: 2017, 2018, 2019

lastupdated: "2019-02-24"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:download: .download}

# Creating and managing block storage in VPC
{: #creating-and-managing-storage-in-vpc}

{{site.data.keyword.block_storage_is_full}} (VPC) provides hypervisor-mounted, high-performance data storage for your virtual server instances (VSIs).

You can create block storage volumes when you provision a virtual server instance in a VPC network.  The VPC infrastructure provides rapid scaling across multiple regions and zones, and extra performance and security.

You can also create new volumes independent of the VSI lifecycle, and later attach these volumes to a VSI. Data volumes persist when detached from the VSI; you can later attach a volume to a new instance. You can also specify that data volumes are automatically deleted when you delete the VSI.  Boot volumes are deleted when you delete the VSI. 

When you provision an {{site.data.keyword.vsi_is_full}} instance, a 100 GB, general purpose IOPS (3 IOPS/GB) block storage volume is automatically created as a primary boot volume and attached to the VSI. During provisioning, you can rename the boot volume and change the volume size.
{:shortdesc}

You can also create secondary data volumes, which are automatically attached to the VSI. For more information about block storage volumes for the VPC, see [About Block Storage for VPC](/docs/infrastructure/block-storage-is?topic=block-storage-is-block-storage-about). To get started creating volumes independent of VSI provisioning, see [Getting Started with {{site.data.keyword.block_storage_is_short}}](/docs/infrastructure/block-storage-is?topicid=block-storage-is-block-storage-getting-started).

By default, boot and data volumes are encrypted with IBM-managed encryption. You can also encrypt your volumes using your own encyption keys, during VSI provisioning or when creating a standalone volume.

## Best practices for creating and naming your VPC block storage volumes:

* Determine your storage requirements before provisioning a volume.  Allow for adequate capacity and IOPS performance.
* Decide whether a predefined IOPS profile best meets your capacity and performance needs, or whether specifying custom settings is better.
* Decide whether you want to create secondary data volumes during virtual server instance provisioning.  These volumes are automatically attached to the instance.
* Decide whether you want the volume attached to a VSI be automatically deleted when you delete the VSI.
* When encrypting volumes with your own encryption key, ensure that the key is valid, that you have authorization to use the key, and that it can be used in your current region.
* Ensure that you are naming ALL of your volumes at provision time, including the boot volume.
* Ensure that you are naming ALL of your volume attachments at attachment time.
* Each volume must have a distinct name within a region within an account.

You can re-use the name of a volume after that volume has been deleted. However, be aware that re-using a volume name could cause confusion for billing purposes.
{:note}
