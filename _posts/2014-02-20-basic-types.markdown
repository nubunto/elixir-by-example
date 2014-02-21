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

## Ranges

Ranges are defined by a start and end value (inclusive). They can be
iterated over as long as the start and end values are integers.

{% highlight elixir %}
iex> 1..3
1..3
iex> Enum.each 1..3, fn num -> num * 2 end
[2, 4, 6]
{% endhighlight %}

Simple and easy!

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

## Tuples

Tuples are an ordered collection of values. They can be of any type (like all Elixir collections).

{% highlight elixir %}
iex> {:stuff, 1, "things"}
{:stuff, 1, "things"}
{% endhighlight %}

They can be used in pattern matching (covered in more detail in another example):

{% highlight elixir %}
iex> {stuff, num, _} = {:stuff, 1, "things"}
{:stuff, 1, "things"}
iex> stuff
:stuff
iex> num
1
{% endhighlight %}

Tuples are often used in Elixir when performing some action which could fail:

{% highlight elixir %}
iex> {status, handle} = File.open("example.txt")
{:ok, #PID<0.43.0>}
{% endhighlight %}

Combined with pattern matching, you can assert the result of an operation, which will throw an error if
the result does not match the pattern specified:

{% highlight elixir %}
iex> {:ok, handle} = File.open("doesntexist.txt")
** (MatchError) no match of right hand side value: {:error, :enoent}
{% endhighlight %}

This pattern is common, and is extremely useful.

## Lists

Lists are implemented as linked lists. They differ from tuples in that tuples are stored
contiguously in memory, and are therefore able to access elements in constant time. Updating
a tuple requires a copy of the entire tuple's data. Lists however are very cheap when adding
or removing elements, but require traversal of the list to reach a given element. Lists, like
tuples, can contain values of any type.

{% highlight elixir %}
iex> [1, 2, 3]
[1, 2, 3]
iex> [:stuff, 1, "things"]
[:stuff, 2, "things"]
{% endhighlight %}

Lists can be pattern matched:

{% highlight elixir %}
iex> [_, two, _] = [1, 2, 3]
[1, 2, 3]
iex> two
2
iex> [head | tail] = [1, 2, 3, 4]
[1, 2, 3, 4]
iex> head
1
iex> tail
[2, 3, 4]
{% endhighlight %}

Elixir has a special syntax for lists of keywords, also called keyword lists. This is sugar for a list
of two-element tuples, where the first element of the tuple is an atom:

{% highlight elixir %}
iex> [head | tail] = [a: 1, b: 2]
[a: 1, b: 2]
iex> head
{:a, 1}
iex> Keywords.get [a: 1, b: 2], :a
1
iex> Keywords.get_values [a: 1, b: 2]
[1, 2]
{% endhighlight %}

This is another type that is commonly used.

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

## Strings and Char Lists

As we saw above, strings in Elixir are implemented using utf8 binaries.

{% highlight elixir %}
iex> is_binary "hello"
true
{% endhighlight %}

Strings have a counterpart, called char lists. As you might guess, where strings are implemented using binaries,
char lists are implemented using lists.

{% highlight elixir %}
iex> 'hello'
'hello'
iex> is_binary 'hello'
false
iex> is_list 'hello'
true
{% endhighlight %}

In general, double-quoted strings are preferred over char lists, which are typically only used when interfacing
with Erlang modules.

