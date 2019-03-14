---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-03"

keywords: resource, access, role, action, permission, assign, administrator, operator, editor, viewer, user, managing

subcollection: vpc

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:table: .aria-labeledby="caption"}

# Planning {{site.data.keyword.vsi_is_short}} Permissions
{: #planning-virtual-servers-for-vpc-permissions}

When you're planning to provision {{site.data.keyword.vsi_is_full}}, you must understand the virtual server access available based on your user role.
{:shortdesc}

When working with VSIs, users are assigned a role based on the {{site.data.keyword.vpc_short}} to which an instance is provisioned. If a user has editor or administrator access to the {{site.data.keyword.vpc_short}}, they inherit the ability to create, delete, modify virtual server instances within that {{site.data.keyword.vpc_short}}.

Review the following table to learn more about user roles and the specific level of access each role encompasses.

* As an administrator of an account, you can define roles and take any available actions on {{site.data.keyword.vsi_is_short}}.
* As an editor of an account, you can modify the state and create/delete subresources.
* As a viewer of an account, you can take actions that don't change the state of the resources.

Virtual server resources *inherit* all user permissions from their parent VPC. Permissions cannot be set at the instance level.
{:note}

<table>
<CAPTION>Table 1. User permissions</CAPTION>
<THEAD>
<TR>
<th>VPC Permission</th>
<th>Description</th>
<th>Actions</th>
</TR>
</THEAD>
<TBODY>
<tr>
<td>Admin</td>
<td>All actions including the ability to manage <br>
access control.</td>
<td>
Access control:
<ul>
<li>Add and remove users</li>
<li>Assign roles for each user</li>
</ul>
<p>
Virtual Servers:
<ul>
<li>Create virtual servers</li>
<li>Stop virtual servers</li>
<li>Delete virtual servers</li>
<li>Restart virtual servers</li>
<li>Duplicate virtual servers</li>
<!-- <li>Resize virtual servers</li> -->
<!-- <li>Add and delete vNICs</li> -->
<!-- <li>Attach and delete volumes</li> -->
<li>View and list virtual servers</li>
<li>Rename virtual servers</li>
<!-- <li>Create image snapshots</li> -->
<!-- <li>Delete image snapshots</li> -->
<!-- <li>Create virtual servers off of image snapshots</li> -->
<li>Create and edit SSH keys</li>
<li>Delete SSH keys</li>
<!-- <li>Add autoscaling policies</li> -->
<!-- <li>Delete autoscaling policies</li> -->
<!-- <li>Modify autoscaling policies</li> -->
<!-- <li>View monitoring and log data</li> -->
<!-- <li>Modify alarms and notifications from monitoring</li> -->
</ul>
</p>
</td>
</tr>
<tr>
<td>Editor</td>
<td>Actions that can modify the state, as well <br>
as, create and delete sub-resources.</td>
<td>
Virtual Servers:
<ul>
<li>Create virtual servers</li>
<li>Stop virtual servers</li>
<li>Delete virtual servers</li>
<li>Restart virtual servers</li>
<li>Duplicate virtual servers</li>
<!-- <li>Resize virtual servers</li> -->
<!-- <li>Add and delete vNICs</li> -->
<!-- <li>Attach and detach volumes</li> -->
<li>View and list virtual servers</li>
<li>Rename virtual servers</li>
<!-- <li>Create image snapshots</li> -->
<!-- <li>Delete image snapshots</li> -->
<!-- <li>Create virtual servers off of image snapshots</li> -->
<li>Create SSH keys</li>
<li>Delete SSH keys</li>
<!-- <li>Add autoscaling policies</li> -->
<!-- <li>Delete autoscaling policies</li> -->
<!-- <li>Modify autoscaling policies</li> -->
<li>View monitoring and log data</li>
<!-- <li>Modify alarms and notifications from monitoring</li> -->
</ul>     
</td>
</tr>
<tr>
<td>Viewer</td>
<td>Actions that do not change state</td>
<td>
Virtual Servers:
<ul>
<li>View and list virtual servers</li>
<!-- <li>View and list image snapshots</li> -->
<li>View monitoring and log data</li>
</ul>
</td>
</tr>
</TBODY>
</table>

## Next steps
For more information on how to change a user's permissions, see [Managing user permissions for VPC resources](/docs/infrastructure/vpc?topic=vpc-managing-user-permissions-for-vpc-resources).
