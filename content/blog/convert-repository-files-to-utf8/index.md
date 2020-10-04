---
title: "Convert repository files to UTF8"
date: 2019-03-08
description: import from previous blog.
---
I recently had to convert a repository from Windows-1252 to UTF-8. The encoding was causing our web pages not to render characters outside of the 1252 set incorrectly. So, I wrote a script to do this!

What it does: It accepts a path `-Path` and recursively searches for all files under that path. It then checks to see if that file is ignored in the .gitignore. If not, it moves on to checking if it's ascii. If it passes that test, it will grab the contents and write them as UTF-8.

**EDIT:** I now filter for designer and resx files. For my purpose, these couldn't get converted because of some special characters.

Feel free to use and offer any feedback about it.

## Parameters

### -Path 

Directory to start recursive search. This directory is assumed valid and a git repository.

### -ShowIgnored 

A switch to output reasons why a file was skipped.

Here's the gist:

`gist:mikeruhl/0340431354810bc6f45a18e6b69a5e87`


