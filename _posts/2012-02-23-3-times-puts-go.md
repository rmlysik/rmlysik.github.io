---
title: 3.times { puts "go!" }
date: '2012-02-23 04:05:13 -0500'
date_gmt: '2012-02-23 04:05:13 -0500'
categories:
- Ruby on Rails
tags: []
comments:
- id: 40
  author: Victor Goff
  author_email: victor@rubylearning.org
  author_url: http://rubylearning.com
  date: '2012-02-23 07:11:08 -0500'
  date_gmt: '2012-02-23 07:11:08 -0500'
  content: "\"I was not learning the fundamental development skills I would need to
    actually write a web application using Ruby on Rails. I am truly grateful, however,
    for the fact that this course got me started on the path to finally learning Rails.\"\r\n\r\nYou
    are right.  The course is not intended to teach the Rails framework.  But I definitely
    look forward to having you come back to complete the course.  It does cover a
    lot of things that you will work with at various times in your development.\r\n\r\nI
    am not sure that we will ever teach a Rails Course proper.  There are a lot of
    people doing this very thing, and doing a good job of doing so.\r\n\r\nI have
    been enjoying Code School by Envy Labs this month, for Rails and some CSS and
    other web-related things.  It is interactive in an automated kind of way, and
    I think it is a good way to learn.\r\n\r\nThanks for the mention of the RubyLearning.com
    Programming for the Web with Ruby!  We like hearing that you are finding it useful!"
- id: 42
  author: admin
  author_email: robert.lysik@sbcglobal.net
  author_url: ''
  date: '2012-02-24 05:21:25 -0500'
  date_gmt: '2012-02-24 05:21:25 -0500'
  content: Victor, thank you. I really do appreciate the time and effort you've put
    into the course Programming for the Web with Ruby. I'm definitely looking forward
    to finishing the course once I've got a better grounding in Rails.
---
I'd been meaning to learn Ruby on Rails for quite some time now, but hadn't committed myself. I'd heard so much about the beauty of the Ruby language and the power of Ruby on Rails that I wanted to find out what made this language so special. The impetus to finally begin learning Ruby on Rails came while browsing Hacker News one day a few weeks ago. I saw a posting for a free online course *Programming for the Web with Ruby*. On a whim I signed up for the course and began working through the lessons.

Initially, I was very enthusiastic about the course. For the first lesson I installed Ruby and created an account on [Heroku](https://www.heroku.com/ "Heroku"){:target="_blank"}. I had previously installed the version control system Git and established a [GitHub](https://github.com/rmlysik "GitHub"){:target="_blank"} account, although it had languished since then for want of time and projects for which I could justify using it.

In the following lessons, I:

*   Created a simple "About Me" webpage using HTML and CSS.
*   Setup an account on RubyGems.org and uploaded a trivial Ruby gem that adds a writesize method to the String class.
*   Installed cURL and experimented with that.
*   Experimented with the net/http, open-uri, hpricot, and nokogiri libraries.

It was at this point that I began to feel that, although I was getting exposed to different aspects of web application development, from using Git and GitHub for version control, to creating and using Ruby gems, I was not learning the fundamental development skills I would need to actually write a web application using Ruby on Rails. I am truly grateful, however, for the fact that this course got me started on the path to finally learning Rails. Once I have a bit more knowledge under my belt I think I will be in a better position to return to complete this course.

I then began searching for an alternative that would get me started down the path to really understanding Ruby on Rails. That's when I happened upon the excellent [Ruby on Rails Tutorial](https://www.railstutorial.org/ "Ruby on Rails Tutorial"){:target="_blank"} by Michael Hartl. I've now worked through the first four chapters of this online tutorial, and I honestly can't wait to begin the next chapter. What makes this tutorial successful in my view is that the author introduces only as much information as is needed for the particular lesson. The lessons also build on one another and are structured in a way to make it seem almost effortless. There is of course the obligatory setup of the Ruby environment, installing Git and setting up GitHub and Heroku accounts, but once this is out of the way the tutorial progresses smoothly and methodically.

The author starts by giving a brief demonstration of the power of Rails to scaffold an application by creating a Twitter-like micropost application. This gives the reader a taste of what is possible, but as the author acknowledges, it doesn't provide any real understanding of the underlying system.

In the following chapter the author starts fresh by creating a basic application with static pages in order to focus on just the controller and view aspects of the Rails MVC framework. He also introduces the concept of test driven development and uses that throughout the remainder of the chapter as additional features are added, first by creating the test that validates the desired functionality but which fails, and then writing the code to make the test pass.

Chapter four delves into aspects of the Ruby language. The author starts the chapter by defining a helper which is a method for use in views. In this case it is a method that formats the title displayed on each page of the application. After demonstrating its use in the application the author goes on to discuss string interpolation, methods and control flow. He then revisits the helper method defined at the start of the chapter to show how these elements all come together. From there the author goes on to investigate arrays, hashes, blocks and classes.

What is deviously clever about this tutorial is that the author intertwines lessons in the mechanics of Rails with software development practices such as version control and test driven development. For anyone who is just starting to learn Ruby on Rails, I highly recommend Michael Hartl's Ruby on Rails Tutorial.
