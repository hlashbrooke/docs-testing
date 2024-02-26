---
tags:
  - Installation
  - Debian
---
# Installing Discourse on Debian

## Work in Progress

This guide consists of the following steps:

* Installing the necessary packages
* Setting up the database
* Installing RVM (Ruby environment)
* Cloning and installing Discourse

I recommend installing discourse as different user than root. The servers set up here are not configured to be secure. Do **NOT** use this as a production environment.

## Packages to install
The following packages have to be installed:

Edit `/etc/apt/sources.list` to contain the following line:

`deb http://backports.debian.org/debian-backports squeeze-backports main`

Now update your sources: `apt-get update`

Install the following packages:

* `apt-get install build-essential git libpq-dev`
* `apt-get -t squeeze-backports install postgresql-9.1 postgresql-contrib-9.1 redis-server`

## Setting up the database (postgres)

Add the following line to `/etc/postgresql/9.1/main/pg_hba.conf` and then restart postgres `/etc/init.d/postgresql restart`.

```
host    all             all             127.0.0.1/32            trust
host    all             all             ::1/128                 trust
```

Create a user that has database create and superuser permissions.

## Installing RVM
First install the recommended dependencies:

`apt-get --no-install-recommends install build-essential openssl libreadline6 libreadline6-dev curl git-core zlib1g zlib1g-dev libssl-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt-dev autoconf libc6-dev libgdbm-dev ncurses-dev automake libtool bison subversion pkg-config libffi-dev`

Then installing RVM is as easy as executing `\curl -L https://get.rvm.io | bash -s stable --ruby`


## Installing  discourse

```
git clone git://github.com/discourse/discourse.git
cd discourse
bundle install
```

Edit the file `config/database.yml` to include the user credentials for the user you just made.

```
rake db:create db:migrate db:seed_fu
redis-cli flushall
thin start
```

### Setting up discourse
Go to your website and create an account. Then go back to the console and do the following:

```
bundle exec rails c  
u = User.first  
u.admin = true  
u.save
```