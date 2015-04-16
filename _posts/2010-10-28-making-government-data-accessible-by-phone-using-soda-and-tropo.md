---
title: Making government data accessible by phone using SODA and Tropo
layout: post
---

__Update:__ I've updated the script to handle text messaging as well. Details [below](#textmessaging)

In an age of smart phones, iPads, and the mobile web, we often forget that a huge portion of the population doesn't even have access to the Internet. How do we make sure that no one is denied access to the excellent advances we're making in open government data? One great option is to make that information accessible via a technology we've had for the last 134 years - the telephone.

[![Phone](http://farm1.static.flickr.com/31/64027565_79b890c8c4.jpg)](http://www.flickr.com/photos/splorp/64027565/sizes/m/in/photostream/)

~

Earlier this week I was asked to speak at a [King County Open Data Workshop](http://www.kingcounty.gov/exec/news/release/2010/October/25OpenData2.aspx) and talk to some of Seattle's civic developers about what they could build using the Socrata Open Data API and data published by King County on their [DataKC.org](http://www.datakc.org) Socrata-powered datasite.

Stretched for time, and wanting to build something compelling, I thought about
what "itches" I'd had in the past that could have been scratched with an app
built using the SODA API. After finding King County's [What do I do with...?](http://www.datakc.org/Government/What-do-I-do-with-Recycling-options-in-King-County/zqwi-c5q3) dataset of recycling options in my area, I remembered the first Christmas I hosted in Seattle. Finding myself in the "Evergreen State", and never having had a "real tree" before, I went down to the local Boy Scout tree sale and bought my first ever live Christmas tree. Not knowing what to do with it, I held onto that tree until almost February, until it was good and brown and crispy. __What if King County had an automated hotline I could have called in order to find out where I could take my tree for composting?__

And thus, an hour and 100 heavily-commented lines later, the [King County Christmas Tree
Disposal Line](http://christmas-tree-disposal.heroku.com/) was born:

[![King County Christmas Tree Disposal Line](/img/posts/2010-10-28-kc_christmas_tree_line.png)](http://christmas-tree-disposal.heroku.com/)

Built using the great tools from our friends at [Tropo](http://www.tropo.com),
the app is very simple. First, we tell Tropo to answer the phone, greet our
user, and accept a five-digit zip code, either entered via the keypad or speech
to text:

<script src="http://gist.github.com/652184.js?file=gistfile1.rb">// Placeholder to keep Maraku from breaking the script tag.</script>

The `lookup_facilities` function then builds a filtered query using the SODA API to
request matching facilities:

<script src="http://gist.github.com/652186.js?file=gistfile1.rb">// Placeholder to keep Maraku from breaking the script tag.</script>

That's really about it. The [Tropo Scripting API](https://www.tropo.com/docs/scripting/) needs a URL from which to load the script to run, so I created a simple [Rack](http://rack.rubyforge.org/) app hosted on [Heroku](http://www.heroku.com) that simply hosts the [christmas.rb](http://christmas-tree-disposal.heroku.com/rb/christmas.rb) file along with a [homepage with a cute little tree](http://christmas-tree-disposal.heroku.com/). If you want to check it out or fork the code for yourself, I've pushed the whole shebang up to [Github](http://github.com/socrata/christmas-tree-disposal-line).

If you want to give it a try, simply call `(206) 397-0769` and enter a Seattle-area zip code, like `98133`.  Tropo also supports SMS, IM protocols, and even Twitter, so there is much more left to explore. If you build something cool, make sure you [submit your app](/submit-your-app/) and leave a comment below. Good luck!

__Update:__ I've updated the Tropo script to handle requests via text message as well. Besides some general refactoring, the key was checking the Tropo session's `initialText` value to see if the sender sent a text message to start with. The rest of the details can be found in [my diff](https://github.com/socrata/christmas-tree-disposal-line/commit/88d9bb4584f00e2fe828b754f79ada1d55a058b1):

<script src="https://gist.github.com/671812.js?file=gistfile1.rb">// Placeholder to keep Maraku from breaking the script tag.</script>

_Photo from [slorp](http://www.flickr.com/photos/splorp/)'s CC-licensed Flickr photostream_