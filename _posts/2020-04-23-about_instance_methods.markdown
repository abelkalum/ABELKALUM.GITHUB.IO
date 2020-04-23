---
layout: post
title:      "About Instance Methods"
date:       2020-04-23 14:51:11 +0000
permalink:  about_instance_methods
---


What hyped up my interest in Instance Methods is the fact that Ruby classes are not only “...capable of instantiating new individual instances” but they can also define “what those instances can do.” [Learn.co]. I wanted to learn more about what goes on inside a class; what do class and instance methods do.
I do understand that a class encapsulates its instance methods and class methods. It is the responsibility of the class to enact the behavior and functionality of any new features or functionality introduced to the class. So when we define a method inside a class we are essentially either creating an instance method [ex: def from_an_instance]  or a class methods [ex: def self.from_the_class] as seen in the example below adapted from https://dev.to/adamlombard/ruby-class-methods-vs-instance-methods-4aje
```
class SayHello
  def self.from_the_class
    "Hello, from a class method"
  end
  def from_an_instance
    "Hello, from an instance method"
  end
end
```
Instance methods are used when “*you are required to act on a specific instance of a class. When you need to introduce a functionality that corresponds to the identity of an instance, you should use the instance method.*” [Source: https://www.railscarma.com/blog/ror/ruby-class-methods-class-instance-methods-ruby/]
In other words, when you are dealing with instance methods you should understand that each instance method has its own functionality and the only way to access that functionality is through the instance method.

