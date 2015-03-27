## Logging
by Tim Pease ![http://travis-ci.org/TwP/logging](https://secure.travis-ci.org/TwP/logging.png)

* [Homepage](http://rubygems.org/gems/logging)
* [Github Project](https://github.com/TwP/logging)
* email tim dot pease at gmail dot com

### Description

Logging is a flexible logging library for use in Ruby programs based on the
design of Java's log4j library. It features a hierarchical logging system,
custom level names, multiple output destinations per log event, custom
formatting, and more.

### Install

```
gem install logging
```

### Example

This example configures a logger to output messages in a format similar to the
core ruby Logger class. Only log messages that are warnings or higher will be
logged.

```ruby
require 'logging'

logger = Logging.logger(STDOUT)
logger.level = :warn

logger.debug "this debug message will not be output by the logger"
logger.warn "this is your last warning"
```

In this example, a single logger is created that will append to STDOUT and to a
file. Only log messages that are informational or higher will be logged.

```ruby
require 'logging'

logger = Logging.logger['example_logger']
logger.add_appenders(
    Logging.appenders.stdout,
    Logging.appenders.file('example.log')
)
logger.level = :info

logger.debug "this debug message will not be output by the logger"
logger.info "just some friendly advice"
```

The Logging library was created to allow each class in a program to have its
own configurable logger. The logging level for a particular class can be
changed independently of all other loggers in the system. This example shows
the recommended way of accomplishing this.

```ruby
require 'logging'

Logging.logger['FirstClass'].level = :warn
Logging.logger['SecondClass'].level = :debug

class FirstClass
  def initialize
    @logger = Logging.logger[self]
  end

  def some_method
    @logger.debug "some method was called on #{self.inspect}"
  end
end

class SecondClass
  def initialize
    @logger = Logging.logger[self]
  end

  def another_method
    @logger.debug "another method was called on #{self.inspect}"
  end
end
```

There are many more examples in the [examples folder](https://github.com/TwP/logging/tree/master/examples)
of the logging package. The recommended reading order is the following:

* [simple.rb](https://github.com/TwP/logging/blob/master/examples/simple.rb)
* [rspec_integration.rb](https://github.com/TwP/logging/blob/master/examples/rspec_integration.rb)
* [loggers.rb](https://github.com/TwP/logging/blob/master/examples/loggers.rb)
* [classes.rb](https://github.com/TwP/logging/blob/master/examples/classes.rb)
* [hierarchies.rb](https://github.com/TwP/logging/blob/master/examples/hierarchies.rb)
* [names.rb](https://github.com/TwP/logging/blob/master/examples/names.rb)
* [lazy.rb](https://github.com/TwP/logging/blob/master/examples/lazy.rb)
* [appenders.rb](https://github.com/TwP/logging/blob/master/examples/appenders.rb)
* [layouts.rb](https://github.com/TwP/logging/blob/master/examples/layouts.rb)
* [formatting.rb](https://github.com/TwP/logging/blob/master/examples/formatting.rb)
* [colorization.rb](https://github.com/TwP/logging/blob/master/examples/colorization.rb)
* [consolidation.rb](https://github.com/TwP/logging/blob/master/examples/consolidation.rb)
* [fork.rb](https://github.com/TwP/logging/blob/master/examples/fork.rb)
* [mdc.rb](https://github.com/TwP/logging/blob/master/examples/mdc.rb)

### Notes

Although Logging is intended to supersede Log4r, it is not a one-to-one
replacement for the Log4r library. Most notably is the difference in namespaces
-- Logging vs. Log4r. Other differences include renaming Log4r::Outputter to
Logging::Appender and renaming Log4r::Formatter to Logging::Layout. These
changes were meant to bring the Logging class names more in line with the Log4j
class names.

### Requirements

The Logging source code relies on the Mr Bones project for default rake tasks.
You will need to install the Mr Bones gem if you want to build or test the
logging gem.

```
gem install bones
```

After Mr Bones is installed you can install all the depdencies via the rake
task.

```
rake gem:install_dependencies
```

Always remember that `rake -T` is your friend!

### License

The MIT License

Copyright (c) 2015 Tim Pease

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
