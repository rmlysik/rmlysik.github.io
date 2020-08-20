---
title: 'Ruby: First Impressions'
date: '2012-02-26 21:14:36 -0500'
date_gmt: '2012-02-27 02:14:36 -0500'
categories:
- Ruby
tags: []
comments: []
---
As a initiate into the world of Ruby, and as someone coming from a C++ / C# background, I thought I'd jot down some of my initial observations of the Ruby language that I've gleaned so far from reading Michael Hartl's [Ruby on Rails Tutorial](https://www.railstutorial.org/book "Ruby on Rails Tutorial"){:target="_blank"}. As I progress further into my understanding of Ruby and get familiar with the syntax it's very likely that I'll forget what initially struck me as peculiar and interesting about Ruby. At that point everything will have become obvious to me and I won't be able to fathom how it could ever have been done differently. But for now, here goes my initial reactions to Ruby:

### if / unless

I'm accustomed to control blocks that look like this:

{% highlight cpp %}
if (x > 0)
  Console.WriteLine("positive");
{% endhighlight %}

However, Ruby allows you to phrase control blocks in a way that more closely approximates usage in the English language, so you can have a statement like:

{% highlight ruby %}puts "positive" if x > 0{% endhighlight %}

or, using unless:

{% highlight ruby %}
puts "positive" unless x < 0
{% endhighlight %}

By the way, no parenthesis, no semi-colons either...

### Implicit Return

Now this is interesting, you don't need to explicitly state that you are returning a value from a function, as you would in C++/C#:

{% highlight cpp %}
if (x > 0)
  return "positive"
{% endhighlight %}

But in Ruby you can do the following:

{% highlight ruby %}
if x > 0
  "positive"
{% endhighlight %}

### Array Negative Indexing

Ruby arrays are zero-offset, as in C++, so the Ruby way of allocating an array and accessing its members is not unusual:

{% highlight ruby %}
my_array = [13, 21, 34]
my_array[0] # = 13
my_array[1] # = 21
my_array[2] # = 34
{% endhighlight %}

What *is* interesting is that Ruby supports negative indexes into arrays o_O:

{% highlight ruby %}
my_array[-1] # = 34
my_array[-2] # = 21
my_array[-3] # = 13
{% endhighlight %}

Ruby arrays also support accessing members using the methods first and last:

{% highlight ruby %}
my_array.first # = 13
my_array.last  # = 34
{% endhighlight %}

You can also pass a parameter to these methods to obtain the first or last *n* items from an array:

{% highlight ruby %}
my_array.first(2) # = [13, 21]
my_array.last(2)  # = [21, 34]
{% endhighlight %}

Finally, you can also use methods second, third, fourth and fifth (but that's it!):

{% highlight ruby %}
my_array.second # = 21
my_array.third  # = 34
{% endhighlight %}

Would I use any of this? I suspect that the first(n) and last(n) methods will come in handy, but I'm undecided about the rest. It certainly provides a lot of flexibility.

### Ranges

Now here's an elegant feature of the Ruby language. Apparently ranges can be created using the Enumerable class in C#, but it is accomplished much more simply in Ruby.
In Ruby a range can be created using the inclusive two-dot (..) operator:

{% highlight ruby %}
my_range = 0..3 # 0, 1, 2, 3
{% endhighlight %}

or the exclusive three-dot (...) operator:

{% highlight ruby %}
my_range = 0...3 # 0, 1, 2
{% endhighlight %}

This can be accomplished in C#, though much less elegantly, using the Enumerable class, see the [explanation](https://stevenharman.net/ "explanation"){:target="_blank"} on Steve Harman's blog:

{% highlight cpp %}
IEnumerable myRange = Enumerable.Range(0, 3);
{% endhighlight %}

But wait, there's more... In Ruby I can declare a range of characters:

{% highlight ruby %}
my_range = 'a'..'f' # a, b, c, d, e, f
{% endhighlight %}

and I can even create a range using strings:

{% highlight ruby %}
my_range = 'dog'..'dot' # 'dog', 'doh', 'doi' ... ,'dot'
{% endhighlight %}

Although I am hard pressed at this point to imagine how I will use this, an example using arrays and ranges from the [Ruby on Rails Tutorial](https://www.railstutorial.org/book/rails_flavored_ruby#sec-arrays_and_ranges "Ruby on Rails Tutorial"){:target="_blank"} seems useful:

{% highlight ruby %}
('a'..'z').to_a.shuffle[0..7].join
{% endhighlight %}

Which creates an array from the range of letters a through z, randomly shuffles them, and then joins the first eight characters of the resulting array to form a string.

### Blocks

Another very interesting and useful feature of Ruby is the concept of blocks which seems most analogous to the foreach statement in C#:

{% highlight cpp %}
int[] myArray = new int[] { 1, 3, 5, 7, 9 };
foreach (int i in myArray)
{
  System.Console.WriteLine(i);
}
{% endhighlight %}

In Ruby we might have:

{% highlight ruby %}
(1..5).each { |i| puts i } # outputs 1, 2, 3, 4, and 5
{% endhighlight %}

Each value in the range 1..5 is passed to the block variable name enclosed between the vertical bar `|` characters. Block methods can also be represented using an alternative syntax with do..end:

{% highlight ruby %}
(1..5).each do |i|
  puts i
end
{% endhighlight %}

Another interesting feature is the map function, which allows you to apply a block to each element in an array or range:

{% highlight ruby %}
(1..3).map { |i| puts i*2 } # outputs [2, 4, 6]
{% endhighlight %}

Now *that* looks like it will be very useful.

### Conclusion

Although the Ruby syntax may at first blush be quite different from what I've become accustomed to, there are many analogous features between C# and Ruby. It's hard to say at this point whether I'll find Ruby to be a more effective language. After I've gone through some more extensive examples I may have a better feeling for where Ruby's strengths lie.
