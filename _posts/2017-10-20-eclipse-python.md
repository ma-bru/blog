---
title:  "(Somewhat) usable Eclipse installation for Python development"
categories:
  - Howto
tags:
 - IDE
 - Eclipse
 - Development
 - Python
 - PyDev
---

I mainly do C++ and Python development.
For C++ I'm really happy with QtCreator.
Personally I barely use the Qt framework and despite the name it does an awesome job for any kind of C++ development.
It's lightweight, has the best CMake integration I've ever seen (It's 2017, can we please get rid of IDE specific build systems?).
Plus some nice features like an integrated Clang based syntax checker.

For Python, I'm not that lucky.
When googling around you basically find two options for full featured IDEs: PyDev and PyCharm.
Both of them are painfully slow, Java based, memory hogs.
Many years ago I had to use Eclipse for a while and decided I have enough of it - there used to be a whole website dedicated to people posting about how much it sucks.
So I settled with PyCharm.

Apart from the sluggish responses, Pycharm is OK.
However some of the advanced features need a commercial licence.
So in a moment of weakness, I decided to give Eclipse another chance.
Surprisingly, turns out it's not all that bad anymore.
However the default installation options are.

The standard way to install Eclipse is to go to their [website](http://eclipse.org).
Follow the download button that brings you to another download button, which downloads a
weird Windows like installer - Since when is extracting an archive not good enough anymore?
When you run the installer it gives you a few choices of what flavour of Eclipse you
want to install.
All of them are bloated and none of them is fitting for Python development.

I decided to give the "Eclipse IDE for Java Developers" a try (it's the only one that has the word essential in it's description).
After installation, which asked me if I trust some certificates (You're the official installer. You should know!), it finishes installation.
As expected, after starting it, it feels slow and bloated.
A look at the installed plugins shows the following:

![Default Eclipse]({{ site.url }}{{ site.baseurl }}/assets/images/eclipse/eclipse_java.png)

That's a lot of stuff I don't want and didn't ask for (At least the installer didn't give me any choice).
I tried to remove everything I don't need - I'm looking at you, [MyLyn](http://paranoid-engineering.blogspot.de/2008/07/what-is-eclipse-mylyn-anyway.html) - which felt like cleaning a Windows system from pre-installed bloatware, but somehow ended up removing too much and eclipse wouldn't start anymore.
Since I believe in [KISS](wiki.archlinux.org/index.php/arch_terminology#KISS) (funny to mention KISS in a post about eclipse...) I decided it's the wrong way to start with something already broken and then try to fix it.

So here's the sane way to install Eclipse for Python development:

1. Go to <http://archive.eclipse.org/eclipse/downloads/>
2. Download the Platform Runtime Binary for the version you want
3. Unzip
4. Start and install PyDev as described in http://www.pydev.org/manual_101_install.html 
5. Make sure not to install the PyDev MyLyn plugins unless you really want them.
6. Enjoy your clean and fast (well, as clean and fast as possible...) experience:

![Minimal Eclipse]({{ site.url }}{{ site.baseurl }}/assets/images/eclipse/pydev.png)

The only problem I had, was that after importing a Python project from filesystem Eclipse didn't automatically start the PyDev perspective and I couldn't find the run and debug buttons.
But manually switching the perspective worked just fine.

Now go ahead and install the plugins you really want and need.
