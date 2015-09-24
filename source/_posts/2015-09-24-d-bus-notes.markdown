---
layout: post
title: "D-Bus Notes"
date: 2015-09-24 01:52:55 +0200
comments: true
categories: 
---

## Abstract

D-Bus is a message bus which can be used for inter process communication primarily designed for Unix like systems. There are two types of message buses that are available. The first being the "system daemon" which is typically used for broadcasting system events such as detecting new hardware. The second type being the "user session daemon" which is typically restricted for user sessions.

<!--more-->

#### D-Bus

* `dbus-daemon` - controlled by `/etc/init.d/dbus-1`
	* `system` (starts by default)
	* per user - `session` 
* To start the user session daemon
  * eval `dbus-launch --auto-syntax`
	  * starts message bus 
	  
#### D-Bus Utilities

##### Structure
* bus name (has '.' seperators)
	* objects identified by object path (has '/' separators)
		* methods (for ingress) (has '.' separators)
		* signals (for egress)

##### To find the dbus addresses

```
$ netstat -an | grep @/tmp/dbus- | awk '{ print $NF }' | sort | uniq
@/tmp/dbus-C5P7XVCXyF

$ dbus-monitor --address unix:abstract=/tmp/dbus-y3RN1QljDz
```

#### Resources

* [Tutorial: Interprocess Communication with D-Bus and Python](http://www.documentroot.net/en/linux/python-dbus-tutorial)
* [An actually decent Python DBus Tutorial](http://excid3.com/blog/an-actually-decent-python-dbus-tutorial/)
* [How to write dbus service for Linux (in Python)](https://coelhorjc.wordpress.com/2014/12/09/howto-write-dbus-service-for-linux-in-python/)
