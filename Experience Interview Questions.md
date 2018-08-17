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
### How we enter 5000 entry in Rails in very less time or Speeding Up Bulk Imports in Rails
https://blog.codeship.com/speeding-up-bulk-imports-in-rails/
```
Product.transaction do
    products = CSV.read("#{Rails.root}/tmp/products.csv")
    columns = [:sku, :name, :origin, :msrp_cents]
    Product.import columns, products, validate: false
  end
```
### find(:all) in rails 4 and 5 alternate
find_by is not deprecated, but the syntax is changing a bit. From find_by_name("Bob") to find_by(:name, "Bob")
Now take a look at find_by implementation:
```
def find_by
  where(*args).take
end
```
There is a difference between find and find_by in that find will return an error if not found, whereas find_by will return null.
Sometimes it is easier to read if you have a method like find_by email: "haha", as opposed to .where(email: some_params).first.

.find_by() is not only easier to read than where().first but is also faster (at least in Rails 4.2). If you look at the generated SQL query, where().first will have an additional ORDER BY xxx.id ASC. So unless the order is important to you, you should use find_by instead. PS: where().take doesn't add the ORDER BY part
```Model.find```

1- Parameter: ID of the object to find.

2- If found: It returns the object (One object only).

3- If not found: raises an ActiveRecord::RecordNotFound exception.
```
Model.find_by
```
1- Parameter: key/value

Example:

User.find_by name: 'John', email: 'john@doe.com'

2- If found: It returns the object.

3- If not found: returns nil.

Note: If you want it to raise ActiveRecord::RecordNotFound use find_by!
```
Model.where
```
1- Parameter: same as find_by

2- If found: It returns ActiveRecord::Relation containing one or more records matching the parameters.

3- If not found: It return an Empty ActiveRecord::Relation.

### what is serializer in rails
Active Model Serializers which be used to generate a JSON API in Rails.
http://railscasts.com/episodes/409-active-model-serializers
### Difference between Active Model, Active Record and Active Resource
ActiveModel: This component was created in Rails 3. They took all the model related parts that did not have a database requirement of Rails 2 ActiveRecord and moved it into ActiveModel. So ActiveModel includes things like validations. More information: http://www.rubyinside.com/rails-3-0s-activemodel-how-to-give-ruby-classes-some-activerecord-magic-2937.html

ActiveRecord: This is the component that associates a class to the database. This will give the class functionality such as methods that make it easy to pull records from the database (An example is the find method).

ActiveResource: Similar to ActiveRecord. However, instead of being backed by a database, an ActiveResource object is backed by another application through a web service API. More information: http://ofps.oreilly.com/titles/9780596521424/activeresource_id59243.html
### What is the Asset Pipeline?
https://guides.rubyonrails.org/asset_pipeline.html
The asset pipeline provides a framework to concatenate and minify or compress JavaScript and CSS assets. It also adds the ability to write these assets in other languages and pre-processors such as CoffeeScript, Sass and ERB. It allows assets in your application to be automatically combined with assets from other gems.
<b>1.1 Main Features</b>

The first feature of the pipeline is to concatenate assets, which can reduce the number of requests that a browser makes to render a web page. Web browsers are limited in the number of requests that they can make in parallel, so fewer requests can mean faster loading for your application.

Sprockets concatenates all JavaScript files into one master .js file and all CSS files into one master .css file. As you'll learn later in this guide, you can customize this strategy to group files any way you like. In production, Rails inserts an <b>SHA256 fingerprint</b> into each filename so that the file is cached by the web browser. You can invalidate the cache by altering this fingerprint, which happens automatically whenever you change the file contents.

The second feature of the asset pipeline is asset minification or compression. For CSS files, this is done by removing whitespace and comments. For JavaScript, more complex processes can be applied. You can choose from a set of built in options or specify your own.

The third feature of the asset pipeline is it allows coding assets via a higher-level language, with precompilation down to the actual assets. Supported languages include Sass for CSS, CoffeeScript for JavaScript, and ERB for both by default.
<b>1.2 What is Fingerprinting and Why Should I Care?</b>

Fingerprinting is a technique that makes the name of a file dependent on the contents of the file. When the file contents change, the filename is also changed. For content that is static or infrequently changed, this provides an easy way to tell whether two versions of a file are identical, even across different servers or deployment dates.

When a filename is unique and based on its content, HTTP headers can be set to encourage caches everywhere (whether at CDNs, at ISPs, in networking equipment, or in web browsers) to keep their own copy of the content. When the content is updated, the fingerprint will change. This will cause the remote clients to request a new copy of the content. This is generally known as cache busting.

The technique Sprockets uses for fingerprinting is to insert a hash of the content into the name, usually at the end. For example a CSS file global.css
```
global-908e25f4bf641868d8683022a5b62f54.css
```
### What exactly are the “components” of Rails 
Rails components are modules which are included by default in application.rb with require rails/all:

action mailer is a module for designing email service layers

action pack is a module for handling and responding to web requests (includes action_controller, action_dispatch)

action view is a module for handling view template lookup and rendering

active job is a module for declaring jobs and making them run on a variety of queueing backends

active model is non-database functionality extracted from Rails 2 Active Record (validates :name, presence: true)

active record connects classes to relational database tables (migrations, associations)

active support contains all Ruby extensions ([].blank?)

### What is the order of ActiveRecord callbacks and validations?
Rails 4

The most up-to-date version of this list can be found in the Rails 4 Guides.
Creating an object

    before_validation
    after_validation
    before_save
    around_save
    before_create
    around_create
    after_create
    after_save
    after_commit/after_rollback

Updating an object

    before_validation
    after_validation
    before_save
    around_save
    before_update
    around_update
    after_update
    after_save
    after_commit/after_rollback

Destroying an object

    before_destroy
    around_destroy
    after_destroy
    after_commit/after_rollback

### mysql vs postgres
https://www.differencebtw.com/difference-between-mysql-and-postgresql/

MySQL is a relational database management system RDBMS while PostgreSQL is an object relational database management system (ORDBMS).

MySQL is developed by Oracle and PostgreSQL is developed by the PostgreSQL Global Development Group.

MySQL uses MySQL partitioning technology for storing data on different nodes of database while PostgreSQL does not implement true partitioning.

Partitioning is done in MySQL for performing horizontal clustering while in PostgreSQL similar capability is done by table inheritance.

Performance of MySQL is faster as compare to PostgreSQL.

Sub-selects are available with PostgreSQL but not in MySQL.

Foreign key support is available in PostgreSQL but not in MySQL.

Triggers are available in PostgreSQL but not in MySQL.

Unions are available in PostgreSQL but not in MySQL.

Constraints are available in PostgreSQL but not in MySQL.

Vacuum (cleanup) are available in PostgreSQL but not in MySQL.

PostgreSQDL is closer to the ANSI SQL standard while MySQL is not fully compliant with ANSI SQL.

Database design is simpler in MySQL as compare to PostgreSQL.

## ORDBMS
An object-relational database (ORD), or object-relational database management system (ORDBMS), is a database management system (DBMS) similar to a relational database, but with an object-oriented database model: objects, classes and inheritance are directly supported in database schemas and in the query language.

### SQL query to check if a name begins with a vowel
select distinct city from station where city LIKE 'A%' or city LIKE 'E%' OR city LIKE 'I%' OR city LIKE 'O%' OR city LIKE 'U%' OR city LIKE 'a%' OR city LIKE 'e%' OR city LIKE 'i%' OR city LIKE 'o%' OR city LIKE 'u%';

### SQL query to check if a name begins and ends with a vowel
SELECT DISTINCT city
FROM   station
WHERE  city RLIKE '^[aeiouAEIOU].*[aeiouAEIOU]$'

## PUT vs PATCH
NOTE: When I first spent time reading about REST, idempotence was a confusing concept to try to get right. I still didn't get it quite right in my original answer, as further comments (and Jason Hoetger's answer) have shown. For a while, I have resisted updating this answer extensively, to avoid effectively plagiarizing Jason, but I'm editing it now because, well, I was asked to (in the comments).

After reading my answer, I suggest you also read Jason Hoetger's excellent answer to this question, and I will try to make my answer better without simply stealing from Jason.
Why is PUT idempotent?

As you noted in your RFC 2616 citation, PUT is considered idempotent. When you PUT a resource, these two assumptions are in play:
```
    You are referring to an entity, not to a collection.

    The entity you are supplying is complete (the entire entity).
```
Let's look at one of your examples.
```
{ "username": "skwee357", "email": "skwee357@domain.com" }
```
If you POST this document to /users, as you suggest, then you might get back an entity such as
```
## /users/1

{
    "username": "skwee357",
    "email": "skwee357@domain.com"
}
```
If you want to modify this entity later, you choose between PUT and PATCH. A PUT might look like this:
```
PUT /users/1
{
    "username": "skwee357",
    "email": "skwee357@gmail.com"       // new email address
}
```
You can accomplish the same using PATCH. That might look like this:
```
PATCH /users/1
{
    "email": "skwee357@gmail.com"       // new email address
}
```
You'll notice a difference right away between these two. The PUT included all of the parameters on this user, but PATCH only included the one that was being modified (email).

When using PUT, it is assumed that you are sending the complete entity, and that complete entity replaces any existing entity at that URI. In the above example, the PUT and PATCH accomplish the same goal: they both change this user's email address. But PUT handles it by replacing the entire entity, while PATCH only updates the fields that were supplied, leaving the others alone.
https://stackoverflow.com/questions/28459418/rest-api-put-vs-patch-with-real-life-examples

### Recovering stash entries that were cleared/dropped erroneously 

If you mistakenly drop or clear stash entries, they cannot be recovered through the normal safety mechanisms. However, you can try the following incantation to get a list of stash entries that are still in your repository, but not reachable any more:
```
git fsck --unreachable |
    grep commit | cut -d\  -f3 |
    xargs git log --merges --no-walk --grep=WIP
```
