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
 - why?
 - go over some vocab
 - see a demo of it in Ruby and JS using a real world example
 - discuss what the differences are
 - review


## Why - do we need to know?
- We make use of inheritance anytime we use JS! We should know what is going on behind the scenes.
- We may want to implement inheritence ourselves in our code.

## Disclaimer:
- It isn't common to need to implement inheritence in small to medium sized projects. Use only when it REALLY makes sense. Forcing data into inheritence patterns will create a bad situation.

## Vocab:
**prototype**: an object that is used as a template to make other objects.

**inheritance**: giving the stuff of the parent to the kids. There is only one parent in inheritence in computer science.

**constructor**: A function that is used as a prototype object. It creates new objects like itself.

## Demo 1: 
Creating an instance of a class/prototype

**Ruby**:
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
**JavaScript**:
```js
class User {
  constructor (email) {
    this.email = email;
  }
  
  welcome () {
    //functionality to send a welcome email:
    console.log('sending welcome email to ' + this.email);
  }
};

me = new User("me@me.com");
// User { email: 'me@me.com' }
me.email;
// 'me@me.com'
me.welcome();
// sending welcome email to me@me.com
```
## Demo 2: Inheritence
**Ruby**:
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
**JS**:
```js
class User {
  constructor (email) {
    this.email = email;
  }
  
  welcome () {
    //functionality to send a welcome email:
    console.log('sending welcome email to ' + this.email);
  }
};

class Admin extends User {
  constructor (email, accessLevel) {
    super(email);
    this.accessLevel = accessLevel;
  }

  emailAllUsers () {
    // functionality to email all users
    console.log('emailing all users');	
  }
}

me = new Admin("me@me.com", 5);
// Admin { email: 'me@me.com', accessLevel: 5 }
me.emailAllUsers();
// emailing all users
me.welcome();
// sending welcome email to me@me.com

```

## Differences Behind the Scenes:
**Ruby**: Class based

**JS**: Pure objects

**Ruby**: Copies functionality of parent class into child object

**JS**: Links to functionality of parent object by looking 'up the chain' of inherited Constructors

### Disclaimer 2:
- This chaining lookup allows you to change an object after it is created by changing it's parent's prototype. 


## Review:

1. You can do inheritance, like in Ruby, but a little bit different. 
2. Instead of classes, everything is an object, so objects inherit from "prototype" objects known as Constructors 
4. the JS engine looks 'up the chain' to check for inherited methods/ attributes, rather than the object copying everything into itself
5. You will be taking advantage of the power of inheritance just by using JavaScript, but rarely will you need to implement inheritence yourself in your codebase. 




