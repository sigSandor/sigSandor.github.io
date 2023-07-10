---
layout: post
title: "How to start a free website"
categories: tutorials
featured: False 
---


______________________________________________________________________________________________________


### <span style="color: red; font-weight: bold;">Quick access links</span>

These are the steps I took to get started making a free website.  

requirements:


OS: Windows 10
Github account
Git bash
Ruby
Sublime text

______________________________________________________________________________________________________


The first step is to install the necessary software in order to build a static website

1. install Git Bash and Ruby. 

Git bash will give us access to bash, which I like to use in conjunction with The Ruby language, which allows us to use RubyGems.

In short, Gems are like plugins stored in the gemfile.

> https://git-scm.com/downloads Git Bash

> https://www.ruby-lang.org/en/downloads/ Ruby


Both are needed to update your website from your local machine.

______________________________________________________________________________________________________ 

2. Getting started, choosing a github pages theme.

I used https://github.com/jusx/really-simple

You can also look for themes on "https://jekyllrb.com/docs/themes/"         "https://jekyllthemes.io/free"

And more on github, google etc.

![fork](/assets/fork.jpg)

![fork2](/assets/fork2.jpg)

______________________________________________________________________________________________________

3. Creating your own Website Repository, and downloading it locally

https://github.com/jusx/really-simple 

On the example page I have given, you *must* fork the repository FIRST. Secondly, you also have to set the name of the repository to *your* username at .github.io 

("username.github.io", "username" is your GitHub username) 



Next, open *Git Bash* 

so we can navigate to where we want to store our website. 

> cd Documents/

Then

>  gh repo clone username/username.github.io


Now we have the files for a basic website. 

> cd /username.github.io


> bundle exec jekyll serve 

bundle exec jekyll serve will start the local server so you can configure the website live.
______________________________________________________________________________________________________

4. Important directories and files 

- config.yml is our configuration file

- the "posts" directory will hold your posts for a blog. Try creating a new post and figure out where it is created on the site.

- asset folder will hold pictures etc.

Go on and try it out! 


