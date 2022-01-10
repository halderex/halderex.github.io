+++
categories = ["DRAFT", "Exchange", "Azure Automation"]
date = 2022-01-08T23:00:00Z
description = "Dynamic AND Mail-enabled security groups are a highly wanted feature. This article describes how to achieve this using Azure Automation."
image = "/images/blog/eric-krull-ejcuhcdfwrs-unsplash.jpg"
title = "Dynamic AND Mail-enabled security groups with Azure Automation"

+++
DRAFT, IN PROGRESS! Dynamic AND Mail-enabled security groups are a highly wanted feature in Azure AD and Exchange Online. This article describes how to achieve this using Azure Automation.

***

## The need for "dynamic" mail-enabled security groups

Mail-enabled security groups are very useful and versatile. They can be used in both Exchange Online and Azure Active Directory to distribute email and secure resources, among other things.

> Like a distribution group, a mail-enabled security group provides a single point of contact for delivering email to the members of the group. However, a mail-enabled security group is also a _security principal_, which means you can assign permissions to the group that affect all group members who are also security principals (user mailboxes, mail users, other mail-enabled security groups, etc.).

(Quote from [Recipients in Exchange Online | Microsoft Docs](https://docs.microsoft.com/en-us/exchange/recipients-in-exchange-online/recipients-in-exchange-online))

A limitation however, is that mail-enabled security group only allows for static membership by default. You can of course add and remove users from groups as needed, but this is often a manual and time-consuming process. There's also a risk of mistakenly adding users to the wrong group or forgetting to adding new users etc. This might lead to security incidents such as unwanted permissions or information not being distributed as intended.

### Dynamic group options in Azure AD and Exchange Online

Just to make things clear, the concept of dynamic groups already exist in the Microsoft 365 cloud platform:

* **Dynamic Security Groups** can be created in Azure AD. This kind of group can not however be mail-enabled currently.
* **Dynamics Distribution Lists** in Exchange Online uses rules and queries to determine members. These are evaluated when an email is sent to the list and there is no easy way for end-users to see who will receive the message.

Wouldn't it be awesome if you could combine these two group types? Having fully dynamic AND mail-enabled security groups, with membership visibility to email senders and the ability to use the same groups as security principals in Azure and Microsoft 365! What a dream...

## Azure Automation to the rescue!

I recently came across the requirement of "dynamic" mail-enabled security groups at a client who has multiple companies in the same Azure AD and Microsoft 365 tenant. Each company of course has different departments and staff are spread over various countries. On top of that, there are numerous teams with members that change over time and where individuals can be part of multiple teams. Then there's the aspect of differencing employees from consultants... Quite a complex scenario but surely not an uncommon one. Automating the process of keeping groups up to date would be a huge time-saver and make life so much easier for the it administrator. 

### Planning the solution

When planning for automation, a first step might be to note down the manual steps required to complete the tasks. From here, one can iteratively refine and optimize the process to make it lean and efficient.

A starting point for create and update dynamic mail-enabled security groups could be:

1. Determine a policy on what user attributes to use for different purposes and a guideline on how to populate them.
2. Define and create mail-enabled security groups as required by the organization together with rules for group membership, based on user attributes.
3. For each group:

   a.  Search the directory for users whose attributes match the defined rules.

   b. Add and remove members as needed.

Next, we need to figure suitable tools to use. When working with Azure Active Directory and Exchange Online, Powershell is always close at hand and in this case, the [Exchange Online Management Module](https://docs.microsoft.com/en-us/powershell/exchange/exchange-online-powershell-v2?view=exchange-ps) should have all the "cmdlets" we need.

### Future improvement

In my implementation I initially created the mail-enabled security groups manually. An improvement would be to either use a script for this task or, even better, have the Azure Automation Runbook create missing groups before populating them.

### References, sources and inspiration

* [About the Exchange Online PowerShell V2 module | Microsoft Docs](https://docs.microsoft.com/en-us/powershell/exchange/exchange-online-powershell-v2?view=exchange-ps)

***

{{< center >}}_Photo by_ [_Eric Krull_](https://unsplash.com/@ekrull?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) _on_ [_Unsplash_](https://unsplash.com/s/photos/robot?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText){{< /center >}}