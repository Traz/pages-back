---
layout: post
title: "Shells  (Mingw / Msys) : DevKit Git"
tags: ['shell','vim']
published: true
---



### Shells versions


Once you'd installed the basics, you've got 2 shells : one on _/devkit_ and one on _/git_

It may cause some conflit (differents version, different tools ...). So, i choose to drop the Git shell from th ePATH environment variable (_c:/dev/git/bin_) but keep the path for git command (_c:/dev/git/cmd_) : you can run the both shell (the git one can have autocompletion on git command, plus a nice PS1), but the Devkit shell is the default one.

### Shell personnalisation

On Windows you've got a standard home path, but it's too easy to becom a piece of trash with other win programs ...

So i'd set up a new home directory for all bash shell : _c:/dev/home_, and puts some modification on profile file from the both shell (_c:/dev/devkit/etc/profile_ and _c:/dev/git/etc/profile_)

{% highlight sh %}
HOME="c:/dev/home"
HISTFILE=$HOME/.bash_history
HOME="$(cd "$HOME" ; pwd)"
{% endhighlight %}

Chek also _/etc/fstab_ for some personnal mount.


### VI / VIM / GVIM 

VIM is usefull with quick simple edit, but is not bundle with DevKit (only whith Git). So go to the [VIM web site](http://www.vim.org), download and install it (as usual, in c:/dev/...). It put some .BAT file directly under c:/windows ... but thoses aren't accessible when you run your shell (only under DOS prompt). So, just add _c:/dev/vim/vim73_ to your PATH variable, and check it :

{% highlight sh %}
sh -l -i
vim
{% endhighlight %}
