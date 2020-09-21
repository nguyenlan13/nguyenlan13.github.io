---
layout: post
title:      "Self in Ruby"
date:       2020-09-21 02:30:27 +0000
permalink:  self_in_ruby
---


In Ruby, everything is an object. Self in Ruby always refers to the current object, regardless of context. The context in which self is used will determine the meaning. 

Using self inside a class definition will reference the parent class.
```
class Animal
     puts "Self inside class definition is #{self}"
end
```
Self inside class definition is Animal


Using self to define a class method will also reference the parent class but not to individual instance of the class. In the example below, self.age is a reader method and can be called by Animal.age . Attribute accessors, writers, and readers are all class methods. 

```
class Animal
    attr_accessor :name
    attr_writer :weight

    def self.age
        puts "Self in a class method is #{self}"
    end
end

```
Self in a class method is Animal


Self in the context of an instance method will refer to the individual instance of the class but not to the class itself. Instance methods cannot be called in the same way that class methods are called, rather it can only be called after a new instance of the of class is instantiated.

```
class Animal

    def initialize(type)

    def type
        puts "Self in an instance method is #{self}
        return "Horse"
    end
end
```

animal = Animal.new
puts "the 'type' is #{animal.type}"

Self in an instance method is #<Animal:0x00000004bvc34c6>
the 'type' is Horse

