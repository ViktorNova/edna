edna
====

Simple and rad mp3 playlist server in Python. I did not write this, it is a brilliant project by Greg Stein. This is a GitHub clone of the original project at Sourceforge http://edna.sourceforge.net/

Here is the original readme by Greg Stein:

##edna -- an MP3 server
edna is a quick hack that I put together, based on ideas from my friend, Geoff Elliott. He had written a program named ampRadio that operates much like edna -- serving up HTML pages with links to MP3 files, and then serving out those MP3s.

###What is edna?

edna allows you to access your MP3 collection from any networked computer. This software streams your MP3s via HTTP to any MP3 player that supports playing off a remote connection (e.g. Winamp, FreeAmp, Sonique, XMMS, WMP).

edna supports:

   - Browsing your music collection from a remote computer.
   - URL support to allow people to stream specific songs.
   - Automatic playlist construction for entire directories of songs, including a "shuffle" ability.
   - The merging of multiple music collections while keeping the files on the remote computer.

While any silly web server can do this (serve up MP3s), there are two cool features about edna:
 
   - The pages are dynamically constructed, adjusting to directory structure and the files in those directories. This is much nicer than using simple directory indexing. While the dynamic file list could be done with various CGI or PHP-like tools, the dynamic directories would be a lot harder.
   - This is the coolest part... Rather than directly serving up an MP3, the software serves up a playlist. This gets passed to your player (e.g. WinAmp) which turns around with an HTTP request to stream the MP3. I must give credit to Geoff for this one :-)

When constructing a page for a directory, edna will list all subdirectories, MP3 song files (.mp3 extensions), playlists (.m3u extensions), certain other types of music and video files (such as .wav), and images. All other files will be ignored.

edna can automatically create play lists for individual directories of songs, and all directories recursively. These lists can also be shuffled (by edna, rather than your player).

Your MP3 player must be able to recognize .m3u files, and your browser must know to pass .m3u files to your player. Your player must be capable of handling URLs within a playlist. I've tested this with WinAmp, which definitely meets these needs.

###Where to get it?

The latest edna is currently labeled as version 0.6 because there are still a few more features that I would like to add. It is very stable and can be used (now) without a problem.

edna is licensed under the GPL. It is a small Python script. At the moment, it is about 1000 lines (version 0.1 was only 250!). You can get the source from the distribution.

Please feel free to sign up on the edna mailing list. We discuss new features, installation and configuration issues, and current development.

###Installation and Use

The server should work for any platform. I've tested it on Linux and Windows. I've been using Internet Explorer and WinAmp (on Windows) to navigate the pages and play the files.

Using edna is boringly simple. Make sure you have (at least) Python 1.5.2 installed on your system. Edit the edna.conf file with your setup. This is simple to do, as all you need to tell it is:

   - what port to run on
   - the directories for your MP3 files
   - optionally, how to log requests
   
Then, simply run edna.py. This can be done using:

````
% python edna.py
````

It will then go into an infinite loop, serving up pages and files. Hit ctrl-C to stop it.

###Running as an NT Service

Starting with edna 0.4, it is now possible to use edna as an NT Service (thanks to Bill Tutt). You will need the most recent Python/Win32 extensions, and have NT 4.0 or Windows 2000 for this code to work.

The NT Service scripts are in the ntsvc subdirectory of the distribution. Change to that directory to install or remove the edna service.

####Installation
````
python ednaNTSvc.py -c C:/path/to/edna.conf --startup auto install
````

####Removal
````
python ednaNTSvc.py remove
````

####Usage string output from ednaNTSvc.py
````
Usage: 'ednaNTSvc.py [options] install|update|remove|start [...]|stop|restart [...]|debug [...]' 
Options for 'install' and 'update' commands only:
 --username domain\username : The Username the service is to run under
 --password password : The password for the username
 --startup [manual|auto|disabled] : How the service starts, default = manual
````

####Starting edna from sysvinit scripts

Check the included makefile and adjust the installation paths. The script will run edna on startup.

###Modifications

If you don't like the HTML it generates, then look at template files in the templates subdirectory. It should be quite apparent how to make your changes.

I'm quite willing to accept patches or other fixes. Just email them to the edna mailing list at edna@lyra.org.

Thanks

I'd like to thank the following people for their contributions to the edna server:

Matteo Bertini: quick navigation links
Steve Davis: init scripts
Dieter Deyke: image display and playlist rewriting
Jeffrey Griffith: server statistics, edna client, web design
Christophe Kalt: Unicode pages, ZIP support, fixes, releases
Stephen Kennedy: skipping the top-level directory, skip ".foo" directories
Erno Kuusela: access control
Andy Lowe: recursive play lists
"Lord Satan": Python 1.6 and later compatibility
PK Shiu: the "is new" feature
Shaw Terwilliger: support for serving icons, text files
Bill Tutt: NT Service ability, shuffle play, multiple file extensions (and more)
"vivake": XML output and extended MP3 info
Joe Ward: UI improvements
Dave Williams: watch out for single-letter directories
Kristian Kvilekval: bug fixes, page caching, releases, unix daemon mode

-Greg Stein
