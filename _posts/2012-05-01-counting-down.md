---
layout: post
status: publish
published: true
title: Counting Down
author_url: http://robertlysik.com
date: '2012-05-01 23:23:22 -0400'
date_gmt: '2012-05-02 03:23:22 -0400'
categories:
- Ruby on Rails
- JavaScript
tags: []
comments:
- id: 120
  author: Thanh Huynh
  author_email: hkthanh89@gmail.com
  author_url: ''
  date: '2012-09-12 06:16:33 -0400'
  date_gmt: '2012-09-12 10:16:33 -0400'
  content: I think you should use keyup() function, because when i used your code,
    i realized keydown() function not work accurate, when i typed the first character,
    counter was still 140, or i typed 2 first character and press backspace 2 times,
    counter was 139 but it must be 140.  So i changed to keydown() function and it
    works well. Any way, thanks for your code help me to do counter :D
- id: 121
  author: Robert
  author_email: robert.lysik@sbcglobal.net
  author_url: http://robertlysik.com
  date: '2012-09-12 23:25:04 -0400'
  date_gmt: '2012-09-13 03:25:04 -0400'
  content: Yes, you're absolutely right, good catch! I've gone ahead and edited the
    post to reflect your recommendation. Thank you!
---
I generally learn more by doing something rather than just reading about it, or watching someone else do something. I've been working through each of the exercises in the Ruby on Rails tutorial with the hope that some of this knowledge will sink in. I've now reached the exercises for the penultimate :) chapter of the tutorial, and the last exercise for this chapter is prefaced with the warning **challenging**:

> Add a JavaScript display to the Home page to count down from 140 characters.
    
### The Plan

Simple enough, I imagine. We'll just display the number of remaining characters below the text field like so:

![Micropost Counter](/images/posts/2012/04/MicropostCounter.png "MicropostCounter")

The first thing we'll do is add a div to the existing partial for the home page that I'll call "counter" (line 6):

app/views/shared/_micropost_form.html.erb

{% highlight ruby %}
<%= form_for(@micropost) do |f| %>
  <%= render 'shared/error_messages', object: f.object %>
  <div class="field">
    <%= f.text_area :content, placeholder: "Compose new micropost..."%>
  </div>
  <div id="counter">140</div>
  <%= f.submit "Post", class: "btn btn-large btn-primary" %>
<% end %>
{% endhighlight %}

Unfortunately this places the counter in an awkward location:

![Counter Position Prior to CSS Change](/images/posts/2012/04/BeforeCSS1.png "BeforeCSS")

So to fix this, we'll add a class "counter" to the div:

{% highlight html %}
<div id="counter" class="counter">140</div>
{% endhighlight %}

And add a "counter" class definition to the custom.css.scss file in the microposts section:

app/assets/stylesheets/custom.css.scss

{% highlight css %}
/* microposts */
.counter {
  float: right;
}
{% endhighlight %}

Now the counter will be displayed in the lower right corner as shown in the first example.

### The Script

Next comes the JavaScript. We need to subtract the length of text for the textarea element from 140 and display the result in the counter div.
Since we're already pulling in jQuery, I figured we might as well take advantage of it:

{% highlight javascript %}
$(document).ready(function() {
  $("#micropost_content").keyup(function() {
    $("#counter").text(140 - $(this).val().length);
  });
});
{% endhighlight %}

So what's going on here?

[1] Wait for the document to load using $(document).ready().

[2] Bind our handler method to the keyup event for the micropost_content textarea element. `$("#micropost_content")` returns the element having an id matching micropost_content. keyup() binds the specified function to the keyup event.

[3] Set the text of the counter div element to the difference of 140 and the length of the text in the micropost_content element. $this refers to the micropost_content textarea element.

To give this counter added emphasis, it would be nice to set the color of the text to red when the value becomes negative.

{% highlight javascript %}
$(document).ready(function() {
  $("#micropost_content").keyup(function() {
    var counter = $("#counter");
    var charsRemaining = 140 - $(this).val().length;
    counter.text(charsRemaining);
    counter.css('color', (charsRemaining < 0) ? 'red' : 'black');
  });
});
{% endhighlight %}

Points of interest:

[3] The counter variable was added so that we don't need to traverse the DOM again to get the micropost_content element.

[4] The value of the variable charsRemaining will be displayed in the counter div and will also be used to determine the text color.

[6] Here the jQuery css() method is used to set the value of the 'color' property of the counter element. The ternary operator is employed to return the text color, reads as "If charsRemaining is less than zero, return 'red' otherwise return 'black'". The string returned is passed as an argument to the css() method to set the 'color' property.
Now when the maximum number of characters is exceeded the text should be red:

![Micropost Limit Exceeded](/images/posts/2012/05/LimitExceeded.png "LimitExceeded")

Although I could probably leave the script tag in the micropost form partial, I'd rather like to have it pulled into the head element of the document. I came across one suggestion for how to do this on [StackOverflow](https://stackoverflow.com/questions/3437585/best-way-to-add-page-specific-javascript-in-a-rails-3-app "StackOverflow"){:target="_blank"}. First, wrap the script section in a content_for block, like so:

app/views/shared/_micropost_form.html.erb

{% highlight ruby %}
<% content_for :head do %>
<script type="text/javascript">
  $(document).ready(function() {
      $("#micropost_content").keyup(function() {
        var counter = $("#counter");
        var charsRemaining = 140 - $(this).val().length;
        counter.text(charsRemaining);
        counter.css('color', (charsRemaining < 0) ? 'red' : 'black');
      });
    });
</script>
<% end %>
{% endhighlight %}

Then yield to the block in the application layout (line 8):

app/views/layouts/application.html.erb

{% highlight html %}
<!DOCTYPE html>
<html>
  <head>
    <title><%= full_title(yield(:title)) %></title>
    <%= stylesheet_link_tag    "application", media: "all" %>
    <%= javascript_include_tag "application" %>
    <%= csrf_meta_tags %>
    <%= yield :head %>
    <%= render 'layouts/shim' %>
  </head>
  <body>
    <%= render 'layouts/header' %>
    <div class="container">
      <% flash.each do |key, value| %>
        <%= content_tag(:div, value, class: "alert alert-#{key}") %>
      <% end %>
      <%= yield %>
      <%= render 'layouts/footer' %>
      <%= debug(params) if Rails.env.development? %>
    </div>
  </body>
</html>
{% endhighlight %}

If you view source on the home page now you should see that the counter script appears in the head element. Furthermore, when you browse to any other page, the counter script shouldn't exist.
