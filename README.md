sonostream - tell Sonos speaker to enqueue MP3s from URL
========================================================

The `sonostream` program commands a local Sonos speaker to enqueue MP3s 
from a URL.

Getting Started
---------------

Install required gems via Bundler:

    $ bundle install

Or, install prequisites manually:

    $ gem install httpclient nokogiri sonos

Play a song on the first local Sonos speaker:

    $ sonostream http://example.com/music/song.mp3

Description
-----------

The `sonostream` program commands a local Sonos speaker to enqueue MP3s 
from a URL from the Unix command line. It also provides simple access to 
volume, play, and pause functionality from the command line. Sonos 
integration is provided via the `sonos` RubyGem, which also provides a 
`sonos` command line program that lets you queue a single URL with a 
command like the following:

    $ sonos speaker 'Living Room' add_to_queue http://example.com/music/song.mp3

The advantage of `sonostream` is that you can provide it a link to an 
HTML page, and it will recursively crawl it for any links that return a 
Content-Type of `audio/mpeg`:

    $ sonostream -s 'Living Room' http://example.com/music/index.html

### Usage

To display help text and exit:

    $ sonostream -h

To enqueue music from a URL (either to a single MP3, or to an HTML page 
that includes links to MP3s, and possibly other HTML subpages that link 
to MP3s):

    $ sonostream http://example.com/music/index.html

To choose which speaker to use, pass a speaker name:

    $ sonostream -s 'Bedroom 2' http://example.com/music/index.html

The default is to just choose the first speaker that the `sonos` gem 
returns (this is especially convenient if you have only one speaker, or 
the first speaker returned is the one you use most often).

To do a dry run (just print what would be enqueued, showing what MP3 
links were recursively crawled from an index page):

    $ sonostream -n http://example.com/music/index.html

To set the volume (and exit, if no URL is provided; or load music from a 
URL, if a URL is provided):

    $ sonostream -v 50

To play or pause music:

    $ sonostream play

    $ sonostream pause

Note that the above are pretty much equivalent to the following commands:

    $ sonos speaker 'Living Room' volume= 50

    $ sonos speaker 'Living Room' play

    $ sonos speaker 'Living Room' pause

They are just provided as syntactic sugar so you can use the same style 
command line invocation to enqueue, set volume, play, and pause music.

One of a volume setting, `play` or `pause` command, or a URL are required.

### See Also

The source code for this program is on GitHub:

* https://github.com/andrewgho/sonostream

This program is just a simple command line wrapper to the `sonos` 
RubyGem, which is also on GitHub:

* https://github.com/soffes/sonos

The original, pioneering Sonos API and command line interface are the 
the SoCo Python library:

* http://python-soco.com/

"Sonos" is a registered trademark of Sonos, Inc.

Author
------

Andrew Ho (<andrew@zeuscat.com>)

License
-------

    Copyright (c) 2014, Andrew Ho.
    All rights reserved.
    
    Redistribution and use in source and binary forms, with or without
    modification, are permitted provided that the following conditions
    are met:
    
    Redistributions of source code must retain the above copyright notice,
    this list of conditions and the following disclaimer.
    
    Redistributions in binary form must reproduce the above copyright
    notice, this list of conditions and the following disclaimer in the
    documentation and/or other materials provided with the distribution.
    
    Neither the name of the author nor the names of its contributors may
    be used to endorse or promote products derived from this software
    without specific prior written permission.
    
    THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
    "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
    LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR
    A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT
    HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
    SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT
    LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE,
    DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY
    THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
    (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
    OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
