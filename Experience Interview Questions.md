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

