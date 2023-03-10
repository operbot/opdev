README
######


**NAME**


**OPB** - object programming bot


**SYNOPSIS**

::

 opb [-c|-d|-h]
 opb <cmd> [key=value] [key==value]


**DESCRIPTION**


**OPB** is a bot, intended to be programmable, with a client program to
develop modules on and a systemd version with code included to run a 24/7
presence in a channel.

**OPB** uses object programming, where the methods are seperated
out into functions that use the object as the first argument of that funcion.
This gives base class definitions a clean namespace to inherit from and to load
json data into the object's __dict__. A clean namespace prevents a json loaded
attribute to overwrite any methods.

**OPB** provides object persistence, an event handler and some basic code to
load modules that can provide additional commands.

**OPB** has some functionality, mostly feeding RSS feeds into a irc
channel. It can do some logging of txt and take note of things todo.


**INSTALL**

::

 $ sudo python3 -m pip install opb --upgrade --force-reinstall


**CONFIGURATION**


configuration is done by calling the ``cfg`` command of ``opb``
 

**irc**


::

 $ opb cfg server=<server> channel=<channel> nick=<nick>

 (*) default channel/server is #opb on localhost


**sasl**

::

 $ opb pwd <nickservnick> <nickservpass>
 $ opb cfg password=<outputfrompwd>


**users**


as default the user's userhost is not checked when a user types a command in a
channel. To disable userhost checking disable users with the ``cfg``
command::

 $ opb cfg users=False


To add a user to the bot use the met command::

 $ opb met <userhost>


to delete a user use the del command with a substring of the userhost::


 $ opb del <substring>


**rss**

::

 $ opb rss <url>


**RUNNING**


this part shows how to run ``opb``.


**cli**


without any arguments ``opb`` doesn't respond, add arguments to have
``opb`` execute a command::

 $ opb
 $


the ``cmd`` command shows you a list of available commands::

 $ opb cmd
 $ cfg,cmd,dlt,dpl,flt,fnd,ftc,met,krn,mre,nme,pwd,rem,rss,thr,upt


**console**


use the -c option to start the bot as a console::

 $ opb -c
 OPB started at Fri Jan 6 01:49:58 2023
 > cmd
 cmd,dlt,dpl,flt,ftc,krn,log,met,mre,nme,pwd,rem,rss,thr,upt
 >


running the bot in the background is done with the -d option::


 $ opb -d


**COMMANDS**


here is a short description of the commands::


 cfg - show the irc configuration, also edits the config
 cmd - show all commands
 dlt - remove a user
 dne - flag todo as done
 dpl - set display items for a rss feed
 flt - show a list of bot registered to the bus
 fnd - allow you to display objects on the datastore, read-only json files on disk 
 ftc - run a rss feed fetching batch
 log - log some text
 met - add a users with there irc userhost
 mre - displays cached output, channel wise.
 nme - set name of a rss feed
 pwd - combine a nickserv name/password into a sasl password
 rem - remove a rss feed by matching is to its url
 rss - add a feed to fetch, fetcher runs every 5 minutes
 thr - show the running threads
 tdo - adds a todo item, no options returns list of todo's
 upt - show uptime


**PROGRAMMING**


The ``operbot`` package provides an Object class, that mimics a dict while using
attribute access and provides a save/load to/from json files on disk.
Objects can be searched with database functions and uses read-only files
to improve persistence and a type in filename for reconstruction. Methods are
factored out into functions to have a clean namespace to read JSON data into.

basic usage is this::

 >>> from operbot import Object
 >>> o = Object()
 >>> o.key = "value"
 >>> o.key
 >>> 'value'

Objects try to mimic a dictionary while trying to be an object with normal
attribute access as well. hidden methods are provided, the methods are
factored out into functions like get, items, keys, register, set, update
and values.

load/save from/to disk::

 >>> from operbot import Object, load, save
 >>> o = Object()
 >>> o.key = "value"
 >>> p = save(o)
 >>> obj = Object()
 >>> load(obj, p)
 >>> obj.key
 >>> 'value'

**MISSION**


OPB is a contribution back to society, placed in the Public Domain.


**AUTHOR**


| B.H.J. Thate - operbot100@gmail.com
|

**COPYRIGHT**


``opb`` is placed in the Public Domain.
