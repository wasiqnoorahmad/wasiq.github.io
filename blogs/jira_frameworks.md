---
layout: default
title: Blogs
# permalink: /jira_frameworks
---

# Behind the Scenes: The Complexities of Jira Integration Frameworks

## Introduction

Greetings, everyone! I’m Wasiq Noor, a young software engineer with a passion for exploring the wonders of technology through blogs. I've dabbled in various tech stacks, including AWS and GCP, and today, I'm excited to share my first blog post. In this article, I'll delve into the complexities of Jira integrations and discuss why they can be challenging.

In recent years, intra-app integrations have become commonplace. You've likely encountered sites that allow third-party sign-ups via platforms like Google, Facebook, and Microsoft. Some even support GitHub or LinkedIn integrations for code enhancements and job applications. Having had the opportunity to work on integration workflows for Google, Slack, Jira, and more, I was eager to share my experiences.

### The Jira Integration Nightmare

Working for a company that identifies critical risks in deployed clusters, we received a customer request for Jira integration. They wanted to track critical risks on a Jira ticket, assignable to an engineer within their team. Always prioritizing a seamless customer experience, we set out to minimize clicks and make the integration process efficient.

Little did we know that this seemingly simple task would turn into a nightmare.

## The Journey through Atlassian Frameworks

To attract a broader audience, we decided to publish our app on the Jira Marketplace. Atlassian offers two frameworks for building apps - Forge and Connect. As we delved into the documentation, we discovered that Atlassian prefers Forge over Connect. However, Forge apps aren't designed for seamless integration with third-party tools, as they are hosted exclusively on Atlassian servers.

### Forge Framework

Atlassian strongly recommends Forge for app development within its ecosystem. As we delved into the documentation, we discovered that Forge relies on Atlassian's hosted servers, limiting its integration capabilities with third-party tools. Forge apps lack server support within the app, making it challenging to initiate conversations with external tools. Essentially, Forge is an app-building platform that resides exclusively within Atlassian Jira workspaces, suitable for certain use cases but not conducive to our integration needs.

### Connect Framework

Connect, Atlassian's legacy framework for building marketplace apps, allows developers to host apps on their premises. Despite its promise, exploring Connect revealed sparse documentation and minimal guidance. Intrigued by on-premises hosting, our team created a Proof of Concept (POC). However, Connect posed challenges, requiring a dedicated storage interface for preserving access tokens. While Connect supports default integration with popular databases like Dynamo DB, the need for a dedicated table raised concerns about disrupting our existing database design. Similar to Forge, Connect lacked a clear mechanism for initiating communication with the Atlassian app, adding complexity to our integration efforts.

Navigating the intricacies of Forge and Connect frameworks pushed us to explore alternative solutions for our Jira integration needs.

## 3-legged OAuth (3LO)

Designed to support third-party integrations, 3LO presented a compromise. While it allowed third-party apps to perform operations in a user's Jira workspace, publishing an app on the marketplace became challenging. Operating on behalf of the user introduced complexities, such as the app becoming invalid when the Jira user was removed or deactivated. The time-limited authentication tokens and refresh token restrictions further complicated matters.

3LO is a Jira integration method designed to support third-party applications. While it addresses some integration needs, it comes with specific challenges. Unfortunately, opting for 3LO often requires compromising on the goal of publishing an app on the marketplace.

### Integration Mechanism

3LO enables third-party apps to perform operations within a user's Jira workspace. However, this comes at the cost of the app operating on behalf of the user. This approach poses challenges, especially when the Jira user is removed or deactivated from the workspace, rendering the integration invalid.

### Token Expiration and Refresh

Authentication tokens provided by 3LO have a time limit of 60 minutes. After this period, the tokens expire, requiring reacquisition using a refresh token. Notably, the refresh token itself has a hard limit of one year. Once this limit is reached, developers must integrate the app again.

To add another layer of complexity, if the refresh token goes unused for 90 days, the integration becomes invalid. This necessitates setting up scheduled jobs for all integrated customers to keep their tokens refreshed and maintain the functionality of the integration.

### Downsides and Compromises

While 3LO allows third-party apps to interact with a user's Jira workspace, the compromises and limitations make it less favorable. Operating on behalf of the user raises concerns about the validity of the integration, and the token expiration intricacies add an extra layer of maintenance.

Despite the challenges, our team had to opt for 3LO to achieve the integration goals, acknowledging the additional cost and complexities involved in maintaining token validity.

## The Frustration: Why Every Solution Falls Short

Our primary goals were simple:

1. Gain visibility on the Jira marketplace.
2. Support our customers in creating Jira tickets.

Unfortunately, with Forge, Connect, and 3LO, Jira SDK support was limited, forcing us to abandon goal for publishing on marketplace. Additionally, the lack of support for connecting with Jira hosted apps externally led us to settle for 3LO, with the added burden of setting up refresh token jobs to maintain integration validity.

While our product now supports creating Jira tickets, the seemingly simple workflow has turned into a challenging ordeal.
