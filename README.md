# Manage Azure Subscriptions and RBAC Lab

**Table of Contents**
1. [Introduction](#Overview)
2. [Create Management Group](#Create-the-management-group)
3. [Create the helpdesk Group](#Create-the-helpdesk-group)
4. [Assign RBAC Roles](#Assign-rbac-roles)
   - [VM Contributor Role](#VM-sontributor-role)
   - [Custom Support Role](#Custom-support-role)
5. [Monitor Role Assignment](#Monitor-role-assignment)
6. [Takeaway](#Takeaway)

# Overview

In this lab, we will use a **Management Group** to manage Access to **Virtual Machines** within multiple **Subscriptions** without having to edit each Subscription separately. 

## Create the Management Group

1. Navigate to > **Resource Manager** > **Organization** > **Management Groups** blade.
2. Click on ‘**Create’**, give the group a name, and click ‘**Submit’**.
3. Once the group has been created, click on the **3 dots (…)** next to your subscription(s) and select ‘**Move’**.
4. Move them to the new **Management Group**.
    
    ![image.png](/image.png)
    

## Create the helpdesk Group

1. Navigate to the **Entra ID portal** > **Manage** > **Groups.**
2. Click on ‘**New Group’** and give it a name. Everything else can be left as default.
    
    ![image.png](/image%201.png)
    
3. Click ‘**Create’**.

## Assigning RBAC roles

### VM Contributor Role

1. Navigate back to the **Resource Manager** > **Organization** > **Management Group** > Select **your** Management Group.
2. On the left tab, select ‘**Access Control (IAM)’** blade.
3. Click **Add** > ‘**Add role assignment’**.
4. Find the Virtual Machine Contributor role and select it. Click ‘**Next’**.
5. In the Members tab, under Assign access to, select ‘**User, group, or service principal’**.
6. Then, under '**Members**', click on '**Select members**' and choose the **helpdesk** role we created earlier.
7. Click ‘**Review + assign**’. Once reviewed, click it again to assign the role to the helpdesk group.
    
    ![image.png](/image%202.png)
    

> If you added multiple subscriptions to the Management Group, assigning this role at the Management Group scope allows the helpdesk group to manage Virtual Machines across all the Subscriptions.
> 

### Custom Support Role

1. Navigate back to the **Resource Manager** > **Management Groups** > **Your** Management Group.
2.  Click on the **Access control (IAM)** blade.
3. Click ‘**Add**’ > ‘**Add custom role**’ and give it a name.
4. Under the ‘**Baseline permissions**’, select ‘**Clone a role**’ and clone the ‘**Support Request Contributor**’ role.
5. In the ‘**Permissions**’ tab, click ‘**Exclude permissions**’ and select ‘**Microsoft Support**’. Then you will select ‘**Register Support Resource Provider**’ and click ‘**Add**’.
    1. Under the default ‘**Support Request Contributor**’ role, all permissions under ‘**Microsoft.Support**’ are granted. So, we use the ‘**Exclude permissions**’ tab to revoke a specific action from being performed.
        
        ![image.png](/image%203.png)
        
6. Click ‘**Review + create**’, review the role permissions, and click ‘**Create**’.

> Now we’ve created a custom role and assigned it to our Management Group. This grants the helpdesk group the ability to exercise their permissions across all the Subscriptions within the Management Group.
> 

## Monitor Role Assignment

1. Navigate to the ‘**Monitor**’ portal > ‘**Activity log**’ blade.
2. Click on ‘**Management Group**’ highlighted in blue and select **your** Management Group.
3. Here, you can monitor the creation/assignment of roles within the Management Group. 
    
    ![image.png](/image%204.png)
    

## Takeaway

- In this lab, we create a Management Group to manage access to multiple Subscriptions simultaneously.
- Created a helpdesk role that can manage Virtual Machines across all subscriptions within the Management Group via inheritance.
- Created and assigned a custom Azure Support role by using one of the existing Microsoft Roles as a template.
