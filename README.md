<<<<<<< HEAD
# The Path to Faster and Better HTML Sanitization

Kasper Timm Mehli Hansen
email: kaspth@gmail.com
github, twitter: @kaspth
I study Multimedia Design at Copenhagen School of Design and Technology.

## Synopsis
I will improve the HTML sanitization in Ruby on Rails by doing two things:
1. Exchange the existing implementation with an approach that is both safer and faster.
2. On top of the old API provide new API for developers to gain more control over what gets sanitized.

## Project
Outlined here are the two parts of this project and the reasoning behind them.

### Updating the implementation
Today Rails uses the HTML-scanner gem to do its sanitization. My proposal switches the gem that is used, while keeping the old API for backwards compatibility. Instead of the scanner gem, I will use Loofah. Loofah is built on top of Nokogiri, meaning we rid the implementation's reliance on regular expressions and we get speed. On large documents and fragments Loofah is around [60 to 100% faster](https://gist.github.com/flavorjones/170193) than the current implementation.

### Providing a new API
Loofah also makes this next bit possible, because of its support for custom HTML scrubbers. While researching for this proposal I came across a few StackOverflow questions where developers wanted to have more control of what tags were scrubbed [(here's one)](http://stackoverflow.com/questions/6512253/rails-html-sanitizing). This is what I want to bring to Rails.
Here's an example of how I think this could work in a model:
```ruby
class Comment < ActiveRecord::Base
  # block based
  # block takes a node
  scrubs :body do |node|
    node.remove if node.name == "script"
  end
	
  # method based
  # method is last argument and has a node parameter
  scrubs :name, :body, :remove_style_blocks 
	
  # list based via a kind option
  # options are based on the available scrubbers in Loofah
  scrubs :name, kind: :whitelist 
end
```
The new API could be implemented in a separate gem at first, if the Rails core team isn't ready to add it.

So to reiterate the benefit of switching to Loofah for Ruby on Rails is a faster solution which will bring more control to developers.

## Roadmap
I expect the project to take until the end of August with me working about 37-40 hours a week when the coding begins. Here's how I picture the overall roadmap (subject to change by mentor intervention):

1. Learn more about Rails SanitizeHelper API, previous XSS attacks as well as class methods in an ActiveRecord::Base model (from now till late May).
2. Work to refine API idea and flesh out the implementation approach (from now until mid of June, when coding begins).
3. exchange HTML-scanner with Loofah (mid June to 1st July).
4. new API - kind based approach + testing (1st-14th. July).
5. new API - method based approach + testing (14th-28th. July).
6. new API - blocks based approach + testing (28th. July to mid August).
7. General testing/refactoring of new API (until end of August).

## Experience
A quick description of some projects to show my experience.

### Game in ActionScript
A 2d battle arena shooter [published as Open Source](https://github.com/kaspth/prinze-game). I wrote this by myself earlier this year for a project at School. Although we had a course in ActionScript it was extremely limited, so I had to learn a lot in a short time. I found a guide online which showed how to make a 2d platformer [(part 1 here)](http://as3gametuts.com/2011/11/11/platformer-1/). His logic was in one big file though and written at a very basic level. Borrowing his methodology I internalized the code, improved it and turned it into the fighting game, we ended up with. Also worth noting, the project set a high bar for what students could accomplish and went way beyond the teachers' expectations.

### Ruby and Rails development
I have used Ruby for over two years ever since falling in love with it after reading Why's (Poignant) Guide to Ruby. I have used Ruby to automate the uploading of product photos to a website, via the Mechanize gem, after they had vanished from a CMS. I also have some experience developing with Rails, where a partner and I made a blogging app for another school project, but that was a couple of years ago.
Back to now, or more specifically last month, I worked on my own static site generator though it is really bare bones and not quite finished.

### Portfolio website
The generator mentioned above was made to help with this project in School. We had to build our own website using HTML5, CSS and JavaScript. It went above the expectations of the assignment by also using a responsive layout (and even attempting to write a generator). View it [here](http://kasp853b.keaweb.dk/).

There you have it, a peek at a few of the things I have done. I didn't even get to tell you about the iOS development I have dabbled with. Nonetheless, these snippets should have given you an indication that I have experience in shipping Open Source projects, understanding other people's code and that I will go above and beyond my own and other's expectations.

## About me
I'm Kasper, but everyone calls me by my middle name Timm. I live in Copenhagen, Denmark and the timezone there is UTC+2. I work somewhere between 9-22, not all the time of course. This wide range is just to say that I'm flexible with my schedule.
Something that I can manage albeit with less flexibility, however, is my summer commitments. 

### Commitments
I have a portfolio exam sometime in June, no later than the 21st. I won't know the exact date for sure until sometime in late May or early June. Having said that, the exam revolves around projects I have worked on through this semester so that much preparation is not needed. The next semester will be starting on 26th August, but the project is scheduled such that it won't overlap.

### Why me?
I'm fluent in English. You will not have a problem communicating with me. On a related note I'm also a great writer. I have written a novel which I'm working on getting published. Being interested in writing I know full well what clear and succinct sentences can bring to a persons understanding of a problem.
I know when to stop and call it a day. You won't see me coding the night away and burn out two weeks into the project. Burning out won't be a problem either as I'm excited about coming up with a new solution.

To elaborate on why this problem excites me I will tell a little story. Recently I was at a conference where Don Melton, the person who started the Safari (and WebKit) project at Apple, spoke. Don told us how his team made Safari fast. To see him talking about how early Safari builds were even slower than Mac IE and how they changed course to become the fastest browser was incredibly inspiring. Right now I'm feeling that same kind of inspiration as I think of this project. The variety it entails. I get to both update existing code while getting a hand at managing new complexity. The new territory I get to tread. A clear part of what excites me is to do something I haven't done before, not exactly like this anyway.

So I don't fear the complications that this task will bring, I welcome them. They give me a chance to show my worth. To show that I can do this. I'm the path to better sanitization in Rails.
=======
gsoc-application
================

My project proposal for Google Summer of Code 2013.
>>>>>>> 4eb64fa3acc69d0e95d7c4df69726aca4de90714
