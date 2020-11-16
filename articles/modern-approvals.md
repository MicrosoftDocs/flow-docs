---
title: Easily Automate approval workflows. | Microsoft Docs
description: Automate approval workflows that integrate with SharePoint, Dynamics CRM, Salesforce, OneDrive for Business, Zendesk, or WordPress.
services: ''
suite: flow
documentationcenter: na
author: msftman
manager: anneta
editor: ''
tags: ''
ms.service: flow
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/27/2020
ms.author: deonhe
search.app: 
  - Flow
search.audienceType: 
  - flowmaker
  - enduser
---
# Create and test an approval workflow with Power Automate

With Power Automate, you can manage the approval of documents or processes across several services, including SharePoint, Dynamics 365, Salesforce, OneDrive for Business, Zendesk, or WordPress.

To create an approval workflow, add the **Approvals - Start an approval** action to any flow. After you add this action, your flow can manage the approval of documents or processes. For example, you can create document approval flows that approve invoices, work orders, or sales quotations. You can also create process approval flows that approve vacation requests, overtime work, or travel plans.

Approvers can respond to requests from their email inbox, [the approvals center](https://flow.microsoft.com/manage/approvals/received/) on the Power Automate website, or the Power Automate app.

## Create an approval flow
Here's an overview of the flow we'll create and test:

   ![A screenshot that shows an overview of the flow that's created in this article](./media/modern-approvals/create-flow-overview.png)

The flow performs the following steps:

1. Starts when someone creates a vacation request in a SharePoint Online list.
1. Adds the vacation request to the approval center, and then emails it to the approver.
1. Sends an email with the approver's decision to the person who requested vacation.
1. Updates the SharePoint Online list with the approver's decision comments.

[!INCLUDE [sharepoint-detailed-docs](includes/sharepoint-detailed-docs.md)]

## Prerequisites

To complete this walk-through, you must have access to:

[!INCLUDE [prerequisites-for-modern-approvals](includes/prerequisites-for-modern-approvals.md)]

Create these columns in your SharePoint Online list:

| Column | Type |
| ------ | ------ |
| Title | Single line of text |
|Start date | Date and Time |
| End Date | Date and Time |
| Comments | Single line of text |
| Approved | Yes/No |
| Manager Comments | Single line of text |

Make note of the name and URL of the SharePoint Online list. You'll need these items later when you configure the **SharePoint - When an item is created** trigger.

## Create your flow from the blank template
[!INCLUDE [sign-in-and-create-flow-from-blank-template](includes/sign-in-and-create-flow-from-blank-template.md)]

## Add a trigger

[!INCLUDE [add-trigger-when-sharepoint-item-created](includes/add-trigger-when-sharepoint-item-created.md)]

The **Site Address** and the **List Name** are the items you noted earlier in this walkthrough.

![SharePoint info](./media/modern-approvals/select-sharepoint-site-info.png)

## Add a profile action

1. Select **New step**, and then type **profile** into the **Choose an action** search box.

1. Find, and then select the **Office 365 Users - Get my profile** action.

    ![search for profile](./media/modern-approvals/search-for-profile.png)

1. Select the fields from your profile that you want to include in your flow, and then click **Create** to save the work you've done so far.

## Add an approval action

[!INCLUDE [add-an-approval-action](includes/add-an-approval-action.md)]

> [!NOTE]
> This action sends the approval request to the email address in the **Assigned To** box.
>
> If your scenario requires it, you can attach files to your approval requests that use Microsoft Dataverse.

## Add a condition

[!INCLUDE [add-approval-condition-response](includes/add-approval-condition-response.md)]

## Add an email action for approvals

Follow these steps to send an email if the vacation request is approved:

[!INCLUDE [add-action-to-send-email-when-vacation-approved](includes/add-action-to-send-email-when-vacation-approved.md)]

   ![configure approved email template](./media/sequential-modern-approvals/yes-email-config.png)

## Add an update action for approved requests

[!INCLUDE [add-action-to-update-sharepoint-with-approval](includes/add-action-to-update-sharepoint-with-approval.md)]

> [!NOTE]
> **Site Address**, **List Name**, **Id**, and **Title** are required.

![update item configuration](./media/modern-approvals/configure-update-item.png)

## Add an email action for rejections

[!INCLUDE [add-action-to-send-email-when-vacation-rejected](includes/add-action-to-send-email-when-vacation-rejected.md)]

![configuration for rejected requests](./media/modern-approvals/configure-rejected-email.png)

## Add update action for rejected requests

[!INCLUDE [add-action-to-update-sharepoint-with-rejection](includes/add-action-to-update-sharepoint-with-rejection.md)]

   > [!NOTE]
   > **Site Address**, **List Name**, **Id**, and **Title** are required.

   ![update item card](./media/modern-approvals/configure-update-item-no.png)

4. Select **Save** to save the work we've done.

If you've followed along, your flow should resemble this screenshot:

![A screenshot that displays the completed flow](./media/modern-approvals/completed-flow.png)

Now that we've created the flow, it's time to test it!

## Request an approval

[!INCLUDE [request-vacation-approval](includes/request-vacation-approval.md)]


## Create long-running approvals

If it's likely that your flow will run for more than 30 days, consider storing your approvals in Dataverse. This makes it possible for you to create flows that act on responses to approval requests, even after the original flow run times out. To do this, use two flows, one to send an approval request, and the other to run business logic on the responses to the approval request, based on the **Create an approval (v2)** action. Learn more about [long running approvals](https://docs.microsoft.com/business-applications-release-notes/april19/microsoft-flow/increased-run-duration).

>[!TIP]
> If you use modern email clients, you don't have to wonder if a request is still required because Power Automate automatically updates the email to indicate that the approval is completed.

## Cancel an approval requests

Sometimes you might want to cancel an approval request that you've sent. Possibly you made a mistake in the request, or it’s no longer relevant. In either case, the person who sent the request can Cancel it by following these steps:

1. Select the approval
1. Select **Cancel approval** in the side pane.

>[!TIP]
>You can always select the **History** tab to view the approval requests that you've canceled.

>[!NOTE]
> The cancel feature is supported on the **Create an approval (v2)** action.

## Request approvals from guest users

You can send approvals requests to persons outside your organization. To do this, use Azure Active Directory (Azure AD) guest users by [inviting users from other tenants as guests](https://docs.microsoft.com/azure/active-directory/b2b/add-user-without-invite).

When you assign a role to a guest, this gives the guest the permission required to participate in the approval process.

Now that you've created and tested your flow, be sure to let others know how to use it.

## Learn more

* View and manage [pending approval requests](approve-reject-requests.md)
* Create [sequential approval flows.](sequential-modern-approvals.md)
* Create [parallel approval flows.](parallel-modern-approvals.md)
* Install the Power Automate mobile app for [Android](https://aka.ms/flowmobiledocsandroid), [iOS](https://aka.ms/flowmobiledocsios), or [Windows Phone](https://aka.ms/flowmobilewindows).
