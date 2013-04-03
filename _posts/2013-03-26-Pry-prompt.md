---
layout: post
title: "PRY colorized prompt"
description: "It was a long way ..."
tags: ['pry','prompt']
published: true
---

### The solution, now ! 

After few hours of digging around several solution, I've finally have a working colorized prompt for PRY !*

So the final solution now : (puts those lines in your _.pryrc_ at you $HOME)

{% highlight ruby %}

Pry.prompt = [
              proc { |target_self, nest_level, pry|
                    "[#{pry.input_array.size}]\001\e[0;32m\002#{Pry.config.prompt_name}\001\e[0m\002(\001\e[0;33m\002#{Pry.view_clip(target_self)}\001\e[0m\002)#{":#{nest_level}" unless nest_level.zero?}> "
                   },
              proc { |target_self, nest_level, pry|
                    "[#{pry.input_array.size}]\001\e[1;32m\002#{Pry.config.prompt_name}\001\e[0m\002(\001\e[1;33m\002#{Pry.view_clip(target_self)}\001\e[0m\002)#{":#{nest_level}" unless nest_level.zero?}* "
                   }
              ]
{% endhighlight %}

### Explications

First the color code :

{% highlight ruby %}
color = {
  :red => "31m",
  :green => "32m",
  :yellow => "33m",
  :blue => "34m",
  :purple => "35m",
  :cyan => "36m"
}
{% endhighlight %}

The color format is `\e[0;31m` for a red and `\e[1;31m` for a darkess red, ending with a `\e[0m` sequence.

But you have to escape those special caracters because the readline library doesn't count well the line lenght. So this why we got a `\001` in starting and a `\001` in finish.

### Further reading

Pry prompt can change in realtime in the pry shell whith the `_pry_` variable, ie :

{% highlight ruby %}
_pry_.prompt = proc { "> " }
_pry_.prompt = Pry::DEFAULT_PROMPT
{% endhighlight %}

Check thoses links :

- [Pry customization](https://github.com/pry/pry/wiki/Customization-and-configuration#runtime-customization)
- [Pry issue on colorizing the prompt](https://github.com/pry/pry/issues/493)
- [Stakoverflow discussion about escaping sequence](http://stackoverflow.com/questions/8992330/why-does-my-irb-prompt-with-ansi-color-codes-mess-up-page-up-down-behavior-with)
- [Another stakeoverflow about readline and color](http://stackoverflow.com/questions/8806643/colorized-output-breaks-linewrapping-with-readline/8916332#8916332)
- [The right explication for the escaping sequence in readline](http://superuser.com/questions/301353/escape-non-printing-characters-in-a-function-for-a-bash-prompt)