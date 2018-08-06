# Ruby On Rails Interview Questions For Experience Developer more or equal to 4 year
### diff map and pluck
### how many engine available in mysql.
MyISAM(non transactional), InnoDb(Transactional)
### transaction and non transaction db?
### What app server we use to deploy the app?
passenger,unicorn, puma
### Difference between Application server and Web Server 
http://rorguide.blogspot.com/2011/07/difference-between-application-server.html
apache, nginx, IIS are web servers

mongrel, webrick, phusion passenger are app servers

<b>App server</b> is something which works with particular programming language and parses and executes the code
since mongrel and webrick can only work with rails, so they are app servers

<b>Web servers</b> are servers which can take the request from the browser.
Web servers normally works on port 80 though we can change the port in configuration
since mongrel and webrick can take that request directly, so they can be thought of as web servers but web servers do have a lot of other functionality like request pipeline, load balancing etc.
App servers lack these functionalities.

About Mongrel server:
mongrel work as web as well as app server if you are talking about dev environment
but in production, mongrel alone can not work it will be too slow
so we need a web server in front of mongrel
