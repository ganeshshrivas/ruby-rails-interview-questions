# Ruby basics
Ruby is a class-based object-oriented programming language. Meaning that every object is an instance of a class, and a class defines the state(variables) and behaviors(methods) of an object. An object is an entity with state and behavior, as defined by its class.

Ruby is a perfect Object Oriented Programming Language. The features of the object-oriented programming language include −

Data Encapsulation 

Data Abstraction 

Polymorphism 

Inheritance 



### What is a class? 
A class is the blueprint from which individual objects are created. In object-oriented terms, we say that your bicycle is an instance of the class of objects known as bicycles.

Take the example of any vehicle. It comprises wheels, horsepower, and fuel or gas tank 	capacity. These characteristics form the data members of the class Vehicle. You can differentiate one vehicle from the other with the help of these characteristics.
A vehicle can also have certain functions, such as halting, driving, and speeding. Even these functions form the data members of the class Vehicle. You can, therefore, define a class as a combination of characteristics and functions.

### What is the difference between a class and a module? 
A Module is a collection of methods and constants.

So yes, Math is a Ruby Module. Being collections of reusable code (also called libraries), Modules can have classes inside of them, whereas classes cannot have other classes inside.

technically, in Ruby, Class, and Module are just Classes, and Class inherits from Module, which is to say, every Ruby Class is a Ruby Module (but not conversely).

Modules are about providing methods that you can use across multiple classes - think about them as "libraries" (as you would see in a Rails app). Classes are about objects; modules are about functions.
```
╔═══════════════╦═══════════════════════════╦═════════════════════════════════╗
║               ║ class                     ║ module                          ║
╠═══════════════╬═══════════════════════════╬═════════════════════════════════╣
║ instantiation ║ can be instantiated       ║ can *not* be instantiated       ║
╟───────────────╫───────────────────────────╫─────────────────────────────────╢
║ usage         ║ object creation           ║ mixin facility. provide         ║
║               ║                           ║   a namespace.                  ║
╟───────────────╫───────────────────────────╫─────────────────────────────────╢
║ superclass    ║ module                    ║ object                          ║
╟───────────────╫───────────────────────────╫─────────────────────────────────╢
║ methods       ║ class methods and         ║ module methods and              ║
║               ║   instance methods        ║   instance methods              ║
╟───────────────╫───────────────────────────╫─────────────────────────────────╢
║ inheritance   ║ inherits behaviour and can║ No inheritance                  ║
║               ║   be base for inheritance ║                                 ║
╟───────────────╫───────────────────────────╫─────────────────────────────────╢
║ inclusion     ║ cannot be included        ║ can be included in classes and  ║
║               ║                           ║   modules by using the include  ║
║               ║                           ║   command (includes all         ║
║               ║                           ║   instance methods as instance  ║
║               ║                           ║   methods in a class/module)    ║
╟───────────────╫───────────────────────────╫─────────────────────────────────╢
║ extension     ║ can not extend with       ║ module can extend instance by   ║
║               ║   extend command          ║   using extend command (extends ║
║               ║   (only with inheritance) ║   given instance with singleton ║
║               ║                           ║   methods from module)          ║
╚═══════════════╩═══════════════════════════╩═════════════════════════════════╝
```
### What is an object? 
Everything in Ruby is an object. All objects have an identity; they can also hold state and manifest behaviour by responding to messages. These messages are normally dispatched through method calls. 

A string is an example of a Ruby object. Each string object has its own identity exposed through methods like object_id, == and class. It also has to store the value of the string and thus has state. Methods like split, upcase, downcase exposes the behavior of the object. 
```
Blocks, lambdas, Class - all of the them are objects. Every expression in Ruby evaluates to an object. These are all objects: 
Class, Module, Method, Object.new,  "a string", 42 ,lambda { puts "This is a block of code. An object!"} ,SomeUserDefinedClass.new 
```
### How would you declare and use a constructor in Ruby? 
The initialize method is a standard Ruby class method and works almost same way as constructor works in other object oriented programming languages. The initialize method is useful when you want to initialize some class variables at the time of object creation. This method may take a list of parameters and like any other ruby method it would be preceded by def keyword as shown below −
```
	class Box
   		def initialize(w,h)
      		@width, @height = w, h
   		end
	end
```
### How would you create getter and setter methods in Ruby? 
Getters and setters are just methods that are responsible for setting an instance variable (setter), and retrieving the value of an instance variable (getter). Instance variables are only directly accessible to the objects they belong to, which is why those objects need to explicitly provide a way for external code to access them, if that is desired. So written out completely, a getter and setter for the @velocity instance variable of Car would look like this:
```
class Car  
 def velocity    
   @velocity  
 end
 def velocity=(new_velocity)
   @velocity = new_velocity  
 end
end
```
By using the attr_reader & attr_writer methods given by ruby which automatically creates the setter & getter method for us
```
class Car  
  attr_reader :velocity  
  attr_writer :velocity
end
```
By using attr_accessor which provides both setter & getter method automatically. It is equivalent of using attr_reader & attr_writer
```
class Car  
  attr_accessor :velocity
end
```
### Describe the difference between class and instance variables? 
The main difference is the behavior concerning inheritance: class variables are shared between a class and all its subclasses, while class instance variables only belong to one specific class.

### What are the three levels of method access control for classes and what do they signify?
<b> Ruby Access Control Basics </b>

<b> Public Methods − </b> Public methods can be called by anyone. Methods are public by default except for initialize, which is always private.

<b> Private Methods − </b> Private methods cannot be accessed, or even viewed from outside the class. Only the class methods can access private members.

<b> Protected Methods − </b> A protected method can be invoked only by objects of the defining class and its subclasses. Access is kept within the family. 

### What does ‘self’ mean? 
The keyword self in Ruby gives you access to the current object – the object that is receiving the current message. 
To explain: a method call in Ruby is actually the sending of a message to a receiver. When you write obj.meth, you're sending the meth message to the object obj. obj will respond to meth if there is a method body defined for it. And inside that method body, self refers to obj.

### Explain how (almost) everything is an object in Ruby. 
Classes also are, as instances of `class` Class. Methods, operators and blocks aren't, but can be wrapped by objects (Proc). Simple assignment is not, and can't. Statements like ```while``` also aren't and can't. Comments obviously also fall in the latter group.

Most things that actually matter, i.e. that you would wish to manipulate, are objects (or can be wrapped in objects)

Practically everything in Ruby is an Object, with the exception of control structures. Whether or not under the covers a method, code block or operator is or isn't an Object, they are represented as Objects and can be thought of as such.

Take a code block for example:
```
def what_is(&block)
  puts block.class
  puts block.is_a? Object
end

> what_is {}
Proc
true
=> nil
Or for a Method:
class A
  def i_am_method
    "Call me sometime..."
  end
end

> m = A.new.method(:i_am_method)
> m.class
Method
> m.is_a? Object
true
> m.call
"Call me sometime..."
And operators (like +, -, [], <<) are implemented as methods:
class String
  def +
    "I'm just a method!"
  end
end
```
For people coming into programming for the first time, what this means in a practical sense is that all the rules that you can apply to one kind of Object can be extended to others. You can think of a String, Array, Class, File or any Class that you define as behaving in much the same way. This is one of the reasons why Ruby is easier to pick up and work with than some other languages.

### Explain what singleton methods are. What is Eigenclass in Ruby? 
Methods that are defined for only a single object rather than a class of objects. To define a singleton method sum on an object Point, we’d write:
```
def Point.sum
  # Method body goes here
end
```
The class methods of a class are nothing more than singleton methods on the Class instance that represents that class.

The singleton methods of an object are not defined by the class of that object. But they are methods and they must be associated with a class of some sort. 

The singleton methods of an object are instance methods of the anonymous eigenclass associated with that object. “Eigen” is a German word meaning (roughly) “self,” “own,” “particular to,” or “characteristic of.” The eigenclass is also called the singleton class or (less commonly) the metaclass. The term “eigenclass” is not uniformly accepted within the Ruby community, but it is the term we’ll use here.

<b>eigenclass</b>
class << self is more than just a way of declaring class methods (though it can be used that way). Probably you've seen some usage like:
```
class Foo
  class << self
    def a
      print "I could also have been defined as def Foo.a."
    end
  end
end
```
This works, and is equivalent to def Foo.a, but the way it works is a little subtle. The secret is that self, in that context, refers to the object Foo, whose class is a unique, anonymous subclass of Class. This subclass is called Foo's eigenclass. So def a creates a new method called a in Foo's eigenclass, accessible by the normal method call syntax: Foo.a.
Now let's look at a different example:
```
str = "abc"
other_str = "def"

class << str
  def frob
    return self + "d"
  end
end

print str.frob # => "abcd"
print other_str.frob # => raises an exception, 'frob' is not defined on other_str
```
This example is the same as the last one, though it may be hard to tell at first. frob is defined, not on the String class, but on the eigenclass of str, a unique anonymous subclass of String. So str has a frob method, but instances of String in general do not. We could also have overridden methods of String (very useful in certain tricky testing scenarios).


### Describe Ruby method lookup path. 
``` Include, prepand, super ```
https://gist.github.com/damien-roche/351bf4e7991449714533
### Describe available Ruby callbacks. How can we use them in practice? 
### What is the difference between Proc and lambda? 
lambdas check the number of arguments passed, while procs do not
return in a proc means to return from the proc and the enclosing method; return in a lambda means to return from just the lambda
procs can only use return when the proc is defined inside a method and the proc is called before the method call returns
http://rubyblog.pro/2016/11/lambda-and-proc-difference

1. Lambda strictly checks params number, Proc doesn't
```
l = ->(a, b) { puts "#{a} and #{b}" }
p = Proc.new { |a, b| puts "#{a} and #{b}" }
```
Here we have lambda and Proc which accepts two arguments each. Let's try to call lambda with one param:
l.call("foo") # => wrong number of arguments (1 for 2)
Lambda throws an error, because we passed just one argument instead of two.
```
Now Proc:
p.call("foo") # => foo and
```
Proc worked. First param it set to "foo", and another to nil. By this example we see that lambdas require all params to be passed. Procs are more flexible with arguments. If we didn't pass some arguments, it will set them to nil.
One thing to know: Procs and lambdas behave as methods and accepts default values for arguments:
```
l = ->(word = "default") { puts word }
l.call # => default

p = proc { |word = "default"| puts word }
p.call # => default
```
If we defined default values for arguments, we can call lambda as a Proc and don't pass any values at all. In this case default values will be used.

2. return from lambda just returns value. Explicit return from Proc returns value from current scope (for example method) in which it was defined.
We discussed such example with lambda:
```
def do_math
  sum = ->(a, b) { return a + b }
  result = sum.call(2, 2)
  "Result of 2+2 is #{result}"
end

do_math # => Result of 2+2 is 4
```
Even after call sum.call(2, 2), code inside do_math continued to execute and we've seen string with a result. So explicit return from lambda worked as any other return form regular method.
Explicit return from Proc works in different way:
```
def foo
  p = Proc.new { return "Returned value from Proc" }
  p.call
  "Return from foo"
end

puts foo # => Returned value from Proc
```
As soon as we called p.call, Proc took control over method foo and after explicit return returned its value and interrupted execution of foo method. We didn't get "Return from foo" string. Because foo returned Proc's result of execution.
If we want Proc's return to behave as lambda's, we should remove explicit return from Proc:
```
def foo
  p = Proc.new { "Returned value from Proc" }
  p.call
  "Return from foo"
end

puts foo # => Return from foo
```
In this case after p.call call, method continued to execute and returned last string from foo method.

### What is decoraters?
In object-oriented programming, the decorator pattern is a design pattern that allows behavior to be added to an individual object, dynamically, without affecting the behavior of other objects from the same class.

https://codebrahma.com/ruby-decorators/
```
class Car
  def top_speed
    100 
  end 
end 

class CarWithNitro < Car 
  def top_speed
    super + 30 
  end 
end
 
class CarWithBoost < Car 
  def top_speed 
    super + 50 
  end 
end 
```
The drawback of this pattern is * The subclasses are tightly coupled to the super class. Suppose if the we change the name of the method in the super class we need to make these changes to our subclasses as well. * No way of adding any packs to a car dynamically. If in a certain scenario we need a car with two nitro packs and three boost packs it’s not easy with this architecture.
#### Def
The decorator pattern allows you to attach additional responsibilities to an object dynamically. Decorators provide a flexible alternative to subclassing for extending functionality.

A decorator is a wrapper object on the component class.
Has the same interface as the component it is decorating so that it’s presence is transparent to the clients
Delegates requests to components
Performs additional actions before or after delegating


<b> Applying decorator pattern to our problem step by step </b>

    The component class that we would want to add new features to or “Decorate” is “Car”
    The decorators would be in this case “Nitro” and “Boost”

Now that we have identified what decorators we need let’s write it
```
class Nitro
  # Wrapping the component class, Car object in this case 
  def initialize(component)
    @component = component
  end 
    
  # maintain the same public interface as component
  def top_speed 
    # after delegation modify the value 
    @component.top_speed + 30
  end
end
  
class Boost
  def initialize(component)
    @component = component
  end
   
  def top_speed
    @component.top_speed + 50
  end
end 
```
Now we can start using our decorators to add new packs to a car object.
```
Nitro.new(Car.new).top_speed #130 

Nitro.new(Nitro.new(Car.new)).top_speed #160 

Boost.new(Nitro.new(Car.new)).top_speed #180
```
That’s it, our shiny new power packed cars are ready to be driven
### What is block?
https://www.tutorialspoint.com/ruby/ruby_blocks.htm
A block consists of chunks of code.
You assign a name to a block.
The code in the block is always enclosed within braces ({}).
A block is always invoked from a function with the same name as that of the block. This means that if you have a block with the name test, then you use the function test to invoke this block.
You invoke a block by using the yield statement.
```
def test
   puts "You are in the method"
   yield
   puts "You are again back to the method"
   yield
end
test {puts "You are in the block"}
```
This will produce the following result −
``
You are in the method
You are in the block
You are again back to the method
You are in the block ``
Blocks and Methods
`
def test(&block)
   block.call
end
test { puts "Hello World!"}

This will produce the following result −

Hello World!
`
### When to use lambda?
We can use lambda where we need to strictly check the passing parameter before execution. for ex
In Rails a named scope is essentially a lambda if I'm not mistaken. 
You can use them to make case statements which evaluate expressions:
`
case { animal: "frog" }
when ->(val) { val[:animal] == "dog" }
  puts "bark"
when ->(val) { val[:animal] == "frog" }
  puts "croak"
end`

Kind of a pointless example here but I think it's a potentially useful thing.
### What is MetaProgramming?
Metaprogramming is the writing of computer programs with the ability to treat programs as their data. It means that a program could be designed to read, generate, analyze, or transform other programs and even modify itself while running.

We’ll specifically look at how we can read and analyze our code in Ruby, how we can call methods (or send messages) dynamically, and how we can generate new methods during the runtime of our program.

http://rubylearning.com/blog/2010/11/23/dont-know-metaprogramming-in-ruby/

### What is a decorator?
The decorator pattern is a design pattern that allows behavior to be added to an individual object without affecting the behavior of other objects from the same class.

### Difference between 'each' and 'map'?
each returns the original object. It's used to run an operation using each element of an array without collecting any of the results. For example, if you want to print a list of numbers, you might do something like this:
```
arr = [1, 2, 3, 4]
arr.each { |n| puts n }
```
Now, that puts method above actually returns nil. Some people don't know that, but it doesn't matter much anyway; there's no real reason to collect that value (if you wanted to convert arr to strings, you should be using arr.map(&:to_s) or arr.map { |n| n.to_s }.

map returns the results of the block you pass to it. It's a great way to run an operation on each element in an array and retrieve the results. If you wanted to multiple every element of an array by 2, this is the natural choice. As a bonus, you can modify the original object using map!. For example:
```
arr = [1, 2, 3, 4]
arr.map! { |n| n * 2}
# => [2, 4, 6, 8]
```
### Is “find_all” and “select” the same thing?
#find_all and #select are very similar; the difference is very subtle. In most of the cases, they are equivalent. It depends on the class implementing it.

Enumerable#find_all and Enumerable#select run on the same code.

The same happens for Array and Range, as they use Enumerable implementation.

In the case of Hash, #select is redefined to return a Hash instead of an Array, but #find_all is inherited from Enumerable
```
a = [1, 2, 3, 4, 5, 6]
h = {a: 1, b: 2, c: 3, d: 4, e: 5, f: 6}

a.select{|x| x.even?}       # => [2, 4, 6]
a.find_all{|x| x.even?}     # => [2, 4, 6]

h.select{|k,v| v.even?}     # => {:b=>2, :d=>4, :f=>6}
h.find_all{|k,v| v.even?}   # => [[:b, 2], [:d, 4], [:f, 6]]
```
### Single qoute('') vs Double qoute ("")
single-quoted strings don't process ASCII escape codes and they don't do string interpolation.
```
name = 'Joe'
greeting = 'Hello, #{name}' # this won't produce "Hello, Joe" 
```
except the interpolation, another difference is that 'escape sequence' does not work in single quote
```
puts 'a\nb' # just print a\nb 
puts "a\nb" # print a, then b at newline 
```
### What’s the bang operator do in Ruby? Is it different from the bang that is at the end of a method?
The bang operator is a method that is used to return boolean values. 
In Ruby everything except nil and false are considered truthy values. Let’s consider the following:
```
2.3.0 :028 > arr = [1,2,3,4,5]
 => [1, 2, 3, 4, 5] 
2.3.0 :029 > !arr
 => false 
2.3.0 :030 > !!arr
 => true 
 ```
 We can see that !arr returns false.  We also see that a !! returns the truthiness or falseness of the original piece of data. The bang operator can also be called on a variable like any other method call, arr.! . This would return the same value as !arr . So, how does .! differ from methods like .map! , .uniq! , .filter!...etc
 ```
 2.3.0 :037 > arr = [1,2,3,4,5,6,6,7,7,8]
 => [1, 2, 3, 4, 5, 6, 6, 7, 7, 8] 
2.3.0 :038 > arr.uniq
 => [1, 2, 3, 4, 5, 6, 7, 8] 
2.3.0 :039 > arr
 => [1, 2, 3, 4, 5, 6, 6, 7, 7, 8] 
2.3.0 :040 > new_arr = arr.uniq
 => [1, 2, 3, 4, 5, 6, 7, 8] 
2.3.0 :041 > new_arr
 => [1, 2, 3, 4, 5, 6, 7, 8] 
2.3.0 :042 > arr
 => [1, 2, 3, 4, 5, 6, 6, 7, 7, 8] 
2.3.0 :043 > arr.uniq!
 => [1, 2, 3, 4, 5, 6, 7, 8] 
2.3.0 :044 > arr
 => [1, 2, 3, 4, 5, 6, 7, 8] 
2.3.0 :045 > arr==new_arr
 => true 
 ```
Looking at the example above, when we call .uniq on an arr it returns a new array with all the duplicate values removed. If we check what is saved inside arr we see that the original state of the variable is preserved. Once we add an exclamation point to the end of the method call, the original data stored within arr is mutated. This second method call is destructive.

The main different between the .! method call and any method that ends with an exclamation point is that .! coerces data to return a boolean value that is opposite to the truthiness or falsness that Ruby assigns to that data type.

### instance variable vs Class variable?
Instance variable on a class:
```
class Parent
  @things = []
  def self.things
    @things
  end
  def things
    self.class.things
  end
end

class Child < Parent
  @things = []
end

Parent.things << :car
Child.things  << :doll
mom = Parent.new
dad = Parent.new

p Parent.things #=> [:car]
p Child.things  #=> [:doll]
p mom.things    #=> [:car]
p dad.things    #=> [:car]
```
With an instance variable on a class (not on an instance of that class) you can store something common to that class without having sub-classes automatically also get them (and vice-versa).

Class variable:
```
class Parent
  @@things = []
  def self.things
    @@things
  end
  def things
    @@things
  end
end

class Child < Parent
end

Parent.things << :car
Child.things  << :doll

p Parent.things #=> [:car,:doll]
p Child.things  #=> [:car,:doll]

mom = Parent.new
dad = Parent.new
son1 = Child.new
son2 = Child.new
daughter = Child.new

[ mom, dad, son1, son2, daughter ].each{ |person| p person.things }
#=> [:car, :doll]
#=> [:car, :doll]
#=> [:car, :doll]
#=> [:car, :doll]
#=> [:car, :doll]
```
With class variables, you have the convenience of not having to write self.class from an instance object, and (when desirable) you also get automatic sharing throughout the class hierarchy.

### Is ruby pure OOPS?
What makes a language object-oriented in the first place are naturally objects. Everything is an object in ruby. The whole language is built on the concept of objects and data. Different objects can "communicate" between each other, you can encapsulate data, etc.
### extend Vs include?
Include is for adding methods to an instance of a class and extend is for adding class methods. Let’s take a look at a small example.
```
module Foo
  def foo
    puts 'heyyyyoooo!'
  end
end

class Bar
  include Foo
end

Bar.new.foo # heyyyyoooo!
Bar.foo # NoMethodError: undefined method ‘foo’ for Bar:Class

class Baz
  extend Foo
end

Baz.foo # heyyyyoooo!
Baz.new.foo # NoMethodError: undefined method ‘foo’ for #<Baz:0x1e708>
```
As you can see, include makes the foo method available to an instance of a class and extend makes the foo method available to the class itself.
### Difference between multiple and multi level inheritence in ruby?
Multiple Inheritance :

Single class inherites multiple classes i.e. there is only one child or derived class and multiple parent or base classes.
![alt text](https://qph.ec.quoracdn.net/main-qimg-b305229f7800e84fe16bd8167ef91704)

Multi level Inheritance :

When a class inherits a class and which also inherit another class i.e. a child class inherit a class which also inherit another base class so these class also base class of which inherit its base class.
![alt text](https://qph.ec.quoracdn.net/main-qimg-d23af5ac393cb13d20ea77a374488854)

### How to implement multiple inheritance?
Ruby does not support multiple inheritance.
<b>How can you achieve the same effect as multiple inheritance using Ruby? What is mixin?</b>
Ruby does not have multiple inheritance. Ruby has something similar called mixins which can be implemented using Modules.

Mixins are not multiple inheritance, but instead mostly eliminate the need for it.

To answer your question, when you include two modules in a class and both of them has the method with same name (in your case, method a), in that case, a method from the 2nd (the last one) Module will be called.
```
module A
  def a1
    puts "I am defined in A"
  end

  def a2
  end
end

module B
  def a1
    puts "I am defined in B"
  end

  def b2
  end
end

class Sample
  include A
  include B

  def s1
  end
end

samp = Sample.new
puts samp.a1
I am defined in B
```
It becomes more clear when you inspect the ancestors of the Sample class. 
```
puts Sample.ancestors.inspect
# [Sample, B, A, Object, Kernel, BasicObject]
```
See the order here. When a method is called, Ruby looks for the method definition first in Sample class itself, but doesn't find it. Then, it looks for the a method in B and it finds it and calls it.

### What's the difference between a string and a symbol in Ruby?
In Ruby string are mutable, it means that you can change them: 'foo' +  'bar' will give a concatenated string. You can perceive symbols as immutable strings, it means that you cannot change a symbol: :foo + :bar will give you an error. Most importantly, the same symbols hold reference to the same object:
```
irb(main):007:0> :test.object_id
=> 83618
irb(main):008:0> :test.object_id
=> 83618
irb(main):009:0> :test.object_id
=> 83618

irb(main):010:0> "test".object_id
=> -605770378
irb(main):011:0> "test".object_id
=> -605779298
irb(main):012:0> "test".object_id
=> -605784948
```
This means that using symbols can potentially save a good bit of memory depending on the application. It is also faster to compare symbols for equality since they are the same object, comparing identical strings is much slower since the string values need to be compared instead of just the object ids.

As far as when to use which, I usually use strings for almost everything except things like hash keys where I really want a unique identifier, not a string.

### Write a program to print this pattern N = 7. So value of N is dynamic. If N is 6 or 5 then it should scale accordingly

7

7 6

7 6 5

7 6 5 4

7 6 5 4 3

7 6 5 4 3 2

7 6 5 4 3 2 1

7 6 5 4 3 2

7 6 5 4 3

7 6 5 4

7 6 5

7 6

7
```
puts "Please enter a number"
num = gets.chomp.to_i
puts "Here is scal programe"
tmp = []
i = num
while(i>0) do
	tmp << i
	puts tmp.join(" ")
	i-=1
	if(i==0)
		(0..num).each do |val|
			tmp.delete(val)
			puts tmp.join(" ")
		end
	end
end
```
### Preload, Eagerload, Includes and Joins
# Preload

Preload loads the association data in a separate query.
```
User.preload(:posts).to_a

# =>
SELECT "users".* FROM "users"
SELECT "posts".* FROM "posts"  WHERE "posts"."user_id" IN (1)
```
This is how includes loads data in the default case.

Since preload always generates two sql we can’t use posts table in where condition. Following query will result in an error.
```
User.preload(:posts).where("posts.desc='ruby is awesome'")

# =>
SQLite3::SQLException: no such column: posts.desc:
SELECT "users".* FROM "users"  WHERE (posts.desc='ruby is awesome')
```
With preload where clauses can be applied.
```
User.preload(:posts).where("users.name='Neeraj'")

# =>
SELECT "users".* FROM "users"  WHERE (users.name='Neeraj')
SELECT "posts".* FROM "posts"  WHERE "posts"."user_id" IN (3)
```
# Includes

Includes loads the association data in a separate query just like preload.

However it is smarter than preload. Above we saw that preload failed for query User.preload(:posts).where("posts.desc='ruby is awesome'"). Let’s try same with includes.
```
User.includes(:posts).where('posts.desc = "ruby is awesome"').to_a

# =>
SELECT "users"."id" AS t0_r0, "users"."name" AS t0_r1, "posts"."id" AS t1_r0,
       "posts"."title" AS t1_r1,
       "posts"."user_id" AS t1_r2, "posts"."desc" AS t1_r3
FROM "users" LEFT OUTER JOIN "posts" ON "posts"."user_id" = "users"."id"
WHERE (posts.desc = "ruby is awesome")
```
As you can see includes switches from using two separate queries to creating a single LEFT OUTER JOIN to get the data. And it also applied the supplied condition.

So includes changes from two queries to a single query in some cases. By default for a simple case it will use two queries. 
# references
Let’s say that for some reason you want to force a simple includes case to use a single query instead of two. Use references to achieve that.
```
User.includes(:posts).references(:posts).to_a

# =>
SELECT "users"."id" AS t0_r0, "users"."name" AS t0_r1, "posts"."id" AS t1_r0,
       "posts"."title" AS t1_r1,
       "posts"."user_id" AS t1_r2, "posts"."desc" AS t1_r3
FROM "users" LEFT OUTER JOIN "posts" ON "posts"."user_id" = "users"."id"
```
In the above case a single query was done.
# Eager load

eager loading loads all association in a single query using LEFT OUTER JOIN.
```
User.eager_load(:posts).to_a

# =>
SELECT "users"."id" AS t0_r0, "users"."name" AS t0_r1, "posts"."id" AS t1_r0,
       "posts"."title" AS t1_r1, "posts"."user_id" AS t1_r2, "posts"."desc" AS t1_r3
FROM "users" LEFT OUTER JOIN "posts" ON "posts"."user_id" = "users"."id"
```
This is exactly what includes does when it is forced to make a single query when where or order clause is using an attribute from posts table.
# Joins

Joins brings association data using inner join.
```
User.joins(:posts)

# =>
SELECT "users".* FROM "users" INNER JOIN "posts" ON "posts"."user_id" = "users"."id"
```
In the above case no posts data is selected. Above query can also produce duplicate result.

### Difference between as_json and to_json method in Ruby
as_json returns a hash representation of your model object, while to_json returns a json object.

Note: Internally, when you call the to_json method on your model/serializer, as_json is first called.


to_json returns String. as_json returns Hash with String keys.
```
> { :name => "Konata Izumi", 'age' => 16, 1 => 2 }.to_json
"{\"name\":\"Konata Izumi\",\"age\":16,\"1\":2}"

> { :name => "Konata Izumi", 'age' => 16, 1 => 2 }.as_json
{"name"=>"Konata Izumi", "age"=>16, "1"=>2}
```
### git rebase vs merge
https://www.atlassian.com/git/tutorials/merging-vs-rebasing
 
### git pull vs fetch
git fetch really only downloads new data from a remote repository - but it doesn't integrate any of this new data into your working files. Fetch is great for getting a fresh view on all the things that happened in a remote repository.
Due to it's "harmless" nature, you can rest assured: fetch will never manipulate, destroy, or screw up anything. This means you can never fetch often enough.

git pull, in contrast, is used with a different goal in mind: to update your current HEAD branch with the latest changes from the remote server. This means that pull not only downloads new data; it also directly integrates it into your current working copy files.
### use of manifest.yml file (assets precompile)
rails compare the file entry with define js/css required files. If mismatch then recompile the css/js

### Rails Caching (content vs. page/action/etc)
Page caching: the first time a controller action is requested a copy of the entire generated page is written to a static .html file so that next time someone requests the same action it can be served by the web server without hitting your Rails application at all. This is super fast but has limitations e.g. a request for a cached page doesn't go via your application so you can't use filters to do authentication and restrict page access.

Action caching: the request always goes from the web server to your Rails application so that your filters run but if the request passes the filters and the action is cached then the cached copy is servered instead of actually running the code in your controller action. Limitation: the same cached content is served to all users so the page can't have any personalised data (such as showing the logged in username in the header)

Fragment caching: the controller action's code runs but within the view individual blocks of the page can be cached. e.g. if we have something in the sidebar that is computationally intensive.
### Russian Doll Caching
You may want to nest cached fragments inside other cached fragments. This is called Russian doll caching.
https://guides.rubyonrails.org/caching_with_rails.html#russian-doll-caching
### In AWS Why we need Elastic Ip?
To use same ip address on newest version of ec2 instance if we upgrade the old ec2 instance to new ec2 instance.
### controller concern vs model concerns
http://vaidehijoshi.github.io/blog/2015/10/13/stop-worrying-and-start-being-concerned-activesupport-concerns/
### AWS RDS?
### Setting up Bundler in Rails 2.3

Insert the following code at the bottom of config/boot.rb, right above the line `Rails.boot!`
```
class Rails::Boot
  def run
    load_initializer

    Rails::Initializer.class_eval do
      def load_gems
        @bundler_loaded ||= Bundler.require :default, Rails.env
      end
    end

    Rails::Initializer.run(:set_load_path)
  end
end
```
Create a new file, config/preinitializer.rb, and insert the following. That is config NOT config/initializers.
```
begin
  require 'rubygems'
  require 'bundler'
rescue LoadError
  raise "Could not load the bundler gem. Install it with `gem install bundler`."
end

if Gem::Version.new(Bundler::VERSION) <= Gem::Version.new("0.9.24")
  raise RuntimeError, "Your bundler version is too old for Rails 2.3.\n" +
   "Run `gem install bundler` to upgrade."
end

begin
  # Set up load paths for all bundled gems
  ENV["BUNDLE_GEMFILE"] = File.expand_path("../../Gemfile", __FILE__)
  Bundler.setup
rescue Bundler::GemNotFound
  raise RuntimeError, "Bundler couldn't find some gems.\n" +
    "Did you run `bundle install`?"
end
```
Get all config.gem declarations from your application, and place them into the Gemfile. If you have declarations in development.rb, for instance, place them in a named group. Make sure to include Rails itself and at least one source
```
source :gemcutter
gem 'rails', '~> 2.3.5'
gem 'sqlite3-ruby', :require => 'sqlite3'

# bundler requires these gems in all environments
# gem 'nokogiri', '1.4.2'
# gem 'geokit'

group :development do
  # bundler requires these gems in development
  # gem 'rails-footnotes'
end

group :test do
  # bundler requires these gems while running tests
  # gem 'rspec'
  # gem 'faker'
end

Learn More: Groups
Once you have everything set up, you can use script/console, script/server, and other Rake tasks as usual. From this point on, you can follow the instructions in the Rails 3 guide

$ rake db:migrate
```
### after_create vs after_save vs after_commit, around_*
after_create

Is called after Base.save on new objects that haven‘t been saved yet (no record exists)

after_save

Is called after Base.save (regardless of whether it‘s a create or update save)

after_commit

Is called after the database transaction is completed.

around_* 

callbacks are invoked before the action, then when you want to invoke the action itself, you yield to it, then continue execution. That's why it's called around
The order goes like this: before, around, after.
