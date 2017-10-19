---
title:  "(Somewhat) usable Eclipse installation"
categories:
  - Howto
tags:
 - IDE
 - Eclipse
 - Development
 - Python
---

I mainly do C++ and Python development.
For C++ I'm really happy with QtCreator.
It's lightweight, has the best CMake integration I've ever seen.
Plus some nice features like an integrated clang based syntax checker.
For Python I'm not that lucky.
The two IDEs I tried are both Java based, painfully slow memory hogs: Pydev (Eclipse) and PyCharm.

Pycharm is ok. However some of the advanced features need a commercial licence.
So I decided to give Eclipse another chance.
Turns out it's not all that bad anymore.
However the default installation options are.

The normal way to install Eclipse is to go to their [website](http://eclipse.org).
Follow the download button that brings you to another download button, which downloads a
weird Windows like (slow and dumb) installer.
When you run the installer it gives you a few choices of what flavour of Eclipse you
want to install.
None of them fitting for Python develoment.
I decided to give the "Eclipse IDE for Java Developers" a try (it's the only one that has the word essential in it's descriptions).
After installation, which asked me if I trust some certificates, which I neither know, norwant to bother researching, it finishes installation.

```
Normal: got to eclipse.org follow download link weird ass installer (nearly as slow as windows)
Choose from preconfigured options (None of them fits python development -> smalles evil java)
Questions about if I trust certificates... No idea... 
```


```
Download from http://archive.eclipse.org/eclipse/downloads/ (Platform Runtime Binary)

unzip

Install PyDev as in http://www.pydev.org/manual_101_install.html (Skip Mylyn unless you know what it does and need it.)

Open Python perspective for run button

Install other plugins as needed (git,svn)
```
