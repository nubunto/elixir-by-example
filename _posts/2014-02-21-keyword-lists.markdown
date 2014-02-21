---
layout: post
title:  "Keyword Lists"
tags:   lists, keywords, keyword lists
date:   2014-02-21 09:00:00
---

## Keyword Lists

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

These are quite commonly used in Elixir code.