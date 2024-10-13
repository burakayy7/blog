---
navigation: true
cover: assets/images/jekyll-main.png
title: How I started to Build my website locally
date: 2024-10-12
class: post-template
tags: miscellaneous
layout: post
current: post
subclass: 'post'
---

For a long time (3-4 years!) I have been updating this website either using the online GitHub editor, or cloning it locally and pushing updates. But, today I said enough is enough, overcame my laziness, and finally decided to install Jekyll and build my site locally, so I can test changes fast! This is how I did it.


I will be referencing [this page](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll), so if you wanna follow along...

Ok, first I needed to install Ruby for Windows: [rubyInstaller](https://rubyinstaller.org/)

And I installed the newest version I could. But, I later found out that for some reason, I need a 3.1.X version for Jekyll, so maybe you could research about that, but I suggest you install 3.1.3 (what I ended up doing).

Once you install the Installer and finish the progress, you should see a terminal with Ruby that pops up, asking which of 3 would you like to install:

![alt text](assets/images/miscellaneous/ruby1.png)

Please press 3, then Enter.

Ok, now if you open another Command Prompt, you should get a valid result for:

```
ruby --version
```

Now, using this, we need to install Jekyll and Bundler:
```
gem install jekyll bundler
```

Next, open Git Bash in the folder of the repository you cloned (this should be the repo where your GitHub Pages Jekyll Site is at, and cloned to your local machine) and type:
```
bundle install
```

Now, for me, I also had to do another step before doing this (or just run bundle install again):

I needed to add webrick to my Gemfile, so just add this line to yours:

```
gem 'webrick', '>= 1.7.0'
```

After that is install, all you need to do is run 
```
bundle exec jekyll serve
```

And the output should look something like this:

```
Configuration file: C:/Users/Burak-as-user/Desktop/gitclones/blogEdits/blog/_config.yml
            Source: C:/Users/Burak-as-user/Desktop/gitclones/blogEdits/blog
       Destination: ../blog-pages/
 Incremental build: disabled. Enable with --incremental
      Generating...
       Jekyll Feed: Generating feed for posts
                    done in 4.244 seconds.
  Please add the following to your Gemfile to avoid polling for changes:
    gem 'wdm', '>= 0.1.0' if Gem.win_platform?
 Auto-regeneration: enabled for 'C:/Users/Burak-as-user/Desktop/gitclones/blogEdits/blog'
    Server address: http://127.0.0.1:4000/blog//
  Server running... press ctrl-c to stop.
```

And you should be Done!!

**
I used this with a Jekyll Theme, so I am assuming that you also are using this with a Jekyll website made for GitHub Pages.


And the output provides an Address which the local website should be, and where you can see live changes, locally.

Hope this was helpful!

