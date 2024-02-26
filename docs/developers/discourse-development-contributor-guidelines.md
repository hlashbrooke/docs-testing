---
tags:
  - Contributing
  - Development
  - Meta
---
# Discourse Development Contributor Guidelines

## Environment

Before you begin hacking on Discourse, you need to set yourself up with a good development environment.

Check out the appropriate guide for your platform:

#### All Platforms

- https://meta.discourse.org/t/install-discourse-for-development-using-docker/102009

#### Mac OS X


- https://meta.discourse.org/t/beginners-guide-to-install-discourse-on-macos-for-development/15772

#### Linux (Ubuntu)

- https://meta.discourse.org/t/beginners-guide-to-install-discourse-on-ubuntu-for-development/14727

#### Windows
- https://meta.discourse.org/t/beginners-guide-to-install-discourse-on-windows-10-for-development/75149

## Knowing where to begin

Discourse is a big project and it assumes a certain level of comfort with its underlying technologies such as Ruby and JavaScript. Figuring out exactly how much extracurricular learning you need to do before getting started on Discourse proper can be hard. Luckily there's a guide for that!

https://meta.discourse.org/t/how-to-start-building-stuff-for-discourse-if-youre-newbie-like-myself/45954?u=erlend_sh

## Plugins

Plugins are a great way get the know the Discourse internals in bite-sized portions. It’s also the gentlest way to start contributing code, because plugins don’t need to adhere to the narrow scope of the Discourse core.

Start here:

https://meta.discourse.org/t/beginners-guide-to-creating-discourse-plugins/30515

Also check out the very helpful https://meta.discourse.org/t/plugin-outlet-locations-theme-component/100673.

Need some ideas on what to build? Just have a look through the popular ideas in #feature, #plugin:extras  and the "[Most awesome plugin for Discourse](https://meta.discourse.org/t/what-is-the-most-awesome-plugin-for-discourse-that-does-not-yet-exist/31)" topic (summarize it to see popular suggestions).

## Contributing to Core

Contributing to Discourse core, i.e. github/discourse/discourse, involves a bit more process.

#### Signing the CLA

Firstly, anyone wishing to contribute to the Discourse repository MUST read & sign the [Electronic Discourse Forums Contribution License Agreement](http://www.discourse.org/cla). The Discourse team is legally prevented from accepting any pull requests from users who have not signed the CLA first.

#### Warming up with starter tasks

Browse the #starter-task tag for a list of low-complexity tasks to get you started.

#### Work through the bugs list

We have an ordered list of bugs at: https://meta.discourse.org/c/bug?order=op_likes&status=open. 

Pick a bug, any bug, and get it fixed. 

If you are going to take more than a few hours to fix it and submit a pull request, leave a note on the bug explaining you are working on it.

#### Help flesh out "Feature" topics

There are many open feature requests that need additional detail and team approval to be added to the product. https://meta.discourse.org/c/feature?order=op_likes&status=open feel free to participate on these topics. Adding additional details to the request, creating visual mockups, etc is super helpful!

Just keep in mind that not every feature is destined to be in core:

https://meta.discourse.org/t/how-do-we-decide-what-goes-into-each-release-of-discourse/20870

#### Improve performance

At Discourse we believe performance is a feature. We welcome pull requests that improve either client or server side performance. 

Be sure to focus on high impact areas, like initial load of front page, or topic view. Improving performance for a background process that is triggered monthly is usually not a priority. 

#### Improve Discourse maintained projects

Discourse maintains a large number of open source projects, they are consumed by Discourse. If for any reason you do not feel like signing a [CLA][3]  (or wish to contribute to a non-GPL project) there are plenty of MIT options:

- logster: our web gui log viewer
https://github.com/discourse/logster
- message_bus: the engine that drives all live interactions on the sites
https://github.com/SamSaffron/message_bus
- rack_mini_profiler: development and production live diagnostics 
https://github.com/MiniProfiler/rack-mini-profiler
- onebox: a Ruby gem for turning URLs into website previews 
https://github.com/discourse/onebox 
- discourse_api: our api consumer
https://github.com/discourse/discourse_api
- discourse_docker: the engine that we use to distribute discourse
https://github.com/discourse/discourse_docker 
- wp-discourse: our WordPress plugin
https://github.com/discourse/wp-discourse
- memory_profiler: Ruby 2.1 memory profiler
https://github.com/SamSaffron/memory_profiler
- ember_performance: our Ember performance test suite
https://github.com/eviltrout/ember-performance

---

## Conventions

#### Naming is CRITICAL 

We strive to have 100% parity between names of objects discussed on the site and names of classes and columns in the database. 

For example: we use the term post to describe posts on a topic. It follows that there is a "posts" table with the column "topic_id". If for any reason we decided to call "topics" say "threads", **every** instance of the word topic in the codebase and would have to be renamed to thread.  

#### Compatibility with latest versions of dependant libraries is CRITICAL

We strive to ship Discourse with the up to date dependencies. This means we ship with the latest stable version of Rails, Ruby, Ember and so on. 

We welcome contributions that help update dependencies to the latest stable. However be sure to test for regressions. 

#### Test only contributions are welcome :thumbsup: 

We welcome "test only" contributions, however be sure to focus on the right areas:

1. A process that is untested is very high priority. (For example, testing the sign-in workflow)
1. A controller action that has no testing is high priority. We strive to have a stable API, to achieve we need to ensure all controllers are tested.
1. Mocking is heavily discouraged. Only use mocking when absolutely critical. 

#### Refactoring only NOT welcome :thumbsdown: 

It is often tempting to submit PRs that improve [code climate score][4] or amend internal logic to make it more readable. 

Though we strive to have well factored code that is easy to reason about we can not afford risking regressions on a production product without immediate tangible gain. In the past we have suffered many regressions due to refactoring PRs. 

If you wish to improve an area of the code, **fix a bug** in that area and also improve the code, or **implement a feature** and also improve the code. 

## Contributing code on GitHub

*"...in 10 easy steps!"*

**1) Clone the Repo:**

    git clone git://github.com/discourse/discourse.git

**2) Create a new Branch:**

    cd discourse
    git checkout -b new_discourse_branch

> Please keep your code clean: one feature or bug-fix per branch. If you find another bug, you want to fix while being in a new branch, please fix it in a separated branch instead.

**3) Code**

  * Adhere to common conventions you see in the existing code
  * Include tests, and ensure they pass
  * Search to see if your new functionality has been discussed on [the Discourse meta forum](http://meta.discourse.org), and include updates as appropriate.

**4) Follow the Coding Conventions**

  * two spaces, no tabs
  * no trailing whitespaces, blank lines should have no spaces
  * use spaces around operators, after commas, colons, semicolons, around `{` and before `}`
  * no space after `(`, `[` or before `]`, `)`
  * use Ruby 1.9 hash syntax: prefer `{ a: 1 }` over `{ :a => 1 }`
  * prefer `class << self; def method; end` over `def self.method` for class methods
  * prefer `{ ... }` over `do ... end` for single-line blocks, avoid using `{ ... }` for multi-line blocks
  * avoid `return` when not required

> Remember: We don't accept pull requests consisting entirely of style changes. Style changes in the context of pull requests that also refactor code, fix bugs, improve functionality *are* welcome.

**5) Commit**

For every commit please write a short (max 72 characters) summary in the first line followed with a blank line and then more detailed descriptions of the change. Use markdown syntax for simple styling.

> **Don't forget a prefix!** Be sure to follow the https://meta.discourse.org/t/github-checkin-prefix-convention/19392?u=jomaxro for your commit title.

> **NEVER leave the commit message blank!** Provide a detailed, clear, and complete description of your commit! See "[How to write a Git commit message][5]" for great pointers.

**5a) Linting**

We lint our JavaScript code with [eslint](https://eslint.org/) as well as following the formatting conventions of [prettier](https://prettier.io/), and we lint our ruby code with [rubocop](https://github.com/rubocop/rubocop). All of these checks are run automatically in GitHub actions whenever you create a pull request for Discourse.

It is strongly recommended that you install our pre-commit git hooks using `lefthook`. This will run automatically every time you make a commit in Discourse core, and raise issues with the various languages and templates before you push them up and have to wait for GitHub CI to run. From project root:

```
mkdir .git/hooks
npx lefthook install
```

Depending on your code editor, there should be various tools that can run our linters and display the results inline based on the configurations we have specified in the Discourse project.

**6) Update your branch**

    git fetch origin
    git rebase origin/main


**7) Fork**

    git remote add mine git@github.com:<your user name>/discourse.git


**8) Push to your remote**

    git push mine new_discourse_branch


**9) Issue a [Pull Request](https://help.github.com/articles/proposing-changes-to-a-project-with-pull-requests/)**

Before submitting a pull-request, clean up the history, go over your commits and squash together minor changes and fixes into the corresponding commits. You can squash commits with the interactive rebase command:

```
git fetch origin
git checkout new_discourse_branch
git rebase origin/main
git rebase -i

< the editor opens and allows you to change the commit history >
< follow the instructions on the bottom of the editor >

git push -f mine new_discourse_branch
```

In order to make a pull request,

  * Navigate to the Discourse repository you just pushed to (e.g. https://github.com/your-user-name/discourse)
  * Click "Pull Request".
  * Write your branch name in the branch field (this is filled with "main" by default)
  * Click "Update Commit Range".
  * Ensure the changesets you introduced are included in the "Commits" tab.
  * Ensure that the "Files Changed" incorporate all of your changes.
  * Fill in some details about your potential patch including a meaningful title. Be sure to follow the https://meta.discourse.org/t/github-checkin-prefix-convention/19392?u=jomaxro.
  * Click "Send pull request".

Thanks for that -- we'll get to your pull request ASAP, we love pull requests!

**10) Responding to Feedback**

The Discourse team may recommend adjustments to your code. Part of interacting with a healthy open-source community requires you to be open to learning new techniques and strategies; *don't get discouraged!* Remember: if the Discourse team suggest changes to your code, **they care enough about your work that they want to include it**, and hope that you can assist by implementing those revisions on your own.

  > Though we ask you to clean your history and squash commit before submitting a pull-request, please do not change any commits you've submitted already (as other work might be build on top).

*Thank you for contributing to the Discourse open source project!*

  [2]: https://meta.discourse.org/search?q=%22pr%20welcome%22
  [3]: http://en.wikipedia.org/wiki/Contributor_License_Agreement
  [4]: https://codeclimate.com/github/discourse/discourse
  [5]: http://chris.beams.io/posts/git-commit/

--- 

*Last Reviewed by @SaraDev on [date=2022-06-01 time=18:00:00 timezone="America/Los_Angeles"]*