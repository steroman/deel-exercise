---
id: comments
title: Comments
sidebar_position: 2
---

# Comments

This section includes some comments about how I approach the exercise and what I have found along the way. Happy to discuss more if we get the chance to debrief after the delivery of the exercise.

## Content approach

This section details how I handled the development and delivery of the 2 tasks.

### 1. Explore current documentation

I first explored the current documentation, trying to impersonate a developer who had to use it and who was trying to get started. I wanted to get a clear idea of what I had to do in order to be ready to make API calls. I paid special attention to:

- Onboarding guides such as:
  - [Docs home page](https://nmbrs.stoplight.io/)
  - [Getting Started](https://nmbrs.stoplight.io/docs/nmbrs-restapi/9c14f1c024642-getting-started)
  - [Authentication](https://nmbrs.stoplight.io/docs/nmbrs-restapi/e9e0f5292b4a1-authentication)
  - [Scenarios](https://nmbrs.stoplight.io/docs/nmbrs-restapi/c401b3cb47390-api-changelog)

I also explored other topics such as the changelog or the errors, but I considered them secondary to my task and I had to work with limited time.

### 2. Explore API reference

After I gained some familiarity with the basics, I went on and started exploring the endpoints of the API reference. I did so on both the Stoplight website and the Postman collection. I faced some issues making the Postman collection work, you can read more about it in the [Issues and blockers](#issues-and-blockers) section.

Considering that the main goal was to create a guide on how to create employees, my main focus was mostly on the [Employee-related](https://nmbrs.stoplight.io/docs/nmbrs-restapi/13c6a8d9c7190-create-employee) endpoints and the [Company-related](https://nmbrs.stoplight.io/docs/nmbrs-restapi/5fad7a8461a01-get-company-list) ones. About the latter, even if I knew that the mock API had params already embedded, I still wanted to understand the data structure, the role a company played in making the employee-related calls, and the process a real user would go through.

During this process I took notes of what needed to be done before making calls. This would become the foundation for the [Requirements](http://localhost:3000/deel-exercise/docs/employee-basics/manage-employees#requirements) section of my guide. 

### 3. Make test API calls

After that, I started to make API calls to see how the responses and their payloads matched the documentation. I first tried with Postman, then with call simulator in the Stoplight docs. I must admit that this has been the most uncertain part for me, because all my attempts were failing with either a `404` or a `400` error. I was eventually able to overcome the blockers and make API calls.

During all this process I started making notes of my steps. This would become the foundation for the [hands-on part](http://localhost:3000/deel-exercise/docs/employee-basics/manage-employees#create-employee)(employee creation and update) of the guide I had to write.

### 4. Draft article

With all my notes I then moved on to writing the draft of the article. I had an idea of writing it in Markdown and then figuring out where to publish it.

### 5. Identify tech stack

After that, I moved to the tech stack. You can read about it in the [Teck stack](#teck-stack) section.

### 4. Decisions

- In real life, what I delivered to you would be the MVP for my delivery. I think that making a deliverable that looks close to final is good because it creates a healthy feedback loop. It moves the conversation towards what works and what doesn't, rather than commenting on imaginary deliverables. Even hearing the feedback like "this is wrong" would actually be a success, because the feedback is very actionable.
- At the same time, I would hold much deeper conversations with developers and ask lots of "whys" about the architecture of the API. I believe that when something is hard to describe it's because something is not working in the way it is structured, and that such conversations are healthy and contribute to creating better products.
- My biggest issue was understanding that the prefesence of `personalInfoId` in the payload was causing the creation call to return a `400` error. I then compared the examples with the API reference and noticed that it actually wasn't there.
- I had also noticed that `personalInfoId` would be returned in the `200` response of the `PUT` call. At that point I started to doubt about whether it would be better to instruct users to create an employee without `personalInfo` data in the payload and add it afterwards through a `PUT` call or stick to the existing docs, where the employee was already created with `personalInfo`? I decided to maintain consistency with the original documentation but that's one of the things I would discuss internally with the team.
- Similarly, I had to decide whether to pretend that `personalInfoId` didn't exist at all or make it surface but warn the user that they don't need it. I went with the second option, but in real life this would be a great topic to discuss with the team: whether it's necessary to expose such param in the API calls and why. Because, if it is, then we must explain the benefits to the user.
- I decided to have all the placeholders as ALL CAPS and with words separated by an underscore to promote consistency. In real life, I'd make a more thorough research on best practices for placeholders based on where they appear (path, query, header, body, etc.) and a careful evaluation of the tradeoff of maintaining or losing consistency across different touchpoints (Prose DOCS, API reference, Postman collection, etc.).
- In the guide, I reflected on whether to add `personalInfo` data in the call and create a longer payload or cut data from there and point users to the `personalInfo` object or the creation call. I decided to cut it.

## Teck stack

I used [Docusaurus](https://docusaurus.io/) and deployed it using GitHub Pages. The rationale being that this would be a tech stack close to Stoplight and because Markdown is quite platform agnostic, so this would make it easily portable. Docusaurus supports CommonMark and has very minimal custom elements for Markdown (such as the admonitions).

The docs-as-code approach has many other advantages. From the version control provided by `git` to the possibility of peer reviews provided by GitHub or adding automatic checks using style linters like [vale](https://vale.sh/). 

I also saw some added value in choosing an open-source solution, both from the budget and security perspectives.

## Issues and blockers

Here's some of the issues I found along the way. I thought to record them as they could make for a nice bucket of tasks to tackle in the future by the team. I always make a habit of recording issues so that I always have a pool of improvements to choose from based on the strategic priorities.

- There's inconsistencies between the Postman collection and the Stoplight docs:
  - Conflicting information about the mock server's URL
  - Examples containing
  - Using the mock server URL provided in the [docs home page](https://cffbdec8-71af-4a71-81d7-43321211e7c9.mock.pstmn.io) leads to 404s
- Button "Run in Postman" has issues when choosing the "View collection" or "import a copy" options. The only option working is the "Fork Collection"
- Instructions aren't linear. For example, we explain how to select the Mock server in Postman without explaining how to create it first.
- About the previous point, a big part of the getting started documentation is about how to handle the manage the server in Postman. It's safe to assume that our audience can use Postman and, if not, knows how to learn how to use it. Our job is to point them to the right resources. Not rewriting them also helps reducing maintenance costs, because it will reduce the need to update the docs every time Postman releases a new update and our docs become obsolete. Instead of doing that, I'd find a way to point them to the original Postman docs about how to fork. If using Postman is the only way to play with the API, then it can be transformed into a requirement.
- The goal of a "hello world" is to create a "A-HA!" moment and make them realise the value of the API as early as possible. There's conflicting information that delays this moment. For example, the first section of the home is [Get credentials](https://nmbrs.stoplight.io/#get-credentials). In that section we point users to https://developer.nmbrs.com/docs, which lists a lot of steps to obtain credentials. Those aren't needed right away, so they can be placed at a lower hierarchical level in the user's onboarding.
- Some examples (placeholder values) in the documentation are in Dutch. On one hand, this conveys a lack of care and a sense of poor quality. On the other, it increases the friction for users who are not familiar with the language.
- Inconsistencies between the examples (Postman or API reference) and the YAML part. The biggest example is `personalInfoId`. The fact that it's present in the examples is causing lot of trouble. Also because the message of the 400 error talks about a "Hour component" that is not mentioned anywhere in the docs. This inevitably leads to dead ends for users. But other inconsistencies are for example that in the management of the employee, the personal information is sometimes contained within the `personalInfo` object (`POST`) and sometimes it is not (`PUT`).
- There's also some inconsistencies in marking which parameters are required and which ones are optional in API calls.
- The concept of "Company" is very important for the creation of an employee, because they can't be created without a company (which is passed as a URL parameter). However, it's not tackled in the documentation. The main point for me is that the docs don't explain how to create one, but also don't explain why it can't be created.
- There's some redundant information surfaced. For example the `personalInfo` and the `CreatePersonalInfo` objects. I'm wondering whether they need to be there in the first place and what's their added value.
- All the above issues contribute to a lack of "self-serve" for the API and to making the learning curve quite steep, which is probably the cause behind users needing to contact support all the time. If I had to place a bet on why this is happening, I'd say that it's because the documentation grew very organically and was often crafted with an outside-in perspective and without empathizing with the intended audience. The feeling after using the documentation to do the exercise is that content is optimized for an internal and advanced audience who's already very familiar with the intricacies of the system, but not for who consumes the documentation: an external and entry-level audience. But that's just a guess that's based on a lot of missing context on my side.
- There are many pages or URLs with conflicting information, which makes it hard to understand which one is the most reliable. One example: the information in the [developer site](https://developer.nmbrs.com/docs#T8uKy) and the [Stoplight docs](https://nmbrs.stoplight.io/docs/nmbrs-restapi/e9e0f5292b4a1-authentication).
- Some style issues
  - Inconsistent placeholder values / variables. For example, `:companyId` in Postaman vs `{companyId}` in API reference
    - Inconsistent casing of objects. For example, `PersonalInfo` and `personalInfoId` follow respectively TitleCase and camelCase.
  - I've found some important concepts that I'd like to see clarified in order to gather more confidence in what I was doing. For example, the meaning of "registering an app".
  - Implying that something is easy with expressions like "It's a piece of cake" is not considered inclusive. Ease of use can vary from person to person.
  - Language issues and incorrect grammar in English