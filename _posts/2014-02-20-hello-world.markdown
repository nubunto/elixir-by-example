---
layout: post
title:  "Hello World"
tags: hello world
date:   2014-02-20 17:34:40
---

Our first example will print the classic "hello world" message. First we'll need to open up the Elixir interactive mode. 

{% highlight console %}
$ iex
iex>
{% endhighlight %}

The `iex>` is what lets us know we are running in Elixir's Interactive Mode. It accepts valid Elixir code only. 

{% highlight elixir %}
iex> "hello world"
hello world
{% endhighlight %}

In Elixir everything is an expression so our string "hello world" evaluated to its text. If we want to output something to the console we'd use it like so.

{% highlight elixir %}
iex> IO.puts "hello world"
hello world
:ok
iex>
{% endhighlight %}

Here we've printed out "hello world" and we also got a symbol `:ok`, we won't got into what or why that is for now but just know thats ok! 

If we wanted to close out of `iex` we'll need to type the command `ctrl+c` twice. Now that we can execute and run basic elixir code lets continue.
