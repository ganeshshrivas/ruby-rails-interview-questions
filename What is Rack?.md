### What is Rack?
http://blog.gauravchande.com/what-is-rack-in-ruby-rails

Lets start with a basic browser-server interaction. Say you’re developing an app with Rails (or any other Ruby web framework) and it has a page located at ‘http://localhost:3000/users’ that displays all users. The ‘/users’ request is going to go to your Rails server asking to show all users.

Behind the scenes, this HTTP request that the browser sends looks like this:
```
// Request by the browser

GET /users HTTP/1.1

Host: localhost

Connection: close

```
And, the response sent by the server looks like:
```
// Response by the server


HTTP/1.1 200 OK

Content-Length: 25

Content-Type: text/html

<html>

...

</html>
```
Now, say you’re a web server. You have this Rails app loaded in you. And some browser came to you with that request having path ‘/users’. As a server you understand this HTTP request. But you don’t know what to do with it. You have to give it to your Rails app, because it knows very well what to do with such a request.

There is a problem though. Your Rails app does not understand browser requests directly. You need to translate it in a way that he can make sense of it, work with it and then give you a response which you yourself can understand. But the Rails app is kind of a nut-job and doesn’t co-operate easily. So you take the app to a counsellor, to come up with a system.

The counsellor’s name is ‘Rack’. He says, ‘Look Rails app, the server is ready to work together. He’s going to translate the HTTP request in a format that I’ll tell him to. This format will be easy for you to understand. In return, you have to give him a response that he can easily work with. I’ll tell you how your response should look like. Okay?’

Rails app agrees to co-operate after Rack talks some sense into it.

This is how Rack comes into the picture. It is basically just a set of guidelines for how a server and a Rails app (or any other Ruby web app) should talk to each other. So that there is peace in the world with simple, common rules of server - app communication.

Lets actually see what Rack is asking both server and Ruby app to do, to work peacefully.

First the server. Because of what Rack has specified, server will convert the HTTP request (from the example above) to a simple Ruby Hash, as shown below:
```
// Server to Rails app

env = {

  'REQUEST_METHOD' => 'GET',
  
  'PATH_INFO' => '/users',
  
  'HTTP_VERSION' => '1.1',
  
  'HTTP_HOST' => 'localhost',
  
  ...
  
  ...
}
```
This env variable is then sent to the app. The app does all its work based on the information it got from this variable and returns a response to the server. This response is made exactly how Rack specified, so that the server can understand it.

What the app gives back to the server is a simple Array. This array has exactly 3 elements in it. First is the HTTP status code of the response, second is a Hash of HTTP headers and the third element is a body object (which must respond to each).
```
// Rails app to server

[

  200,
  
  {
  
    'Content-Length' => '25',
    
    'Content-Type' => 'text/html'
    
  },
  
  [
  
    '<html>',
    
    '...',
    
    '</html>'
    
  ]
  
]

```
The server can finally take this array and convert it into a valid HTTP response and send it to the browser (client).

So ‘Rack’ is basically a specification of these two things: what the server should send to the app and what the app should return to the server. That’s it.

Now there are certain rules about what things the Ruby app should compose of, to be able to work with that env variable from the server. In its most basic sense this is what the Ruby app should contain:
```
class App

  def call(env)
  
    [
    
      200,
      
      { 'Content-Length' => 25, 'Content-Type' => 'text/html' },
      
      [ "<html>", "...", "</html>" ]
      
    ]
    
  end
  
end
```
The app should implement a method named call which accepts a parameter env. And this method should return the resultant Array we talked about. (Of course your app would dynamically generate the result Array based on what request it got, but this gives you the idea.)

Any app that confirms to this rule is a ‘Rack application’. If you open Rails up, you’ll definitely find that this method has been implemented in it somewhere. Hence, Rails itself is a Rack application. That is why Rails works on most modern ‘rack-based’ web servers (like Unicorn, Puma, Passenger, Thin, etc.).

This post is getting long for ‘Rack Middleware’ part. If you think this post helped you, just hit me an email if you want me to write about Rack middleware. I’ll write a separate post for it then. Although it’s a really simple concept to understand, once you know what Rack is. railscasts.com has a very good free episode on it here. I suggest you to go through that for info on Rack Middleware.

http://railscasts.com/episodes/151-rack-middleware
