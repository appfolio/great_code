<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [General Programming](#general-programming)
- [Javascript](#javascript)
- [Ruby](#ruby)
  - [General](#general)
  - [Naming](#naming)
  - [Methods](#methods)
  - [Objects](#objects)
  - [Classes](#classes)
  - [Modules](#modules)
  - [Tests](#tests)
  - [Gems](#gems)
- [Rails](#rails)
  - [General](#general-1)
  - [Tests](#tests-1)
  - [Controllers](#controllers)
  - [Controller tests](#controller-tests)
  - [Helpers](#helpers)
  - [Helper tests](#helper-tests)
  - [Templates](#templates)
  - [Partials](#partials)
  - [Models](#models)
  - [Engines](#engines)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

***

# General Programming
- Organize code on filesystem in a meaningful manner
- Declare dependencies
- Prefer additive synthesis over subtractive synthesis
- Follow [SOLID](http://en.wikipedia.org/wiki/SOLID_%28object-oriented_design%29), [DRY](http://en.wikipedia.org/wiki/Don%27t_repeat_yourself), and the [Law of Demeter](http://en.wikipedia.org/wiki/Law_of_Demeter)
- Avoid [Connascence](http://en.wikipedia.org/wiki/Connascence_(computer_programming))
- [Wrap data in objects and provide methods to interact with the data on the class of the object](http://en.wikipedia.org/wiki/Object-oriented_programming)
- Use comments
- Use local variables to improve readability
- Delete commented-out code
- Delete unused code
- Test your code
- Address deprecation warnings; don't add new ones
- Mind code line lengths; use whitespace 
- Make [small things](http://en.wikipedia.org/wiki/Division_of_labour) (classes, modules, objects, subsystems, etc.) that have [specific responsibilities](http://en.wikipedia.org/wiki/Single_responsibility_principle)

# Javascript
- Understand the integral types
- Understand prototypal inheritance
- Use modules
- Avoid globals

# Ruby

## General
- Avoid globals ($global_var, referencing external constants, ENV)
- Avoid dangling references
- Avoid opening classes/modules
- Avoid using `eval`
- Prefer composing objects over using mixins
- Avoid using `alias`, `alias_method` or `alias_method_chain`
- Avoid using keywords or common methods for names (e.g. `send`, `include`, etc.)
- Prefer variables with the smallest scope (local variables, instance variables, class instance variables, class variables)
- Avoid inverted `if`/`unless` statements with complicated expressions
- Avoid `unless` statements with more than one terminal in the expression
- Prefer `if`/`unless` statements over ternaries
- Avoid using `send`, `instance_variable_set` and `instance_variable_get`
- Memoize only when necessary
- Only use the global resolution operator (`::`) when necessary
- Access class instance methods via the dot (`.`) operator instead of the double-colon (`::`) operator
- Avoid using `respond_to?` to check for `nil?`
- Prefer methods over blocks/procs/lambdas
- Prefer using parenthesis for method invocations
- Avoid uses of `respond_to?` and `method_defined?`
- Prefer `respond_to?` over `obj.class.method_defined?`
- Raise well-named, descriptive exceptions; don't call `raise` without an exception class

## Naming
- Use meaningful, intention-revealing names.
- Avoid context-less prefixes/suffixes (Helper/helper, Methods, Mixin, Data/data, etc.)

## Methods
- Choose good names
- Should be small
- Use `?` suffix for queries
- Generally, don't use `!` suffix; only use it according to a prevailing convention
- Prefer keyword args over options hashes
- Do not modify input parameters
- Wrap exceptions
- Use required parameters by default; only provide defaults when necessary

## Objects
- Prefer instances over classes and modules
- Use objects to encapsulate state
- Prefer local variables over instance variables
- Instance variables should hold state with the same life span as the object.
- Don't use instance variables to pass data across methods
- Only provide accessors when necessary
- Inject dependencies

## Classes
- Choose good names
- Prefer [composition over inheritance](http://engineering.appfolio.com/2014/08/20/a-composition-regarding-inheritance/)
- Specify method visibility
- Default to using `private`, not `protected`
- [Use `protected` only when you need to; you most likely don't need to](https://docs.google.com/a/appfolio.com/presentation/d/1U9UiDv6dHSNhVYzVsu7a8eKbC2xEb93OBqTbDVWLE6o/edit?usp=sharing)
- Avoid "class methods"
- Put nested classes in separate files
- Extract complex private/protected methods into other classes

## Modules
- Use [`ActiveSupport::Concern`](http://engineering.appfolio.com/2013/06/17/ruby-mixins-activesupportconcern/) only when you need to
- Create single purpose modules: used as a mixin, used for namespacing, used for holding static methods, defining constants, etc.

## Tests
- Test every code path
- Only test private/protected methods when complex
- Prefer minitest assertions over test-unit
- Test behaviour over implementation
- Avoid computing expected results

## Gems
- Use [semantic versioning](http://semver.org/)
- Require dependencies in manifest
- Use versioned dependencies
- Test the gem
- Use [Appraisals](https://github.com/thoughtbot/appraisal)
- Provide documentation

# Rails

## General
- Avoid Rails' autoloading where possible
- Prefer the Rails Way unless you have a good reason not to
- Prefer Ruby's `nil?` over ActiveSupport's `present?`/`blank?`
- Generally avoid and only use `try`/`present?`/`blank?` when appropriate

## Tests
- Don't override setup/teardown
- Use setup/teardown block helpers
- Setup/teardown hooks should only do things common to all tests in the TestCase class
- Use private methods to denote "non test" methods
- Nest helper classes/module definitions under the TestCase class
- Test file organization should mirror file organization of code under test

## Controllers
- Only use their own helper / Never use another controller's helper
- Never use the `helper` method
- Use [form objects](http://blog.codeclimate.com/blog/2012/10/17/7-ways-to-decompose-fat-activerecord-models/#form-objects)
- Use services for business logic
- Verify parameters
- Use the appropriate HTTP status code

## Controller tests
- Rails Way: only one controller action per test
- Use the correct action method (`get`, `post`, `xhr`, etc.)
- Assert on HTTP response
- Avoid using `assigns`
- Assert on effect of controller action

## Helpers
- Generally prefer presenters, view models or decorators over helpers
- [Do not include helpers of other controllers](https://groups.google.com/a/appfolio.com/forum/?hl=en#!searchin/dev.list/God$20Helpers/dev.list/hKPxbAMuGDw/LEv_jRAC-tQJ)
- Include mixins for all dependencies
- Do not depend on controller-helper stack
- Do not act on instance variables

## Helper tests
- Should not require a specific controller context
- Use `view.` handle
- Avoid using `instance_variable_set`

## Templates
- Do not render templates or partials of other controllers
- Do not use instance variables
- Use partials
- Use view models
- No logic

## Partials
- Same as templates
- Partials that can be rendered by more than one controller go in views/shared

## Models
- Use services for business logic
- Avoid ActiveRecord callbacks
- Avoid overriding common `ActiveRecord::Base` methods (`initialize`, `save`/`save!`, `create`/`create!`, etc.)
- Avoid using `default_scope`
- Avoid using `update_attribute`
- Prefer and default to using validations
- Prefer and default to using `!`-methods that raise exceptions when validations fail
- Handle the return value when using non-`!`-methods (e.g. `save` and `create`)

## Engines
- Use injections
- Make injections explicit
- Provide injection defaults
- Avoid use of `main_app` view route proxy
- Don't provide, use or reference an "Application" controller, helper, JS, CSS, etc.
