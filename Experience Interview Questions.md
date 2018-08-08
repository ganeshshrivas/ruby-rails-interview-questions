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
