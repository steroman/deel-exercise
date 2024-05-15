---
id: comments
title: Comments
sidebar_position: 2
---

# Comments

## Teck stack

## Content approach

## Issues and blockers



This section includes some comments about how I approach the exercise and what I have found along the way. Happy to discuss more if we get the chance to

404s
API onboarding is poor -> hello world is very large because the information is very scattered, postman collections don't work, mock servers are not working
Instructions lead to dead ends. For example, "Select the environment mock server", and it doesn't work.
Inconsistent placeholder values / variables. For example, `:companyId` in Postaman vs `{companyId}` in API reference
Examples in dutch
There's missing information about what 'personalInfoId' is and it's causing lot of trouble.
What params are required, what aren't?
Dead ends. For example, we don't tell them how to create a company. Can they? If they can't, why not?
Inconsistent information, for example, the personal info object and CreatePersonalInfo

There's an audience problem. This is optimized for an internal and advanced audience. It should be optimized for an external and entry-level audience.
It's a lack of self-serve, where users can retrieve each and every information they need.
Terminology consistency etc. For example: what does it mean to "register an app"

Open questions

- What are the questions they ask/issues they face that cause them to call or reach out?

I wanted to create a feedback loop by getting the document out there and validating. Hearing the feedback "this is wrong" would actually be a success, because it would spark conversation around what's wrong and why.

Expose the gaps of our current documentation

Probably a great way would be to ask a developer to record a video of how they set everything up and reproduce the end-to-end flow.
This would also expose points of friction that keep the process from becoming fully self-serve and could also drive roadmap

Too many sites and conflicting info, hard to understand which one is the most reliable. Monitor and prioritise sites to decommission. For example, either Stoplight or proprietary. Having duplicated info on both creates maintenance and duplication issues, as well as create confusion for users. In a previous company, we solved it by leaving the sections in both the docs and the API reference, but making the API reference point to the docs via links.

A big part of the getting started documentation is about how to handle the manage the server in Postman. That's a waste of quite a scarce resource: the user's attention. I think it's safe to assume that our audience can use Postman and, if not, knows how to learn how to use it. Our job is to point them to the right resources. Not rewriting them also helps reducing maintenance costs, because it will reduce the need to update the docs every time Postman releases a new update and our docs become obsolete. Instead of doing that, I'd find a way to point them to the original Postman docs about how to fork. If using Postman is the only way to play with the API, then it can be transformed into a requirement.



Considerations

- I decided to have all the placeholders as ALL CAPS and with words separated by an underscore to promote consistency. However, in real life, I'd make a more thorough research on best practices for placeholders based on where they appear (path, query, header, body, etc.) and a careful evaluation of the tradeoff of maintaining or losing consistency across different touchpoints (Prose DOCS, API reference, Postman collection, etc.).
- Reflection on whether to add sample data in the call and create a longer payload or cut data from there and point users to the PersonalInfo object
- There's gaps around how companies come to exist in the system. There's no way to create them and not much explanation. The more I look at it, the more 