---
tags:
  - Installation
  - Ubuntu
---
# Install Discourse on Ubuntu 12.10 (VM)

Most of step come from [Debian installation guide][1]
My notes as follow:

** updated using RVM
** updated RVM usage 

1.Prepare ubuntu
Clear install ubuntu server version without GUI
for clone vm of ubuntu 
fix missing eth0 issue with following command:

    sudo rm /etc/udev/rules.d/70-persistent-net.rules

2.update apt-get and install essential package

    sudo apt-get update
    sudo apt-get install build-essential git libpq-dev

3.Install postgresql/redis

    sudo apt-get install postgresql-9.1
    sudo apt-get install postgresql-contrib-9.1 
    sudo apt-get install redis-server

modify file 
/etc/postgresql/9.1/main/pg_hba.conf
add following line to create trust authentication

    host    all             all             127.0.0.1/32            trust  
    host    all             all             ::1/128                 trust  

4.Create a postgres DB user [my db user called dba]

    sudo adduser dba
    sudo su - postgres
    createuser -s dba

5.clone discourse 

       git clone git://github.com/discourse/discourse.git 

6\. Install RVM (ruby version manager) to package gems for discourse project
Install RVM    

    curl -L get.rvm.io | bash -s stable --auto
Create file ~/discourse/.rvmrc
add following line

    rvm 1.9.3@discoure
ps:1.9.3 is stade for MRI version 1.9.3
For ruby enterprise edition type "ree"
type

    rvm list known
for the full list
discoure is the gemset name you need to create the gemset at the next steps

After created .rvmrc file 

       cd ~/discourse

you will get some warning message you have to trust the .rvmrc file created in previous step

Install ruby and create gemset under rvm (your current directory have to be ~/dsicourse

    rvm install ruby-1.9.3
    rvm use 1.9.3
    rvm gemset create discoure 

8.Before install discourse
Before discourse can be install follow dependencies is required for nokogiri.

    sudo apt-get install libxslt-dev libxml2-dev

9.Install discourse

    cd discourse  
    bundle install  
Create db

    rake db:create db:migrate db:seed_fu

10.Prepare database.yml

    development:
      adapter: postgresql
      database: discourse_development
      username: dba
      password: dbapw
      host: localhost
      pool: 5
      timeout: 5000
      host_names:
        - "localhost"

11.Prepare redis.yml

    cp redis.yml.sample redis.yml

12.Start discourse
For thin server listen to port 3000
  
    thin start

Part B.
Set up reverse proxy with nginx
You would like to access your thin server with port 80 however it is suggested that you need a reverse proxy to better servering static content and thin server would focus on servering RoR respond.
I am not fully understand what is going on, my step just work for my server.
1.Install nginx

    apt-get install nginx

2.Config nginx
create a file /etc/nginx/nginx.conf
Here is an example:

    #user that run worker thread
    user www-data; 
    worker_processes 4;
    pid /var/run/nginx.pid;
    error_log logs/error.log;
    
    events {
    	worker_connections 768;
    	# multi_accept on;
    }
    
    http {
    
    	##
    	# Basic Settings
    	##
    
    	sendfile on;
    	tcp_nopush on;
    	tcp_nodelay on;
    	keepalive_timeout 65;
    	types_hash_max_size 2048;
    	# server_tokens off;
    
    	# server_names_hash_bucket_size 64;
    	# server_name_in_redirect off;
    
    	include /etc/nginx/mime.types;
    	default_type application/octet-stream;
    
    	##
    	# Logging Settings
    	##
    
    	access_log /var/log/nginx/access.log;
    	error_log /var/log/nginx/error.log;
    
    	##
    	# Gzip Settings
    	##
    
    	gzip on;
    	gzip_disable "msie6";
         
    	##
    	# Virtual Host Configs
    	##
    
    	include /etc/nginx/conf.d/*.conf;
    	include /etc/nginx/sites-enabled/*;
    
    log_format gzip '$remote_addr - $remote_user [$time_local]  '
                    '"$request" $status $bytes_sent '
                    '"$http_referer" "$http_user_agent" "$gzip_ratio"';
    
    
     server { # simple reverse-proxy
    #web server port
        listen       80;
    #If you linked a domain name replace ip address with domain name
        server_name  192.168.1.120;
        access_log   logs/nginx.access.log  gzip buffer=32k;
     
        # serve static files
        location ~ ^/(images|javascript|js|css|flash|media|static)/  {
    #If you linked a domain name replace ip address with domain name
          root    /var/www/virtual/192.168.1.120/htdocs;
          expires 30d;
        }
     
        # pass requests for dynamic content to rails/turbogears/zope, et al
        location / {
    #Thin server IP address and port
          proxy_pass      http://127.0.0.1:3000;
        }
      }
    }


3\. Test the config

    sudo  /etc/init.d/nginx start

If the nginx server config is correct the command return

    Starting nginx: nginx.
Otherwise please check the error msg

4.Test connection with browser
If you got bad gateway error please check if thin server started.

Part C.
People might want to use gmail or isp smtp for testing
Plese refer to this [post][2] for E-mail related config and trouble shooting

Install smtp server with postfix
To be continue.....


  [1]: http://meta.discourse.org/t/installing-discourse-on-debian/2349
  [2]: http://meta.discourse.org/t/help-action-mailer-issue/3447