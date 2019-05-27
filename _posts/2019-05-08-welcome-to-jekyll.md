---
title: "Welcome to Jekyll!"
date: 2019-05-08T15:34:30-04:00
categories:
  - Jekyll
tags:
  - documentation
---

## Initializing a Jekyll Site
To create new website with Jekyll use the command: `jekyll new folder-name`
The posts folder is where you will put your posts. Simple enough.
To initialize on Github, do the following, most of which should be familiar for Git initialization:
* git init
* git status
* git commit -m "Initialization of project"

The following two commands are for Windows specifically.

* bundle lock --add-platform ruby
* bundle lock --add-platform x86_64-linux

## Run Server
To spin up the server, enter command: `bundle exce jekyll serve`
Note that the server will continue to serve updated content as you edit it. This is a great way to check over blog posts to make sure they look good. However, any changes made to _config.yml will not appear until you close the server and then re-open it.
To terminate the server, press `Ctrl-C` on keyboard. Type `y` twice. The connection will close.


## Themes
Themes can be installed from websites like jekyllthemes.org and some ask for you to fork the repository then clone it for your project. You would use `git clone` instead of `jekyll new` for those themes. 
### Gem Themes
Other themes are available as Ruby Gems. To install a new theme from gem, do the following:
1. In `Gemfile` file, change the theme gem name. Ex: `gem  "minima"`
2. In _config.yml, change the theme to say the new theme name. Ex: `theme: minima`
3. To install the Gem, run `bundle` command.

## Create Posts
Install the Gem jekyll-compose so that you do not need to create a new file in _posts everytime you want to add a new post to your site.
1. In `Gemfile` file, add line for jekyll-compose Gem: `gem "jekyll-compose", group: [:jekyll_plugins]`
2. To install the Gem, run `bundle` command.
3. Then use the command `bundle exec jekyll post "Blog Post Name Here"` to create a new post file easily.

## Create Pages
To create a page, use the command `bundle exec jekyll page "Page Title"`. This new page will appear as a .md file at the root of your site directory.

## Front Matter
"Front matter" is the name of the properties you see added by default at the top of every post file. See https://jekyllrb.com/docs/front-matter/ for explanations on all the available properties.

## Linking to Other Pages on Site
The syntax for linking to another page in your own Jekyll site is relatively simple. The name and path appear as such: `[projects](/projects)` for a link to another page.

## Adding Images
You can simply create a folder such as "Images" in the root of your Jekyll site directory. Then stick an image or two within it. No matter what unrecognized Jekyll files you place like this, they'll just all end up ppearing in the Output folder. 

As such, once an image is in the folder, you can reference it on your pages and posts as follows:
* `![Description of image](/images/filename.jpg)`

## Publish Jekyll Website
To deploy the site for the web, you must run a new command for Jekyll to generate the final site files.
This command is: `bundle exec jekyll build`.

By default, the site files are generated in a file called `_site`. In the case that you changed the configuration, such as for this tutorial, then they will generate elsewhere. In this case they are going to genreate to the folder called `public`.

The contents of this output folder is the entire website. So you need to take all those files and upload them to a webserver.