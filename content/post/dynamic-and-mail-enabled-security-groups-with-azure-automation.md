+++
categories = ["Exchange", "Automation", "Azure"]
date = 2022-01-08T23:00:00Z
description = "Dynamic AND Mail-enabled security groups are a highly wanted feature. This article describes how to achieve this using Azure Automation."
image = "/images/blog/eric-krull-ejcuhcdfwrs-unsplash.jpg"
title = "Dynamic AND Mail-enabled security groups with Azure Automation"

+++
Dynamic AND Mail-enabled security groups are a highly wanted feature in Azure AD and Exchange Online. This article describes how to achieve this using Azure Automation.

## The need for "dynamic" mail-enabled security groups

Mail-enabled security groups are very useful and versatile. They can be used in both Exchange Online and Azure Active Directory to distribute email and secure resources, among other things.

> Like a distribution group, a mail-enabled security group provides a single point of contact for delivering email to the members of the group. However, a mail-enabled security group is also a _security principal_, which means you can assign permissions to the group that affect all group members who are also security principals (user mailboxes, mail users, other mail-enabled security groups, etc.).

(Quote from [Recipients in Exchange Online | Microsoft Docs](https://docs.microsoft.com/en-us/exchange/recipients-in-exchange-online/recipients-in-exchange-online))

A limitation however, is that mail-enabled security group only allows for static membership by default. You can of course add and remove users from groups as needed, but this is often a manual and time-consuming process. There's also a risk of mistakenly adding users to the wrong group or forgetting to adding new users etc. This might lead to security incidents such as unwanted permissions or information not being distributed as intended.

### Dynamic group options in Azure AD and Exchange Online

Just to make things clear, the concept of dynamic groups already exist in the Microsoft 365 cloud platform:

* **Dynamic Security Groups** can be created in Azure AD. This kind of group can not however be mail-enabled currently.


* **Dynamics Distribution Lists** in Exchange Online uses rules and queries to determine members. These are executed when an email is sent to the list and there is no easy way for end-users to see who will receive the message.

_Photo by_ [_Eric Krull_](https://unsplash.com/@ekrull?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) _on_ [_Unsplash_](https://unsplash.com/s/photos/robot?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)