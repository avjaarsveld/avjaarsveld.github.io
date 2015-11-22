---
layout: post
tags:
- ruby
- cheatsheet
- development
---

Because ruby methods are named well in general, with easy to remember or guess names this sheet should stay relatively empty. These are some memory joggers...

## What are you?

```
a.is_a? String
a.kind_of? Integer
a.instance_of? Float
```

## Cool Stuff

This section is not for "memory joggers" but rather just some things that make Ruby super cool. Enjoy

```
a,b = ["1", "2"]

> a
=> "1"

> b
=> "2"
```

# Create a new Ruby app with options/parser

`rspec --init`

bin/parser :

```
#!/usr/bin/env ruby
require_relative '../lib/parser'
Parser.new.parse
```

lib/parser.rb :

```
require 'optparse'
require_relative 'other_thing' # lib/other_thing.rb and spec/lib/other_thing_spec.rb
class Parser
  def initialize
    @options = {}
    OptionParser.new do |opts|
      opts.banner = "Usage: parser [options]"

      @options[:something] = :first_boolean_option # default

      # Scan the ARGV for a filename and raise if ARGV is empty
      opts.parse
      @options[:filename] = ARGV.pop
      
      # Could raise an error insted of using this default - default seems more user friendly
      @options[:filename] = 'webserver.log' unless @options[:filename] # default

      # Optional argument with keyword completion for type of something
      opts.on("-t", "--type [TYPE]", [:first_boolean_option, :second_boolean_option],
              "Select type (first_boolean_option, second_boolean_option)") do |t|
        @options[:something] = t
      end

    end.parse!
  end
  def parse
    # Do stuff
  end
end
```

... more to come ...