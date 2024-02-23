# How public Discourse sites are indexed by search engines like Google

While Discourse is a JavaScript application, it can still be crawled by Google and other search engines.

Discourse is designed in such a way that the entire content can be crawled by bots with or without JavaScript.

We ship `NOSCRIPT` tag containing topic list and topic content. 

Additionally old browsers with old JavaScript engines will fallback to a simple read-only view. 

To view the JS disabled view, you can either install a plugin in Chrome/Firefox that disables JS or disable using [these instructions](https://developers.google.com/web/tools/chrome-devtools/javascript/disable).

Here is an example of how meta is rendered to Googlebot:

![image|362x500](upload://ga2z2DB928b3C2U6PTNw8Pw8XsD.png) 

Note that when using the no JS rendering we include pagination.

![image|690x305, 75%](upload://1jWBihS6kJp1vAJ0pDuIVE2ttNU.png)