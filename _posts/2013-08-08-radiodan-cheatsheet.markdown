---
layout: post
title:  "Radiodan cheatsheet"
date:   2013-08-08 09:41:34
author:
  name: Libby Miller
  github: libbymiller
---

I've been working with Radiodan to make a radio that plays whatever is most popular on BBC radio. Dan's been
helping me understand how best to use the Radiodan features. Here's the results of our initial discussions.

## Radiodan

Radiodan is a Ruby library containing four main elements:

* player lib/radiodan/
* builder lib/radiodan/middleware
* event binding
* logging

<br />
## Player

This is currently a wrapper ('adapter') for the MPD player so you can only create an MPD player instance, but
others could be made (i.e. an iTunes wrapper) as long as they support play, pause, and add to playlist: it's a
wrapper for the software that actually plays the audio. To create a player, see Builder below.

The main part of Player is Playlist, which is what you tell the player about to tell it what to play. The Playlist
consists of a state [:play, :stop, :pause], a mode [:sequential, :resume, :random], repeat (default false), an
array of tracks, which themselves contain a file / url, a position (default 0), seek (default 0) and volume
(default 100%).

{% highlight ruby %}
radio4 = Radiodan::Playlist.new(tracks: url)
{% endhighlight %}

A Playlist is also sent back by the Player at regular intervals (currently every 0.5 sec). Radiodan checks the
playlist it sent against the playlist it gets back, and changes the state of the player if they are inconsistent.
So for example if state from MPD is :stop when the Playlist sent to it was :play, then radiodan sends a play
command to MPD.

Example playlist returned:

{% highlight ruby %}
<Radiodan::Playlist:0x1fb95b8 @state=:play, @mode=:sequential, @repeat=false, @tracks=
 [#<Radiodan::Track:0x1fb2808
  #@attributes=
   {"file"=>"http://....", "Name"=>"BBC Radio 4", "Pos"=>"0", "Id"=>"2"}
  >],
@position=0,
@seek=13.073,
@volume=80>
{% endhighlight %}

To change the channel, you simply send it a new Playlist. Similarly for MP3s. MP3 will typically contain more
metadata than streams in general. To access items of metadata from the Playlist, use e.g. player.playlist["Name"].

<br />
##Builder

Builder is about creating and running ad-hoc components for the system, the 'middleware'. To use it you create a class of your own with a 'call' function. This function must be wrapped in a event machine block or it will block. You can see some existing examples of middleware in the radiodan Gem in lib/radiodan/middleware/ - e.g. panic.rb. Radiodan loops through all of these it knows about in order, calling the call function and passing it an instance of Player.

Here's an example of how to start Radiodan with a builder, and you can see the logger, adapter for MPD, the initial playlist and then two pieces of middleware, touch_file and panic.

{% highlight ruby %}
radio = Radiodan.new do |builder|
    builder.log      STDOUT
    builder.adapter  :MPD, :host => 'localhost', :port => 6600
    builder.playlist radio4
    builder.use      :touch_file, :dir => File.join(root, 'tmp')
    builder.use      :panic, :duration => 5, :playlist => radio1
end
radio.start
{% endhighlight %}

<br />
## Event Binding

Any part of the system can register an event with a key and a block to call when the event is triggered, like this:

{% highlight ruby %}
@player.register_event :panic do
      panic!
end
{% endhighlight %}

To trigger an event, do this with the key used earlier, and any value to pass to the block:

{% highlight ruby %}
@player.trigger_event :panic
{% endhighlight %}

[Note: We are considering adding an :all event which captures all events and which can be passed to the web interface via Faye.]

<br />
## Logger

Logging is fairly self-explanatory. To create a logger, pass it to the builder as above. To use it, do this:

{% highlight ruby %}
logger.debug "panicing!"
{% endhighlight %}

You can see the complete example in [radiodan_example](https://github.com/radiodan/radiodan_example/blob/master/bin/start)



