---
layout: post
title: "5. Free website with GitHub Pages"
categories: tutorials
featured: False 
---


______________________________________________________________________________________________________

### <span style="color: red; font-weight: bold;">Getting Started with GitHub Pages and "Just the Docs" </span>

This guide will help you get started with GitHub Pages using the "Just the Docs" theme. It assumes you have a Windows 10 operating system and the following requirements:

    GitHub account
    Git Bash
    Ruby
    Sublime Text

Step 1: Install Required Software

To build a static website, you need to install Git Bash and Ruby.

    Install Git Bash to gain access to Bash.
    Install Ruby to utilize RubyGems.

> https://git-scm.com/downloads Git Bash

> https://www.ruby-lang.org/en/downloads/ Ruby



Both Git Bash and Ruby are necessary to update your website from your local machine.
Step 2: Choose a GitHub Pages Theme

    Visit the just-the-docs/just-the-docs repository on GitHub.
    Fork the repository to your GitHub account.

Fork Repository

    Explore other available themes on resources like jekyllrb.com/docs/themes or jekyllthemes.io/free.


![fork](/assets/fork.jpg)

![fork2](/assets/fork2.jpg)

Step 3: Create Your Website Repository

Set the name of your repository to your username at .github.io (e.g., username.github.io, where "username" is your GitHub username).

Open Git Bash and navigate to the desired location to store your website (e.g., cd Documents/).

Clone the repository locally using the following command:

    gh repo clone username/username.github.io

Access the downloaded files for your basic website:

    cd /username.github.io
    bundle exec jekyll serve

The command bundle exec jekyll serve starts the local server, allowing you to configure the website live.

Step 4: Important Directories and Files

onfig.yml is the configuration file for your website.
The "posts" directory holds your blog posts. Try creating a new post and see where it appears on the site.
The "assets" folder is used to store images and other resources for your website.

Step 5: Uploading Your Site from Local Machine

To upload your website to GitHub Pages, you may need to use a Personal Access Token (PAT). Follow these steps:

Generate a Personal Access Token (PAT) on GitHub. Go to your GitHub account settings > Developer settings > Personal access tokens.
Create a new token with the necessary permissions (e.g., repo for repositories).
Copy the generated PAT and store it securely.

To upload your site using the PAT:

Open Git Bash and navigate to your local repository.

Set the remote URL for your repository using the following command:

    git remote set-url origin https://username:<PAT>@github.com/username/username.github.io.git

Replace username with your GitHub username and PAT with the generated Personal Access Token.

Commit your changes and push them to GitHub:

    git add .
    git commit -m "Update website"
    git push origin main

Now, your website will be deployed on GitHub Pages using the "Just the Docs" theme.




