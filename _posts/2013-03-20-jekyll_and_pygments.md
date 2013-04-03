---
layout: post
title: "Dr Jekyll and Github"
description: "Setup a blog"
tags: ['jekyll','markdown','github']
published: true
---

### Markdown : choising the right one

So we've got rdiscount, maruku, redcarpet, redcloth and kramdown ... (look at <https://www.ruby-toolbox.com/categories/markup_processors>) The last one, kramdown, seem to be the most active with lot of nice features (simplified code declaration, tables, ...).

But, after few try, the configuration Windows + Ruby 2.0 + Jekyll doesn't work with any of them (problem with encoding : "incompatible encoding regexp match (UTF-8 regexp with CP850 string)" ... i have to look further).

Still work : the old rdiscount ... Ok.

### Jekyll : choosing a theme.

After few digs, i choose this one <https://github.com/caarlos0/up> : it's simple, doesn't have some features (tags, articles) but for the starting, it feet.

Cloning it, changing the configuration and it's ok (it come with Disqus, Gauge, Google analytic, ... with a centre configuration in __config.yml_).

### Highlighting some code

With pygments.rb. So : install the gem `gem i pygments.rb` and ... install Python ! Tried with Python 3, but Pygments doesn't work with it (look at issues on Github), so installed Python 2.7 : work with no error, some hatml class generated ... missing a css !!

Digging again and found this solution : <http://www.stehem.net/2012/02/14/how-to-get-pygments-to-work-with-jekyll.html>.

For generating the css file, go to your pygments.rb gem folder _C:\Ruby200\lib\ruby\gems\2.0.0\gems\pygments.rb-0.4.2\vendor\pygments-main_ and launch :

{% highlight sh %}
pygmentize -S default -f html > pygments.css
{% endhighlight %}

Copy the css file into your jekyll css directory, declare it in the layout, `<link href="/css/pygments.css" rel="stylesheet">` and this time all is done :)

For highlighting some code, you must embrace him with a `{ % highlight lexer_name % }` starting block and finish it with a `{ % endhighlight % }` block (remove the space betwenn { or } and % for proper work). You've got plenty of lexer : ruby, irb, bash, bat ... check <http://pygments.org/docs/lexers/>.

Feel free to look in deep at this github repository.

### Some Git

Before sending your pages to Hithub, check them in local with `jekyll serve` : if there are some syntax error, you'll find them quickly (on other side, the page with error isn't displayed and there are no warning ...)
Simply :
{% highlight sh %}
git add .
git comit -m 'my commit'
git push origin master
{% endhighlight %}

