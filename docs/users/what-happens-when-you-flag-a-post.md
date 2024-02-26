---
tags:
  - Flag
  - Moderation
---
# What happens when you flag a post

## What happens when you flag something?

> :mega: Site admins are given significant flexibility via Site Settings to adjust how flags work. This topics assumes that all site settings are set to their *default*. Many of the automatic options presented here, like hidden posts, closed topic, etc. can be disabled or made to require more or less flags before triggering. For full details on flag handling by staff, see the section on [Flags](https://meta.discourse.org/t/discourse-moderation-guide/63116#flags-13) in the https://meta.discourse.org/t/discourse-moderation-guide/63116.

### Single flag
When a user flags a post, it appears in the review queue. Staff, as well as category moderators, can then review the flagged content to decide what to do. Options may include agreeing with the flag, disagreeing with the flag, and ignoring the flag. Additionally, staff can hide the post, triggering an automatic PM to the user encouraging them to edit the post; silence the user; suspend the user; or delete the post. 

Flags from some well trusted users might perform automatic actions like hiding. If a user has a high trust level and their previous flags have been agreed with often by moderators, their flags will be more likely to automatically hide bad content. 

### Multiple flags

If a post receives multiple flags before staff can handle it via the review queue:

1. "Enough" users flag a post. This could be 3 trust level 1 users, 2 trust level 2 users, or a mix.

2. The post in question is *immediately* hidden:

    - the post author sees 

        > Your post was flagged by the community. Please <a href="">see your messages</a>.

    - the community sees 

        > This post was flagged by the community and is temporarily hidden.

    - staff sees the actual post, as posted, in a dimmed state to indicate it has been hidden for others.

3. A friendly private message is sent to the author of the post, describing what happened, and letting them know that for {flag type} a considered edit of any kind is enough to un-hide the post. 

   ![image|690x449, 75%](upload://zYN8pHpFcvuBrq2OiKYehb2osV2.png) 

    Users must wait at least 10 minutes prior to editing the post. This ensures the user stops and thinks before editing, to minimize any rash changes.

### Editing flagged posts

When a post is hidden by flags, users are given the opportunity to edit them. 

- If the post **author edits** the flagged post, the post is un-hidden. The post remains in the review queue for eventual moderator review, but is visible as usual to users again.

- If the post **author does not edit** the flagged post, it is never un-hidden, barring moderator action. If a post stays hidden for 30 days, it is automatically deleted.

### Re-flagging a post that was hidden and edited

If the **same post is hidden by a second round of flags**, the flags must now be manually handled by a moderator. The user is not given an opportunity to edit the post, as they already had that opportunity, and the community still sees an issue.

### Multiple flaggers in the same topic
Should posts in a topic receive multiple flags (exact number depends on the trust levels of the flaggers) from at least 5 unique users, the topic will be closed automatically. The topic will remain closed for 4 hours pending moderator intervention. This helps prevent heated topics from going "off the rails" before a moderator can review what is happening.

![image|690x90](upload://rdRzxHsJ0wRgJiUe5IMBoFJRakJ.png) 

### Trust level 0 users and spam flags

Trust level 0 users are brand new users to the site, and are not trusted. As such, should a trust level 0 user's post receive 3 *spam* flags, not only will the post be hidden, but the user will be silenced, preventing any further posting until a moderator reviews the user.

---
The goal here is for the *community* to be able to protect itself from the worst users, even without a moderator present. But it works even better with a moderator, as the moderator can accelerate the process by handling the flags as they come in.