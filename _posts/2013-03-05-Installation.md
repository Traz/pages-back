---
layout: post
title: "Installation from scratch : Ruby 2.0.0 under Windows"
tags: ['windows','ruby 2','rails 4','sqlite3','ansicon','console2','conemu','git']
published: true
---

First set up some tools. Console2 was for longtime my shell manager, but i've discovered recently ConEmu whitch has more pretty options.

### Console2 2.00b147
Download [Console2](http://sourceforge.net/projects/console/). You'll need to install ANSICON for managing colors (ConEmu do not need ANSICON), see below.

### Configure PATH for NTLM Proxy
In case you're under some NTLM Proxy, you'll need to set some variables :

{% highlight bat %}
set HTTP_PROXY=http://proxy.adress:proxy_port
set HTTP_PROXY_USER=userxxx
set HTTP_PROXY_PASS=passwordxxxx
{% endhighlight %}

I used to centralize all my install into one directory _c:/dev_ and puts all single .exe or .dll under _c:/dev/bin_ and put those in PATH (ie : for SQLite3 dll and exe, LAME library, ffmpeg, ...).

### Ansicon 1.60
For nice console output : [Ansicon](https://github.com/adoxa/ansicon/downloads). Download it and put the file under _c:/dev/bin_.
You can register it for automatic launch in each console : 

{% highlight bat %}
anssicon -i
{% endhighlight %}

ConEmu doesn't use Ansicon.

### Ruby 2.0
Download and install Ruby 2.0 : [RubyInstaller for Windows](http://rubyinstaller.org/) (under _c:/ruby200_). Check it : 

{% highlight bat %}
ruby -v
{% endhighlight %}

### DevKit 4.7.2

Download also on RubyInstaller for Windows the right DevKit (version 4.7.2, 32 or 64 bits) and install it under _c:/dev/devkit_.
Check the PATH :

{% highlight bat %} 
echo PATH
>>... c:/dev/devkit/bin
{% endhighlight %}

And test the first unix commands : 

{% highlight bash %}
sh --login
ls -l
exit
{% endhighlight %}

The home directory is _c:/dev/devkit/home/(user)_. I've created a _.profile_ file here for configuring some alias : 
{% highlight bash %}
alias ls="ls --color"
alias ll='ls -l'
alias w='which'
alias e='exit'
alias st="C:/'Program Files'/'Sublime Text 2'/sublime_text.exe"
{% endhighlight %}

### SublimeText2
Download and install it [SublimeText2](http://www.sublimetext.com/2).

### Configure ST2
In menu preferences / Setting - Default, some modifications

    "font_face": "Consolas",
    "font_size": 10.0,
    "tab_size": 2,
    "translate_tabs_to_spaces": true,
    "folder_exclude_patterns": [".svn",".keep", ".gitignore", ".git", ".hg", "CVS"]> 
    "file_exclude_patterns": ["*.pyc", "*.pyo", "*.exe", "*.dll", "*.obj","*.o", "*.a", "*.lib", "*.so", "*.dylib", "*.ncb", "*.sdf", "*.suo", "*.pdb", "*.idb", ".DS_Store", "*.class", "*.psd", "*.db"],

### Install the Package Manager ST2
SublimeText has many usefull plugins, and a good package manager. Follow the instructions under [Sublime package control](http://wbond.net/sublime_packages/package_control) for the installation.
If you're under a proxy, change your settings : Preferences / Package setting / Package control / Setting - Default :

    "http_proxy": "http://proxy.name:port",
    "proxy_username": "",
    "proxy_password": ""

### Install some plugins for ST2
Check the community site for the packages : [community package control](http://wbond.net/sublime_packages/community), and try them :)


For SublimeTODO package, change the settings (menu preferences / setting user), ie :

    "todo":
    {
      "case_sensitive": true,
      "file_exclude_patterns":
      [
        "*.css",
        "*.po",
        "*.mo"
      ],
      "folder_exclude_patterns":
      [
        "static",
        "vendor",
        "tmp"
      ],
      "patterns":
      {
        "BUG": "BUG[\\s]*?:+(?P<bug>.*)$",
        "TEST": "TEST[\\s]*?:+(?P<test>.*)$"
      },
      "result_title": "TODO Results list"
    }

### GIT
Some good reading link (fr/eng) for starting : 

- <http://rogerdudler.github.com/git-guide/index.fr.html>
- <http://www.siteduzero.com/tutoriel-3-254198-gerez-vos-codes-source-avec-git.html>
- <http://www.pierreschambacher.com/blog/git-in-a-nutshell/>
- <http://git-scm.com/book>

In first, install [GIT for Windows](http://git-scm.com/downloads) under _c:/dev/git_

Configure Console2 for the git bash shell :(console settings / tabs) :

- Title : Git
- Icon : c:/dev/git/etc/git.ico
- Shell : C:\WINDOWS\system32\cmd.exe /c ""C:\Dev\Git\bin\sh.exe" --login -i"

You can either configure ConEmu with the same command line.

Launch a new shell and check :
{% highlight sh %}
git config -l
{% endhighlight %}    

and eventually modifiy them
{% highlight sh %}
git config –-global user.name xxx
git config –-global user.email xxx@xxx.com
git config --global core.editor vim
git config color.ui true
git config format.pretty oneline
git config --global http.proxy http://user:password@proxy.adress:port
{% endhighlight %}
  
Check again : 
{% highlight sh %}
git config --list # pour vérifier
{% endhighlight %}
You can use SublimeText as Git editor : 
{% highlight sh %}
git config --global core.editor "'c:/program files/sublime text 2/sublime_text.exe' -w"
{% endhighlight %}

### SQLite3 3.7.15.2
Go on [SQLite](http://www.sqlite.org/download.html) and download 'precompiled binaries for windows' : 
- sqlite-dll-win32-x86-...zip : the dll 
- sqlite-shell-win32-x86-...zip : the shell SQLite

Copy all of them under _c:/dev/bin_ (so they are in the PATH) and test : 
{% highlight sqlite3 %}
sqlite3
.help
.quit
{% endhighlight %}

### Your Ruby library : GEM
First update : 
{% highlight sh %}
gem update --system
{% endhighlight %}
And the others : 
{% highlight sh %}
gem update
{% endhighlight %}

### And finaly Rails 4 !!
{% highlight sh %}
gem install rails --version 4.0.0.beta1 --no-ri --no-rdoc
rails -v
rails server -p 80
{% endhighlight %}

And ... normaly you'll get some nusty bug here from SQLite3 :) Don't worry, check the next article.

