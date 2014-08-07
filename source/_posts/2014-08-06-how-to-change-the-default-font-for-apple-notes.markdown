---
layout: post
title: "How to change the default font for Apple Notes?"
date: 2014-08-06 14:44:26 -0700
comments: true
categories: 
- Tips
- Mac OS X
---
##Introduction##

When need of a temporary textpad, I do one of the following:

`vi /dev/null`

or open the following browser bookmark aptly called "Notebook" from my bookmark bar:

`data:text/html, <html contenteditable>`

Go ahead, try to copy and paste the above snippet into the browser location and go. Presto, a basic textpad is now available. But, if I need to store notes in a lightweight application - Apple Notes fits the bill for me.

Apple Notes is nice as it's a quick textpad. I don't have to worry about where the file needs to be stored. I can search through all of my notes to bring up the interesting note. I can pull it up on my iPhone. It's a temporary notebook which contains rough notes. Once, these notes are processed, I typically dump them in to Evernote.

But, the reason why we are here is because I needed to change the default font of my Apple Notes. I wanted a monospace font so that I can clip log lines / code snippets into there.

<!--more-->

##Instructions##

1\. Open the following plist file:	

```
sudo vi /Applications/Notes.app/Contents/Resources/en.lproj/DefaultFonts.plist
```

2\. Add the following xml node to the array. Of course, change the string value to your favorite font.
```
    <dict>
        <key>FontName</key>
        <string>Monaco</string>
        <key>Size</key>
        <integer>12</integer>
    </dict>
```

3\. Restart Apple Notes.

4\. From the menu, I selected Monaco as my default font:

```
Font > Default Font > Monaco
```