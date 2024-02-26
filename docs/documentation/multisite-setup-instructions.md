---
tags:
  - Installation
  - Multisite
---
# Multisite setup instructions

### This *only* applies to non-Docker configurations. If you are using the recommended Docker install for your instance of Docker, see [multi-site configuration with Docker](https://meta.discourse.org/t/multisite-configuration-with-docker/14084)

How do you setup multiple forums running on the same server in the same rails instance?  I'll tell you! In this example, I'll create a new site `dinotalk.example.com` operated by T Rex to talk about dinosaurs.

## Setup a new database for the new site:

Create a new PostgreSQL user (trex in this example):

    sudo su - postgres
    createuser --createdb --superuser --pwprompt -Upostgres trex

Create a new database:

    psql -c "create database dinotalk owner trex encoding 'UTF8' TEMPLATE template0"


## Setup multisite.yml

Create a new file in the application directory: `configs/multisite.yml`

Add an entry for your new database. Be sure to give it a unique db_id value! Here's an example:

    dinotalk:
      adapter: postgresql
      database: dinotalk
      username: trex
      password: smallarms
      host: /var/run/postgresql
      pool: 5
      timeout: 5000
      db_id: 2
      host_names:
        - dinotalk.example.com

If you're doing this in development mode, add an entry for `dinotalk.example.com` to your `hosts` file:

```
127.0.0.1 dinotalk.example.com
```

Now it's time to create the database objects.

## Migrate the database

Run database migrations against the new database (and all multisite databases):

    bundle exec rake multisite:migrate


## Start the server

In development mode, just do `bundle exec rails server` as usual. It will serve all sites. Then go to the host you set in your hosts file at the correct port (4000 if you're using the vagrant iamge).  e.g., `http://dinotalk.example.com:4000`


## Make an admin user

Every discourse forum needs at least one admin user, and one of them needs to be used as the sender of system messages.  It's a good idea to set a real person as the system user, instead of an unfriendly account called something like "admin" or "noreply". Create a new account on the site, and then grant it admin from the console.

Note that we use the RAILS_DB env variable to choose which site we're connected to in the console.

```
RAILS_DB=dinotalk bundle exec rails console
```

```ruby
u = User.find_by_username('trex')
u.admin = true
u.save
EmailToken.confirm( u.email_tokens.first.token )
SiteSetting.system_username = 'trex'
```

That's it!  Now you can have fun setting up your forum.  Here are some tasks you'll need to do:

* Create categories
* Write category descriptions
* Configure some site settings (`/admin/site_settings`):
  * Facebook, Twitter, etc. credentials (`facebook_app_id`, `twitter_consumer_key`, etc.)
  * Use your own logo (`logo_url`, `logo_small_url`)
  * Set your company name so the terms of service uses it (`company_full_name`, etc.)
  * Add your Google Analytics tracking code (`ga_tracking_code`)
  * Configure Amazon S3 or Imgur for uploads if you want to use them (`enable_s3_uploads`, etc.)

See the [Admin How To Guide][1] for more detailed instructions.

## Rails commands

You'll want to use RAILS_DB=dinotalk whenever you want to use one of the sites defined in multisite.yml.  For example, to open a rails console and connect to dinotalk:

    RAILS_DB=dinotalk bundle exec rails console

Without RAILS_DB, you'll be connecting to the database defined in database.yml.  When launching a server process, you don't need to set this variable.  The `rails server` command will handle all sites in the same process.


  [1]: https://github.com/discourse/discourse/wiki/The-Discourse-Admin-Quick-Start-Guide