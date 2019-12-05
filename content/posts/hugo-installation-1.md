---
title: "How to spin up a personal blog using Hugo - Part 1"
date: 2019-12-1T23:18:05+05:30
draft: false
featured_image: "/images/unsplash-blog-1.jpg"

tags: ['hugo']
categories: ['Personal Website']
toc: true
---

Before we start, I just want to clarify what this article is and is not - 

- Following **is** my experience of installing a Hugo blog to maintain my personal abode of learnings. This includes the hiccups I encountered along the way. Since I have set this blog up on Ubuntu 16.04, I'll be documenting the steps I had to follow to spin up a satisfactory blog accordingly and eventually host it on Github Pages.
- This certainly **isn't** a complete and one-stop tutorial for setting up a Hugo blog though I'll try to be self-sufficient by providing as many links as I can and give a heads up wherever necessary using my very special superpower - *hindsight*.

Now that we have that out of the way, here's my journey to setting up a personal website/blog using Hugo - right from setting up an environment to adding Google Analytics to track user viewership. To make it less overwhelming and for the purpose of clarity, I have broken the article into parts - 

1. Installing and running Hugo website **(You are here)**
2. Deploying your website to Github Pages - TBD
3. Adding Google Analytics and setting up a convenient Continuous Integration/Development environment. - TBD

## Setting up and installing Hugo

> The first mistake I did was to install `hugo` via Ubuntu 16.04's package manager - `apt` because it seemed the easiest. It costed me a solid 30 minutes to figure out what was going wrong since I could create all the templates necessary for a new website but not get it working on localhost. And at the time of writing this, Ubuntu 18.04 too is facing the same problem.

The second easiest thing is installing hugo via `snap` package manager.

    sudo apt-get install snapd
    sudo snap install hugo

## Create a new Hugo site

To release the Hugo goodness - 

    hugo new site <foldername>

This generates the required skeleton configuration files. If you `cd` into the folder and run `hugo server`, you'll find that an empty site awaits you at `localhost:1313`. Pretty... underwhelming. 

Fret not. The missing puzzle piece is installing a theme. I am using this amazing theme called LoveIt by [Dillon](https://dillonzq.com/). 

### Installing a theme

Instead of just reiterating the commands for installing Dillon's theme, it's easier to just link his [README](https://github.com/dillonzq/LoveIt#getting-started). It's pretty extensive and easy to follow. +1 for documentation. 

> Onto my hindsight superpower, I'd recommend to clone the theme instead of making a submodule. It's just easier to maintain in a repository. 

In the LoveIt theme folder, you'll find `exampleSite` which contains required paraphernalia - 

1. `static` - Contains images, favicons and thumbnails. This is the place where you'll place the images you'll use in your posts as a convention.
2. `content` - Contains starting About page and a demo blog post to get you started.
3. `config.toml` - The most important thing you'll need to copy from the theme to your root folder. This is the configuration file which renders the site as it is now. 

Copy these 3 things to your root folder and you're almost there.

`zh` - This contains post content in Zhōngwén language if I'm not wrong. You'll know if you require it. 

### Run Hugo Run

To render the site and bear the fruit of your effort - 

    hugo server -D --bind=0.0.0.0

1. `-D` - Serves posts with properties `draft=false` which by definition don't render on production unless the boolean is flipped.
2. `--bind` - This particular flag allows you to access your site via other device with the ip address of  your host machine. 

**Voila! Your site should be up and running on `localhost:1313` .**

> Though while accessing the website on other devices, I wasn't able to get past the home page since it tries to access `localhost:1313` explicity on clicking any of the links. Investigation required.