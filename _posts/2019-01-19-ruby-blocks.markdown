---
layout: post
title:  "Ruby Blocks"
date:   2019-09-01 10:50:00 -0400
categories: ruby yield blocks
---
Ruby Coding Language
The first time I heard about Ruby and saw the definition that it is an open-source programming language that focuses on simplicity and productivity, I thought it was just like any other scripting language. However, after getting down into the technical details, I came to discover that it had a few unique features which were a bit daunting. However, through this write-up, I will try to expound on this topic.
When using ruby, it is a bit puzzling at first because methods may receive a code block to perform arbitrary segments of code.
What are Ruby Blocks?
A block simply refers to chunks of code, and it is the same thing as a method, besides the fact that it doesn’t belong to an object. In other scripting languages, blocks are referred to as closures. A block can be invoked from a function with the same name as that of the block. I might have you lost you there but what I mean is that, if you have a block with the name ‘test,’ then you can use the function ‘test’ to invoke this block.
Yield Keyword
When used inside the body of a method, the yield keyword can permit you to call the method at hand with a block of code and pass it over, or yield that block. Let’s think yield keyword as something that instructs you to stop executing the code in a given method, and instead, run the code in this block. Then, go back to the code in the method.

For instance:
```ruby
def test_yield
    content = ""

    with_file("/etc/hosts") do |f|
        puts "Read content"
        content << f.read
    end
    content
end
```

The output will be as follows:
Open file
Read content
Close file
When a method expects a block, it responds by calling the yield function. This is very critical, for example, when you want to iterate over a list or to provide a custom algorithm.
For instance:
If i want to define a person classes initialized with a name; and provide a do with name method when invoked, would just pass the name attribute to the block received.

```ruby
class Person
    def initialize( name )
        @name = name
    end

    def do_with_name
       yield( @name )
    end
end
```


This allows me to call this method and pass an arbitrary code block. For example, if I want to print a name;
```ruby
person = Person.new("Oscar")
#invoking the method passing a block
person.do_with_name do |name|
    puts "Hey, my name is #{name}"
end
```
And it would print:
Hey, my name is Oscar.
BEGIN and END Blocks
A program may feature multiple BEGIN and END blocks. BEGIN blocks are usually executed in the order they are encountered while the END blocks are executed in reverse order.

