---
layout: post
title: "My CYGWIN Development Environment"
tagline: "CYGWIN on Windows 7 Professional for my development needs"
tags: [cygwin, windows 7, ruby, ruby on rails, python, django]

---
{% include JB/setup %}

### Operating System and Machine Type

{% highlight text %}
Windows 7 Professional (c)

Processor:              AMD Sempron(tm) Processor 3100+ 1.80 GHz
Installed Memory(RAM):  2.00 GB
System Type:            32-bit Operating System
{% endhighlight %}

### Install Base CYGWIN system

CYGWIN Install File: [CYGWIN Setup.exe](http://cygwin.org/setup.exe)

#### Pass 1: Install Base CYGWIN

I normally just run the setup on the base install first so that I can get the 
system on the machine first. Then I re-run the setup again to go through and 
select packages that I want to install.

#### Pass 2: Install all CYGWIN Devel Packages

On the next run through of CYGWIN setup select the entire "Devel" category for 
install and conintue round 2 of installs. Nothing harmed to installing more than 
you need. You can always go back through and clean up the packages that you 
don't need at a later time which should be minimal at most. But as this is my 
"development" environment why not do a complete setup of everything that CYGWIN 
has to offer for development. Plus I got tired of having to constantly go back 
through CYGWIN setup on crap that needed to be installed for getting gems and 
other utilities to compile correctly. So I just do a complete install of this 
package to get passed this.

#### Pass 3: Install Selected CYGWIN Packages

Okay now that we have gone through the setup twice lets go through one last 
time and select some additional packages that we will need.

**NOTE:** This is only a list of packages that I go through and check for 
install.

* Database
  * \+ libsqlite3-devl
  * \+ libsqlite3_0
  * \+ sqlite3
* Editors
  * \+ gvim
  * \+ nano
  * \+ vim
  * \+ xemacs
* Graphics
  * \+ ImageMagick
* Net
  * \+ curl
  * \+ inetutils
  * \+ openssh
* Shells
  * \+ mintty ([http://code.google.com/p/mintty/](http://code.google.com/p/mintty/))
  * \+ zsh

### Ruby Development Environment

Install RubyGems  
RubyGems: [http://rubygems.org/pages/download](http://rubygems.org/pages/download)

{% highlight bash %}
$ wget http://production.cf.rubygems.org/rubygems/rubygems-1.3.7.tgz
$ tar xvfz rubygems-1.3.7.tgz
$ cd rubygems-1.3.7/
$ ruby setup.rb install
{% endhighlight %}

Install `rdoc` & `rdoc-data`  
RDoc: [http://github.com/rspec/rspec](http://github.com/rspec/rspec)  
RDoc-Data: [http://github.com/rspec/rspec-rails](http://github.com/rspec/rspec-rails)

{% highlight bash %}
$ gem install rdoc rdoc-data
{% endhighlight %}

Setup `rdoc-data`

{% highlight bash %}
$ rdoc-data --install
{% endhighlight %}

Install Rails 3  
rails: [http://rubyonrails.org/](http://rubyonrails.org)

{% highlight bash %}
$ gem install rails
{% endhighlight %}

Install database connectors  
sqlite3-ruby: [http://github.com/luislavena/sqlite3-ruby](http://github.com/luislavena/sqlite3-ruby)  
mysql: [http://rubyforge.org/projects/mysql-win/"](http://rubyforge.org/projects/mysql-win/)

{% highlight bash %}
$ gem install sqlite3-ruby
$ gem install mysql --platform x86-mingw32
{% endhighlight %}

Install `rspec` & `rspec-rails`  
rspec: [http://github.com/rspec/rspec](http://github.com/rspec/rspec)  
rspec-rails: [http://github.com/rspec/rspec-rails](http://github.com/rspec/rspec-rails)

{% highlight bash %}
$ gem install rspec-rails
{% endhighlight %}

I like to use Growl for Windows for autotest. Install the following only if you 
like to have autotest notification on the desktop.  
autotest: [http://github.com/grosser/autotest](http://github.com/grosser/autotest)  
autotest-rails-pure: [http://github.com/grosser/autotest-rails](http://github.com/grosser/autotest-rails)  
autotest-growl: [http://www.bitcetera.com/en/products/autotest-growl](http://www.bitcetera.com/en/products/autotest-growl)  

{% highlight bash %}
$ gem install autotest autotest-rails-pure autotest-growl
{% endhighlight %}

I use Jekyll for this site so I need to install the gems that I need.  
jekyll: [http://github.com/mojombo/jekyll](http://github.com/mojombo/jekyll)  
rdiscount: [http://github.com/rtomayko/rdiscount](http://github.com/rtomayko/rdiscount)  
RedCloth: [http://redcloth.org/](http://redcloth.org/)  

{% highlight bash %}
$ gem install jekyll rdiscount RedCloth
{% endhighlight %}

### Python Development Environment

Install setuptools  
setuptools package: [http://pypi.python.org/pypi/setuptools](http://pypi.python.org/pypi/setuptools)  

{% highlight bash %}
$ cd /tmp 
$ wget http://pypi.python.org/packages/2.6/s/setuptools/setuptools-0.6c11-py2.6.egg
$ sh setuptools-0.6c11-py2.6.egg
{% endhighlight %}

Install Django  
Django: [http://djangoproject.com/](http://djangoproject.com/)

{% highlight bash %}
$ easy_install django
{% endhighlight %}

Install Pygment for Jekyll install code highlighting  
Pygments: [http://pygments.org/](http://pygments.org/)

{% highlight bash %}
$ easy_install pygments
{% endhighlight %}

That's just about it. If you want some of my examples of how I terminal and 
tools that I use I have included them below 

### Setup VIM

I use VIM for a few things so I download two additional plugins for my VIM 
install.

*Rails*  
rails.vim: [http://www.vim.org/scripts/script.php?script_id=1567](http://www.vim.org/scripts/script.php?script_id=1567)

*Textile*  
Textile for VIM: [http://www.vim.org/scripts/script.php?script_id=2305](http://www.vim.org/scripts/script.php?script_id=2305)

`.vimrc`

{% highlight bash %}
set tabstop=2
set shiftwidth=2
set softtabstop=2
set expandtab
set ai
set si
set nu
set backspace=indent,eol,start
set gfn=Courier_New:h9:cANSI
syntax on
filetype on
colorscheme slate
{% endhighlight %}

**Setup `mintty` Terminal and Defaults**

`.bashrc`

{% highlight bash %}
# base-files version 3.9-3

# To pick up the latest recommended .bashrc content,
# look in /etc/defaults/etc/skel/.bashrc

# Modifying /etc/skel/.bashrc directly will prevent
# setup from updating it.

# The copy in your home directory (~/.bashrc) is yours, please
# feel free to customise it to create a shell
# environment to your liking.  If you feel a change
# would be benificial to all, please feel free to send
# a patch to the cygwin mailing list.

# User dependent .bashrc file

# Environment Variables
# #####################

# TMP and TEMP are defined in the Windows environment.  Leaving
# them set to the default Windows temporary directory can have
# unexpected consequences.
unset TMP
unset TEMP

# Alternatively, set them to the Cygwin temporary directory
# or to any other tmp directory of your choice
export TMP=/tmp
export TEMP=/tmp

# Shell Options
# #############

# When changing directory small typos can be ignored by bash
# for example, cd /vr/lgo/apaache would find /var/log/apache
shopt -s cdspell

# Aliases
# #######

# Interactive operation...
alias rm='rm -i'
alias cp='cp -i'
alias mv='mv -i'

if [ -x /usr/bin/dircolors ]; then
  test -r ~/.dircolors && eval "$(dircolors -b ~/.dircolors)" || eval "$(dircolors -b)"
  alias ls='ls -hF --color=auto'
  alias dir='ls --color=auto --format=vertical'
  alias vdir='ls --color=auto --format=long'

  alias grep='grep --color=auto'                     # show differences in colour
  alias fgrep='fgrep --color=auto'
  alias egrep='egrep --color=auto'
fi

# Some shortcuts for different directory listings
alias ll='ls -l'                              # long list
alias la='ls -A'                              # all but . and ..
alias l='ls -CF'                              #

# Shorten commonly used commands
alias srv='rails server'
alias mig='rake db:migrate'
alias log='tail -f log/development.log'

# e-texteditor
alias e="cygstart /cygdrive/i/e-texteditor/e.exe"

# Mount custom directory to cygwin environment
# You can then access these directories using cd /rails and open by default

export VIM=/usr/share/vim/vim73
{% endhighlight %}

`.bash_profile`

{% highlight bash %}
# base-files version 3.9-3

# To pick up the latest recommended .bash_profile content,
# look in /etc/defaults/etc/skel/.bash_profile

# Modifying /etc/skel/.bash_profile directly will prevent
# setup from updating it.

# The copy in your home directory (~/.bash_profile) is yours, please
# feel free to customise it to create a shell
# environment to your liking.  If you feel a change
# would be benifitial to all, please feel free to send
# a patch to the cygwin mailing list.

# ~/.bash_profile: executed by bash for login shells.

# source the system wide bashrc if it exists
if [ -e /etc/bash.bashrc ] ; then
  source /etc/bash.bashrc
fi

# source the users bashrc if it exists
if [ -e "${HOME}/.bashrc" ] ; then
  source "${HOME}/.bashrc"
fi

# Set PATH so it includes user's private bin if it exists
if [ -d "${HOME}/bin" ] ; then
  PATH=${HOME}/bin:${PATH}
fi

# Custom Paths
JAVA_HOME=/cygdrive/d/src/jdk1.6.0_21

# Set PATH
PATH=$JAVA_HOME/bin:$PATH
export PATH
{% endhighlight %}

### Shortcuts for Terminal

{% highlight bash %}
$ ln -s /cygdrive/i/projects /projects
$ ln -s /cygdrive/i/src /src
$ ln -s /cygdrive/j/servers /servers
{% endhighlight %}