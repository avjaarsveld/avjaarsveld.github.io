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

`cd ~/projects/`

`git init example`

`cd example/`

`rspec --init`

bin/parser :

```
#!/usr/bin/env ruby
require_relative '../lib/parser'
Parser.new.parse
```

spec/lib/parser_spec.rb :

```
require 'spec_helper'
require './lib/parser'

describe Parser do
  let :prime_numbers do
    [2,3,5,7,11,13,17,19,23,29]
  end

  it 'can return the first 10 prime numbers' do
    # The line below will work if `first_ten_prime_numbers` is not protected/private
    # expect(Parser.new.first_ten_prime_numbers).to eq (prime_numbers)
    expect(Parser.new.instance_variable_get(:@prime_numbers)).to eq (prime_numbers)
  end

  xit 'can return the whole table as an array of strings' do
    expected_result = [' 2 |   4   6  10  14  22  26  34  38  46  58']
    expected_result << ' 3 |   6   9  15  21  33  39  51  57  69  87'
    # etc...

    expect(Parser.new.parse).to eq(expected_result)
  end
end
```


lib/parser.rb :

```
require 'optparse'
require 'prime'

# Uncomment line below when lib/other_file.rb and spec/lib/other_file_spec.rb are in place
# require_relative 'other_file_in_same_folder' # like require_relative './other_file'

class Parser
  def initialize
    @prime_numbers = first_ten_prime_numbers
    @options = {}
    OptionParser.new do |opts|
      opts.banner = "Usage: parser [options]"

      @options[:something] = :first_option # default

      # Scan the ARGV for a filename and raise if ARGV is empty
      opts.parse
      @options[:filename] = ARGV.pop
      
      # Could raise an error insted of using this default
      @options[:filename] = 'webserver.log' unless @options[:filename] # default

      # Optional argument with keyword completion for type
      opts.on("-t", "--type [TYPE]", [:first_option, :second_option],
              "Select type (first_option, second_option)") do |t|
        @options[:something] = t
      end

    end.parse!
  end

  def parse
    # Do stuff
  end

  def first_ten_prime_numbers
    @prime_numbers ||= Prime.first 10
  end
end
```

Run `rspec` to test

## Command Line

> Run `chmod u+x bin/parser` to make `parser` executable (from the command line, for example `bin/parser`)

`bin/parser -t s filename` for `:something=>:second_option, :filename=>"filename"`

`bin/parser -t first_option filename` for `:something=>:first_option, :filename=>"filename"`