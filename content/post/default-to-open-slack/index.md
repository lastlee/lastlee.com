---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Communicate Effectively with Slack at Scale"
subtitle: "Empower people with inclusion to yield high quality conversations on Slack"
summary: "Increase productivity and collaboration with Slack"
authors: []
tags: ["slack", "communication", "psychological safety"]
categories: []
date: 2019-12-16T23:00:51-08:00
lastmod: 2019-12-16T23:00:51-08:00
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

Tens of millions of users around the world use Slack every day, but is Slack being used effectively in your organization? I was a part of a team at Autodesk that managed the workspace's 12,000+ users with the goal of supporting the communication platform at scale. How did we manage to leverage human behavior patterns to foster a creative, diverse and inclusive community while managing the prevention of silos and the descent into chaos?

## Culture is an Evolution
Culture evolves every day and your strategy must allow for adaptation. One of the fundamental policies we encouraged each team to practice is to gather feedback and iterate on changes. Ask the team:
- What is working well with Slack?
- What is not working well with Slack?
- How might we improve our approach to communication?

By gathering this feedback from the team, patterns will emerge in the data which will inform you of what to keep doing, what to change and wildcard for good measure. On my immediate team, we gathered this feedback monthly, as the timing seemed to be about right for the impact of the changes. Initially, we observed very clear patterns in the data that people had a hard time managing the number of channels, the volume and velocity of conversations and the quality (noise) of the messaging. Some channels were being misused according to their name or purpose, and other channels people felt had an extremely valuable purpose, but the noise reduced the quality of the content. First, we took inventory of the scope of our channels:
1. Team channel
2. Alerts channel (one per environment)
3. Deployments channel
4. CICD channel
5. etc.

With each channel, we discussed the different facets of the concerns. For example, people didn't feel comfortable broadcasting to a wide audience that participated in the team channel (about 90 people) that they had to stay home to take care of their sick daughter. It wasn't relevant to everyone outside the immediate team, nor would it have been a conversation that would happen naturally in person. Additionally, people really valued the alerts channel, and we came to find out that most people set that channel to send a push notification to their phone whenever a message was delivered to that channel. Instead of changing the behavior of the users to not pay attention to the alerts, we determined the best way to increase the quality of the communication was to establish guardrails around how the alerts channel was used. Only send a message to the channel if there is an incident or a possible anomaly worth distracting engineers from their scheduled work. Update the monitoring and alerting bots that posted to that channel by diligently refining the alerts to be meaningful and actionable, etc..

The result of the refinement based on the feedback was that we began archiving unnecessary channels that nobody found value in, renaming channels to be more appropriate (Deployments was rarely about deployments, so it became a Discuss channel), and created channels that were team members only (not private, but with an express purpose to be team members only).

## Default to Open Policy
On the broader scale, the Slack Admins instituted a policy across the entire company to **Default to Open**. This means we will enforce rules that encourage open, honest and transparent conversations while making it a safe place to do so for anybody in an inclusive manner. To provide guardrails around this policy, we limited the creation of private channels to Slack Admins only. Users could request a private channel be created for the following criteria:
1. Finance discussions
2. Legal discussions
3. HR/Personnel discussions
4. Discussions concerning patentable IP
5. External vendors under NDA

By limiting private discussions to these criteria, almost all valuable conversations happen in public channels that positively encourages cross-domain observation of knowledge and the provides the opportunity for others to contribute to those discussions. In many cases, we saw one team discussion their approach to solve a problem and someone from another team or department chime in to share how they already solved that problem.

Of course direct messages and group DMs exist, but their value is limited by their inflexibility. While the analytics did indicate DMs were still used heavily in terms of message count compared to public channels, we attributed that statistic to the quality of conversation happening in direct message. People tend to be much more verbose in DM resulting in a skewed message count.

## Channel Naming Convention
Early on in the formation of Slack, naming convention patterns started to form, but tended to not be consistent. The Slack Admins created a modifiable post in the Slack Help channel that listed consistent naming conventions, for example:

**Geographic Channels**

#sf-* \
#lon-* \
#pdx-* \
#bos-*

**Autodesk Specific**

These were mandated to be specifically relevant to the whole company

#adsk-general \
#adsk-announcements \
#adsk-*

**Technology Specific**

#tech-terraform \
#tech-aws \
#tech-python \
#tech-*

**Fun**

#fun-cats \
#fun-dogs \
#fun-*

**Product/Team**

#mktg-* \
#bid-* \
#rcw-*

**Private Channels**

priv-*

## Diversity and Inclusion
While diversity and inclusion has been a trending topic in the industry for a little while, the Slack Admins take this practice seriously. In order to create an environment where people feel safe to be themselves and take risks in communicating openly, we made sure to respond quickly and justifiably when needed. We prevented users from creating and adding custom emojis and required them to request a Slack Admin add it for them in order to review and approve. In some cases, emojis consisting of an employees face and name (not the requestor) would be reviewed and we would seek direct approval from the employee whose face it was. Other inappropriate for safe work culture were denied as well. As such, we all made an effort to be participants in corporate diversity and inclusion resource groups and promoted diversity among the Slack Admins ourselves.

## Conclusion
We set out with the goal of breaking down silos and increasing transparency by communicating by default in an open manner. By leveraging the dynamic and organic nature of Slack, we allowed users to organically develop and optimize their processes while providing guardrails around practices that went against an open and inclusive culture.
