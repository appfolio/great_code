# Loading Files
This document explores the methods for loading files in Ruby. 

Here's the gist:

1. Use [Rails autoloading](#rails-autoloading) for files in the _app/_ directory.
2. Don't depend on or use Rails autoloading for files outside of the _app/_ directory.
3. Prefer Ruby's `require`/`require_relative` over `autoload`.

## Rails Autoloading
http://guides.rubyonrails.org/autoloading_and_reloading_constants.html

### Discussion

Rails’ feature of "class caching" should be named "class refreshing".

"Class caching" is the default behavior of Ruby. That is, to interpret a file in Ruby, you call [`require` or `load`](http://ruby-doc.org/core-2.2.3/Kernel.html#method-i-require). 
The file is read only when you call `require`/`load`.

Rails' autoloading implements class refreshing by configuring the application to reload files that have changed 
between requests by looking for files in the "autoload_paths" configuration setting.

Class refreshing is only useful in:

1. the development environment to support the use case of making changes to the code and not having to restart the server.
2. the test environment w.r.t. [Spring](https://github.com/rails/spring).

Rails’ autoloading provides nearly no value in the production environment as class refreshing is typically not used in favor
of eager loading.

### Avoid Rails Autoloading

By default, Rails autoload_paths are configured to only look in _app/_. 

**Rails' autoloading should not be used for loading files outside of _app/_.**

Ruby autoloading and `require` statements can solve just about everything Rails’ autoloading can solve and in a
more predictable manner.

## Loading files with Ruby
https://practicingruby.com/articles/ways-to-load-code

### Discussion on using require instead of autoload

Ruby’s `autoload` has 2 purposes:

1. Optimize load times.
2. Work around dependency cycles.

With #1, you get on-the-fly loading at the time you need the constant. With #2, you can have the
internals of classes depend on each other without introducing a dependency cycle between them at 
class-definition time.

In practice, both of these purposes are rarely necessary.

RE #1: the optimization should be done deliberately and when needed.
RE #2: this should be a last resort. Nearly 100% of the time, you can break dependency cycles trivially.

My thoughts on that stem from the downsides of “over autoloading”:

1. Depending on autoloading for everything keeps the developers unaware of how to build something
without depending on it and unaware of how to go about debugging it.
2. Developers equate Rails’ autoloading (i.e. class refreshing) with Ruby’s autoloading that causes
all kinds of confusion.
3. The optimization part is rarely an optimization in practice as many constants that are registered
for autoloading are referenced at class definition time anyway.
4. Not using `require` statements makes it very difficult to open a file and see what it depends on.
