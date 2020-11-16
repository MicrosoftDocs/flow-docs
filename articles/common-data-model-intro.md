---
title: Microsoft Dataverse | Microsoft Docs
description: Create a flow from a template that uses Microsoft Dataverse.
services: ''
suite: flow
documentationcenter: na
author: msftman
manager: kvivek
ms.service: flow
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/17/2020
ms.author: deonhe
search.app: 
  - Flow
search.audienceType: 
  - flowmaker
  - enduser
---
# Create a flow that uses Microsoft Dataverse

[!INCLUDE[cc-data-platform-banner](./includes/cc-data-platform-banner.md)]

Improve operational efficiency with a unified view of business data by creating flows that use [Dataverse](https://powerapps.microsoft.com/tutorials/data-platform-intro/). 


For example, you can use Dataverse within Power Automate in these key ways:

* Create a flow to import data, export data, or take action (such as sending a notification) when data  changes. For detailed steps, see the procedures later in this topic.
* Instead of [creating an approval loop through email](wait-for-approvals.md), create a flow that stores approval state in an entity, and then build a custom app in which users can approve or reject items. For detailed steps, see [Build an approval loop with Dataverse](common-data-model-approve.md).

In this article, you will create a flow that sends an email notification when a *Qualified Lead Process* creates a new *Opportunity* in Dataverse. The notification includes the *Notes* from the *Lead*.

## Prerequisites

* Sign up for [Power Automate](https://flow.microsoft.com) and [Power Apps](https://make.powerapps.com).
  
    If you have trouble, verify whether [Power Automate](sign-up-sign-in.md) and [Power Apps](https://powerapps.microsoft.com/tutorials/signup-for-powerapps/) supports the type of account that you have and your organization hasn't blocked signup.
* If you haven't used Dataverse before, create a [Dataverse environment with a database](https://docs.microsoft.com/power-platform/admin/create-environment#create-an-environment-with-a-database) in the Power Platform admin center.

## Sign in to your environment

1. Browse to [Power Automate](https://flow.microsoft.com), and then select **Sign in** in the upper-right corner.
   
    ![Sign in](./media/common-data-model-intro/signin-flow.png)
1. In the top right menu you select the environment in which you created the database in powerapps.com.
   
    >[!IMPORTANT]
    >If you don't select the same environment, you won't see your entities.
   
    ![Select environment](./media/common-data-model-intro/select-environment.png)

## Use a template

1. In the **Search for a template by app, task, or industry** box at the top of the screen, enter **common**, and then press **enter**.

   You will see a list of templates with the word "common" in their names, including those templates that use Common Data Model.
   
    ![Search for templates](./media/common-data-model-intro/template-search.png)

1. In the list of templates, select the template that performs that tasks that you want to be performed.
   
    For example, select the template that copies notes from Lead to Opportunity in Dataverse, as shown in the steps that follow.
   
    ![Choose a template](./media/common-data-model-intro/select-template.png)
   
1. If you haven't already created a connection, select **Sign in**, and then provide your credentials as needed.
   
1. Select **Continue**.

   You'll now see the template and its connections. In the following steps, you will customize this template.

## Customize your flow template

1. On the **When an Opportunity is created** card, select the **Environment**, **Entity Name**, and **Scope** that you want to use.
   
    ![Specify the details for the entity](./media/common-data-model-intro/specify-instance.png)

1. Complete the **Get Opportunity Record** card, per your requirements.
   
    ![Get Opportunity Record](./media/common-data-model-intro/get-opportunity-record.png)

1. Configure the **Originate from a Lead** card. 
   
    ![Originate from a Lead](./media/common-data-model-intro/originate-from-lead.png)

1. Complete the **Get Lead** and the **List Notes for the Lead** cards on the **If yes** side of the decision branch. 

   ![Complete decision branch](./media/common-data-model-intro/get-lead-list-notes.png)

1. Expand the **Apply to each** card, and then  delete the **Copy Lead Note to New Note** card.

1. Select **Add an action**, search for **notification**, and then select **Send me an email notification**.

   ![Email notification](./media/common-data-model-intro/apply-to-each.png)

1. Configure the notification card to send you an email notification with the details of the notes for the lead.

   ![The notification card](./media/common-data-model-intro/notification-card.png)


>[!TIP]
>If you can't find a template that does what you need, you can [build a flow from scratch](get-started-logic-flow.md) that operates on top of Dataverse.

