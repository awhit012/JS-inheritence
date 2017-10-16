# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) JS Prototypal Inheritance

### Sample Teach 
*by Alex White*

## Objective:

By the end of the lesson, students will be able to...

	- Demonstrate a use case that explains prototypal inheritance
	- Demonstrate what kind of flexibility prototypal inheritance gives
	programmers

## Opening:

### We are going to talk about JS Prototypal inheritence 
 - why we need to know about it
 - go over some vocab
 - see a demo of it in Ruby and JS using a real world example
 - discuss what the differences are
 - review


## Why - do we need to know?
- We make use of inheritance just by using JS and should know what is going on

## Why - is it even a thing?
- code reuse 
- code organization

## Disclaimer:
- It isn't common to need to implement inheritence in small to medium sized projects. Use only when it REALLY makes sense. Forcing data into inheritence patterns will create a bad situation.

## Vocab:
**prototype**: an object that is used as a template to make other objects.
**inheritance**: giving the stuff of the parents to the kids
**OOP**: a programming pattern that models objects with attributes and functionality.
**Class**: a platonic 'essence' of something
**Constructor**: A function that is used as a prototype object. It creates new objects like itself.

## Demo 1: 
Creating an instance of a class/prototype
ruby code:
```ruby
class User
	attr_reader :email
	def initialize(email)
		@email = email
	end

	def welcome
	  # functionality to send a welcome email:
	  p 'sending welcome email to ' + self.email
	end
end

me = User.new("me@me.com")
me.email
me.welcome
```
js code:
```js
function User(email) {
  this.email = email;
};

User.prototype.welcome = function() {
	//functionality to send a welcome email:
	console.log('sending welcome email to ' + this.email);
};

me = new User("me@me.com");
me.email
me.welcome();
```
## Demo 2: Inheriting one object from another
```ruby
ruby code:
class User
	def initialize(email)
		@email = email
	end

	def welcome
	  # functionality to send a welcome email:
	  p 'sending welcome email to ' + self.email
	end
end

class Admin < User
	def email_all_users
		# functionality to email all users
		p "emailing all users"
	end
end

me = Admin.new("me@me.com")
me.welcome
me.email_all_users
```
JS code:
```js
function User(email) {
  this.email = email;
};

User.prototype.welcome = function() {
	//functionality to send a welcome email:
	console.log('sending welcome email to ' + this.email);
};

function Admin(email, accessLevel) {
  User.call(this, email);
  //Admin.prototype.constructor = Admin

  this.accessLevel = accessLevel;
}
Admin.prototype = Object.create(User.prototype);

Admin.prototype.emailAllUsers = function() {
	// functionality to email all users
	console.log('emailing all users');
}

me = new Admin("me@me.com", 5);
me.emailAllUsers();
me.welcome();
```

## Differences Behind the Scenes:
**Ruby**: Class based
**JS**: Pure objects

**Ruby**: copies functionality into child object
**JS**: Links to functionality by chaining object-prototypes

## Disclaimer 2:
- This chaining lookup allows you to change an object after it is created by changing it's parent's prototype. 


Review:

1. You can do inheritance, like in Ruby, but a little bit different. 
2. Instead of classes, everything is an object, so objects inherit from other objects, or "prototype" objects known as Constructors 
2. Instead of inherited objects copying the functionality of their parent over to them, in JS the child object is linked to its parent. It just references the parent in order to satify the behavior
3. The place where we store functions is in a sub-object on the parent called .prototype
4. the JS engine goes 'up the chain' to check for inherited methods/ attributes
5. You will be taking advantage of inheritance all of the time while using JS, taking advantage of it's power just by using JavaScript, but rarely will you need to implement inheritence yourself in your codebase. 




