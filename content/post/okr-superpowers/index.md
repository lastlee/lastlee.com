---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Engage Your OKR Superpowers"
subtitle: "Become a high performing team with well-crafted OKRs"
summary: "Become a high performing team with well-crafted OKRs"
authors: []
tags: []
categories: []
date: 2019-12-18T08:21:15-08:00
lastmod: 2019-12-18T08:21:15-08:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: true

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

## What are OKRs?
OKR stands for **Objectives** and **Key Results**. This is a methodology for creating goals and continually measuring the quality of progress in achieving those goals. OKRs are how you track progress, create alignment and encourage engagement around measurable goals. While this sounds simple or idealistic, there can be huge benefits from a well-engineered OKR program within your organization.

## Who uses OKRs?
Many organizations use OKRs in a variety of different ways. Some may not call them OKRs, but at the very least, setting goals and periodically measuring progress is a common practice for nearly any organization. The degree to which they are successful largely depends on how engaged the employees are with the objectives. **[Measure What Matters](https://www.goodreads.com/book/show/39286958-measure-what-matters)**, written by John Doerr, captures the stories of many companies successfully using OKRs, how they became successful and the attributes of the OKR programs.

## How most companies use OKRs
Several organizations I have been in have used OKRs to a small degree of success. It is fairly common to see the same patterns:
1. Leadership determines that OKRs will be the direction we must go
2. Management will watch a TED Talk and quickly become an "expert"
3. Some form of Objectives will be set, along with a variety of KRs
4. Individual contributors are made aware of this policy and generally remain doing the same work but have to figure out how to label their user stories with the new system
5. Engagement dies down after a couple quarters
6. OKRs are only mentioned in a quarterly all-hands
7. Cycle continues while resentment builds up

While this pattern happens naturally, it is not the intention, nor is it ideal. We can do better.

## What we learned
While at Autodesk, we had a very similar deployment of the initial version of OKRs. There was no great management system to keep track of the OKRs, and the only people invested in doing any work associated with the OKRs were the managers who saw it as an opportunity to look good to senior leadership. This was clearly counter-productive to the spirit of the objectives, and we had a realization that we needed to address this. We took a look into the data where we could begin to understand what the problem space entailed. With dozens of teams in an organization of around 1100 employees, we had a sufficient dataset to group the Objectives and Key Results into affinity clusters. The parameters we used to group the objectives were as follows:
**Objectives**
- Length (word count)
- Primary verb
- Grammatic structure

**Key Results**
- Contains a number

With these facets, we were able to group similar Os and KRs and found them generally to be correlated with similar authors. For example, several of the same people tended to have objectives that were lengthy, possibly even multiple sentences in length. Other people tended to have much shorter Objectives, etc.. With these groups, we ran a correlation to another dataset that was used to evaluate Agile Maturity by industry standard methods. This is when the patterns of quality started to emerge.

## Research and results
We identified a high correlation between high performing teams and the quality of their OKRs. Using natural language processing, we studied the grammar, sentence structure and quality of the words most commonly used. Quality was evaluated by scoring all of the primary verbs and assigning a weight for each. These teams had the following characteristics of their Objectives:
- Very short and concise. Average around 6 words for each objective.
- Primary verb was either the first or second word
- Primary verb was impactful and actionable

And the Key Results tended to show these characteristics:
- Measure a single metric at a time
- Always contain a number as the target
- Use numerically measurable attributes for areas that typically are hard to measure, like CSAT and NPS

Here's a sample list of verbs and qualifying adverbs used that were highly rated:

| Verbs | Qualifying Adverbs |
| -----:| ------------------:|
| eradicate | radically |
| delight | sustainably |
| eliminate | thoughtfully |
| accelerate | compassionately |
| drive | dramatically |
| engage |
| disengage |
| charter |
| instill |
| disrupt |
| impress |
| challenge |
| empower |

What we concluded was there tended to be a simple sentence structure that achieved the best result:

Define your objective generally with the following pattern: (optional) qualifying adverb -> objective imperative verb -> object -> (optional) to/from state

**Examples of great objectives:**

* Delight customers with resilient cloud products
* Drive construction products to materialization
* Empower users to create new content

**Examples of great KRs:**

* Cloud products maintain 99.9% SLA as measured by synthetic login, launch and load metrics
* Mean time to remediation is less than 10 minutes on average
* Construction customers hit 20,000 daily active users

It is particularly important to include a number in the key result to indicate the level of quality that is expected with the outcomes the team is trying to achieve. Without that motivation for quality, solutions can be reached with a lower level of quality than desired.

We challenge OKR authors to create objectives in five words. This is a huge challenge, but fake bonus points are awarded to those who can create an engaging objective in five words. We believe this will help everyone remember what it is they are working towards, keeping the memorable objective top of mind every day.

## Changing the language
As this new OKR program 2.0 was being rolled out during an organizational transformation, the particular language we used to convey our intentions needed to match the languaged used to describe the structure of the organization, according to Conway's Law. The new organization had been advertised as a matrix structure, much flatter and had allowances for new communication pathways that had not existed before. This compression of hierarchy into an undirected graph necessitated new ways to describe communications. Lera Boroditsky and Guy Deutscher argue that language shapes the way we think and affects our culture. So we determined the best application of this line of thought is to remove certain words that imply hierarchy to our conversation around OKRs. Words and phrases like: trickle-down, cascade, skip-level, pass-down, roll up, percolate up were all removed from our vernacular. Instead, we replaced those words with the parlance of [Graph Theory](https://en.wikipedia.org/wiki/Graph_theory), and words like feedback cycle, traverse, etc.

## Passive engagement
With these changes, we see teams refining their objectives to be shorter and KRs to be more measurable such that everyone involved knows right away what it is they are working toward, and how they can measure their contribution toward success. Having the individual contributors know the objectives will significantly help during sprint planning and standup.

## Conclusion
This is an evolution of the approach to using OKRs effectively. We would like to see higher quality OKRs spread across the industry to create higher engagement and interest from the individual contributors.
