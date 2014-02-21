---
layout: post
title:  "Strings and Char Lists"
tags:   strings, string, char, charlists
date:   2014-02-21 08:00:00
---

## Strings

As we saw in [Basic Types](/basic-types), strings in Elixir are implemented using utf8 binaries.

{% highlight elixir %}
iex> is_binary "hello"
true
{% endhighlight %}

Strings offer easy interpolation, using any valid Elixir expression:

{% highlight elixir %}
iex> name = "Paul"
"Paul"
iex> "Hello #{name}!"
"Hello Paul!"
{% endhighlight %}

Elixir supports multiline strings:

{% highlight elixir %}
iex> IO.puts "This is a
...>     multiline
...>     string!"
This is a
    multiline
    string
:ok
{% endhighlight %}

As you can see, it preserves the spacing exactly as written. This is usually not the intended output. Elixir
has heredocs, which allow you to specify the margin for the string, which addresses this:

{% highlight elixir %}
iex> IO.puts """
...>     This is a heredoc, you can control
...>     the margin by aligning the trailing
...>     quotes to the body of your text. You
...>     can "double" and 'single' quote
...>     inside them without escaping.
This is a heredoc, you can control
the margin by aligning the trailing
quotes to the body of your text.
You can "double" and 'single' quote
inside them without escaping.
:ok
{% endhighlight %}

Heredocs are used heavily for documentation.

## Char Lists

Single-quoted strings are called char lists. As you might guess, where double-quoted strings are implemented 
using binaries, char lists are implemented using lists.

{% highlight elixir %}
iex> 'hello'
'hello'
iex> is_binary 'hello'
false
iex> is_list 'hello'
true
{% endhighlight %}

Char lists support all the same features as double-quoted strings - interpolation, multiline strings, and heredocs.

In general, double-quoted strings are preferred over char lists, which are typically only used when interfacing
with Erlang modules.
