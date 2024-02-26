
---
tags:
  - Notifications
  - Settings
---
# How does the notifications menu work?

Ding! ⏰

In Discourse, you'll come across several types of notifications.
Most of them will pop up near your avatar at the top right. As for chat-related notifications, they'll appear on the chat icon.

Notice a green envelope icon on your avatar? It's indicating you have a new personal message.
Likewise, a green counter on the chat icon shows you've received a personal chat message.
![image|146x60](upload://bZ7FfQlz3gJnrACCpVb3siOEetv.png)

If there's a blue counter on your avatar, it's to tell you about other notifications.
A blue counter on the chat icon? This points to unread messages in chat channels.
![image|146x60](upload://gqflvuAH5tPucD3ftvkIoF46CTM.png)

For the moderators out there, you might see red flag icons on your avatar.
These flags are there to tell you that there are items to review, like user registrations, posts to approve, flagged posts, and so forth.
![image|60x60](upload://A8dEkAheFJ1gp4P1IK0bizU2783.png)

Clicking the chat icon will open the chat window. Here you can see which users and channels the notifications are linked to.
![image|402x317](upload://xVY7TkC31sH8eYniH7hxM4uf2o.png)

Clicking your avatar will remove the notification icon, and show all the unseen notifications in a menu containing several tabs.
![image|198x500](upload://88ahCDZScITTEQgqSiZYoVVeafb.png)

Notifications that you haven't checked out yet will appear with a highlighted background at the top of the list. You can click on each icon on the right to list all the notifications of that type.
![image|364x430](upload://79cZu2dSaiZ1FBOHIWWyOqVTkqL.png)

Tapping the <kbd>✔️ Dismiss button</kbd> will mark all the notifications from the current tab as read.

Here's a rundown of the notification types, from top to bottom.

|Icon|Notification types|
|-|-|
| <img src="https://d11a6trkgmumsb.cloudfront.net/original/4X/a/c/6/ac626c73be2d63c1b5173a2e290f3973cc0976fc.png" alt="All notifications"> | All notifications  |
| <img src="https://d11a6trkgmumsb.cloudfront.net/original/4X/8/3/0/830d58ff5dae8533879681f60fe0044debb36d72.png" alt="Replies and mentions"> | Replies and mentions |
| <img src="https://d11a6trkgmumsb.cloudfront.net/original/4X/9/8/6/98669caffff7cccac87fb60a9c6c6b6751b322b8.png" alt="Likes"> | Liked posts |
| <img src="https://d11a6trkgmumsb.cloudfront.net/original/4X/c/b/a/cba0aeee8edb19037290f4823258c154cf0b52a1.png" alt="Personal messages"> | Personal messages |
| <img src="https://d11a6trkgmumsb.cloudfront.net/original/4X/5/4/b/54b589e47beca5f0f5701cc9bbd7074b7d431583.png" alt="Bookmarks"> | Bookmark reminders |
| <img src="https://d11a6trkgmumsb.cloudfront.net/original/4X/3/1/f/31f88e424968634fd53315da7311e28ff055dfd6.png" alt="Chat"> | Chat notifications |
| <img src="https://d11a6trkgmumsb.cloudfront.net/original/4X/0/6/2/0622b14f01ae6230f40a8ee53de06ba5c4576451.png" alt="Flags"> | Reviewable items (Moderators only) |
| <img src="https://d11a6trkgmumsb.cloudfront.net/original/4X/2/9/0/2903dfd8b35bf2e7b685ba38ae9d4c1d0b26092f.png" alt="Other"> | Other notifications, including badges grants |

For the most curious ones, you can see all the notification types in the code [here](https://github.com/discourse/discourse/blob/dc6b547ed89f652b5406489d76140b76cf8e0d1d/app/models/notification.rb#L91).