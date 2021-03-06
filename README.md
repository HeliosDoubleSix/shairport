Shairport v0.03
==============
James Laird <jhl@mafipulation.org>
April 11, 2011

What it is
----------
This program emulates an Airport Express for the purpose of streaming music from iTunes and compatible iPods. It implements a server for the Apple RAOP protocol.

It probably supports multiple simultaneous streams, if your audio output chain (as detected by libao) does so.

Setup
-----
    $ make
    $ perl -MCPAN -e 'install Crypt::OpenSSL::RSA'`
    $ sudo apt-get install libssl-dev libcrypt-openssl-rsa-perl libportaudio-dev libhttp-request-ascgi-perl`

How to use it
-------------
1. Make sure avahi-daemon is running and the prerequisites are installed (see INSTALL).
2. Edit shairport.pl with your favourite text editor to set the access point name and/or password, if desired.
3. `perl shairport.pl`

The triangle-in-rectangle Airtunes logo will appear in the iTunes status bar of any machine on the network, or on iPod play controls screen. Choose your access point name to start streaming to the Shairport instance.

Thanks
------
Big thanks to David Hammerton for releasing an ALAC decoder, which is reproduced here in full.
Thanks to everyone who has worked to reverse engineer the RAOP protocol - after finding the keys, everything else was pretty much trivial.
Thanks also to Apple for obfuscating the private key in the ROM image, using a scheme that made the deobfuscation code itself stand out like a flare.
Thanks to Ten Thousand Free Men and their Families for having a computer and stuff.
Thanks to wtbw.

Changelog
---------
* 0.01  April 5, 2011
    * initial release
* 0.02  April 11, 2011
    * bugfix: libao compatibility
* 0.03  April 11, 2011
    * bugfix: ipv6 didn't work -
	* IO::Socket::INET6 is required too


How to compile and install on Mac OSX 10.6
------
prerequisite: install XCode, install homebrew (https://github.com/mxcl/homebrew)

    $ brew install pkg-config libao
    $ make
    $ perl -MCPAN -e 'install Crypt::OpenSSL::RSA'
    $ perl -MCPAN -e 'install IO::Socket::INET6'
    $ perl shairport.pl

OSX 10.5 only bundles perl 5.8, which won't work with shairport. After getting a update
here (http://www.perl.org/get.html), it worked.

Available launch options for 
------
    $ shairport.pl --apname=My Name --password=secret
    

How to run as a daemon on Mac OSX 10.6
------
    $ cp hairtunes shairport.pl /usr/local/bin
    $ vi /usr/local/bin/shairport.pl # change the path of hairtunes from ./hairtunes to /usr/local/bin/hairtunes
    $ mkdir -p ~/Library/LaunchAgents
    $ cp org.mafipulation.shairport.plist ~/Library/LaunchAgents/ # you may want to change AP name in this file
    $ launchctl load -w ~/Library/LaunchAgents/org.mafipulation.shairport.plist
    $ launchctl unload -w ~/Library/LaunchAgents/org.mafipulation.shairport.plist # to remove
