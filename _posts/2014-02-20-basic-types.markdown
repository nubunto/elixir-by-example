---
layout: post
title:  "Basic Types"
tags:   types
date:   2014-02-20 20:37:00
---

Elixir has the following built-in types:

## Integers

{% highlight elixir %}
iex> decimal = 1000
1000
iex> -5
-5
iex> hex = 0xabcd
43981
iex> bin = 0b1100
12
{% endhighlight %}

Note: There is no fixed limit to the size of integers.

## Floats

{% highlight elixir %}
iex> 4.0
4.0
iex> 0.567
0.567
iex> 0.567e2
56.7
iex> 0.567e-2
0.00567
{% endhighlight %}

Note: Floats in Elixir are double precision, accurate up to 16 digits.

## Booleans

Booleans are booleans.

{% highlight elixir %}
iex> true
true
iex> true == true
true
iex> true == false
false
{% endhighlight %}

No surprises there!

## Atoms

Atoms are essentially constants. Their value is their name.

{% highlight elixir %}
iex> :stuff
:stuff
iex> :stuff == :stuff
true
iex> :+
:+
{% endhighlight %}

Atoms can contain arbitrary characters, but must be enclosed in quotes.

{% highlight elixir %}
iex> :"Hello World!"
:"Hello World!"
{% endhighlight %}

Atoms also serve a dual purpose for accessing Erlang modules, which we'll see in later examples.

## Binaries

Binaries are simply a collection of bits and bytes.

{% highlight elixir %}
iex> <<1, 2, 3>>
<<1, 2, 3>>
iex> size <<1, 2, 3>>
3
{% endhighlight %}

You can pattern match on binaries:

{% highlight elixir %}
iex> << head, tail :: binary >> = << 1, 2, 3 >>
<<1, 2, 3>>
iex> head
1
iex> tail
<<2, 3>>
{% endhighlight %}

You can modify the type and size of each field of the binary like so:

{% highlight elixir %}
iex> <<1 :: size(2), 2 :: size(4), 3 :: size(2) >>
"K"
iex> << 100 :: utf8, 250 :: utf8, 300 :: utf8 >>
"dúĬ"
{% endhighlight %}

As you can see, IEx renders printable binaries as if they are strings. This is because in Elixir, strings are
implemented using binaries! This can be confusing, just be aware of it when playing with binaries in IEx.

