---
layout: post
permalink: how-to-fix-ruby-on-rails-in-os-x-el-capitan
title: How to fix Ruby on Rails in OS X El Capitan
date: 2015-10-10
autor: Enrique Benitez
description: Fixing Ruby on Rails in OS X El Capitan through Rbenv and some commands...
color-code: development-blue
category-tag: Development
category-tag-slug: blog-content-post-category-tag
category-title-slug: blog-content-post-title
category-link-slug: blog-content-post-link
categories: development
image: http://media.idownloadblog.com/wp-content/uploads/2015/06/Wallpaper-OS-X-El-Capitan-Mac.jpg
---
Two days ago, I upgraded to El Capitan, since then my Macbook Pro is smoother, faster and feels a little bit lighter, everything seemed to be perfect, until yesterday.

<h3 markdown="1" class="text-to-center">El Capitan broke my development environment
</h3>

![Captain Hook](https://cdn-images-1.medium.com/max/800/1*a68imd1bX8obl6HylT6NQg.jpeg){: .md-image .image-to-center}

Yes, I started to hate El Capitan, but as I dig deeper into the problem, I found why my dev environment is all fucked up.

The problem was with **Homebrew**.

### Homebrew vs SIP ###

As you know, Homebrew is a package manager for OS X, you probably have been using it to install things into your machine, like this:

<script src="https://gist.github.com/bntzio/5488f1dd93c088d19e5a.js"></script>

Well, that’s awesome, but the problem with OS X El Capitan and Homebrew is that SIP (System Integrity Protection) doesn’t play very well with Homebrew at the moment.

SIP prevents you from writing to many system directories such as /usr, /System & /bin, regardless of whether or not you are root, that’s the problem (but a very nice security feature for normal users).

Obviously, Homebrew and SIP are nemeses.

### Hum… OK, but how do I fix it? ###

Ok, too much information for now, let’s get to the nitty gritty.

In order to fix your development environment, you’ll need to destroy it first.

#### Install XCode CommandLine Tools ####

This is because Homebrew depends on these tools.

<script src="https://gist.github.com/bntzio/9d3ec1e21bb4f444bbc9.js"></script>

**Note**: *if something like this appears, just click “Install” (if you already have Xcode) or “Get Xcode” if you don’t*.

#### Reinstall Homebrew ####

Handy scripts:

<script src="https://gist.github.com/bntzio/63ba83c8d97efec975bb.js"></script>

<script src="https://gist.github.com/bntzio/c2920cab8a7741f25c98.js"></script>

**Note**: *it may not be needed to reinstall Homebrew, however I did it because I wanted a clean install of my packages in my new OS X El Capitan, if you do so as well, feel free to reinstall Homebrew, but backup your local databases if you got any you’d like to keep, remember that Homebrew installed your DB’s (MySQL, PostgreSQL) and if you uninstall Homebrew, all your packages will be removed as well*.

### Here comes the REAL solution ###

Welcome, rbenv.

![Rbenv](https://johndelblog.s3.amazonaws.com/uploads/upload_4/homepage_rbenv.png){: .image-to-center}

**Rbenv** is an awesome version manager for Ruby (similar to RVM).

This is the real solution to all of your problems regarding installations when you use rbenv, you isolate the installations of your packages or gems so you don’t fuck up your projects when versioning and so on.

#### Install rbenv with Homebrew ####

<script src="https://gist.github.com/bntzio/a99900ca281b2f79c44d.js"></script>

#### Add rbenv to bash so that it loads every time you open a terminal ####

<script src="https://gist.github.com/bntzio/196a3b6fa43f689fa297.js"></script>

#### Source your ~/.bash_profile ####

<script src="https://gist.github.com/bntzio/0dfe1baefd85a3ec455b.js"></script>

#### Install Ruby with rbenv ####

<script src="https://gist.github.com/bntzio/c136a01b3c113df2d9dc.js"></script>

#### Check your Ruby version ####

<script src="https://gist.github.com/bntzio/5fc1b2288c08a1c9bdf0.js"></script>

#### Install Rails ####

<script src="https://gist.github.com/bntzio/052b4b6537089c2d8e84.js"></script>

This will install Rails 4.2.4 (recommended) in a rbenv environment.

#### Tell rbenv about it with rehash ####

<script src="https://gist.github.com/bntzio/c331e787f22f099d4f12.js"></script>

#### Verify Rails is installed ####

<script src="https://gist.github.com/bntzio/91c5b8ef8e757d6e4385.js"></script>

#### Setting up databases ####

MySQL:

<script src="https://gist.github.com/bntzio/bba94b53afda1be2d364.js"></script>

PostgreSQL:

<script src="https://gist.github.com/bntzio/5488f1dd93c088d19e5a.js"></script>

And that’s it! now you can continue working with Ruby on Rails as normal, try it by creating a new rails application.

<script src="https://gist.github.com/bntzio/4de1b5751fa274f576b0.js"></script>

And voila! Ruby on Rails working on OS X El Capitan with rbenv and Homebrew.

**Note**: *just remember to source your bash_profile each time you want to work with rbenv and their virtual environments, if you don’t source it, you will not have any installations (because they are inside the rbenv environment, not in your local environment), it’s a way better way to manage your packages and/or gems don't you think? ;)*

### Conclusion ###

I think that OS X El Capitan increases the security of our machines in a very good way, sometimes that’ll affect developers (like you and me) but the good thing is, now we are kind of forced to work with more security while developing apps, before the El Capitan upgrade, I didn’t have rbenv or a Ruby version manager at all, I just installed everything in my local machine configuration, which is bad practice when you start working with multiple applications that need different configurations and environments.

Oh, you may want to take a look at [Vagrant](https://www.vagrantup.com/) the next time you upgrade to a different OS, it’s a very elegant way to manage development environments, it’s worth to take a look and play with it, I just implemented Vagrant in my everyday development workflow, I’ll write about it soon, so stay updated ;)

