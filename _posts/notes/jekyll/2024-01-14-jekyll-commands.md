---
layout: post
title: "Jekyll commands and files to build blog."
date: 2024-01-14 11:50:33 +0900
categories: [notes, jekyll]
permalink: /:year/:month/:title
---
I'm going to summarize several important contents when I set-up static web pages by Jekyll and Github pages. Actually I was really suprised that it's so easy to make and deploy this blog with github built-in services, Github pages. and Here are [jekyll's getting-started page](https://jekyllrb.com/docs/) and [chirpy theme guide](https://chirpy.cotes.page/posts/getting-started/) what I refered to. Yeah, Try make your own blog too, if you want.

On this post, I'd like to leave several important memos which I have used when I make this blog.

## Commands(Set up)
- `bundle install`: install dependencies which are configurd in Gemfile
- `bundle exec jekyll serve` : Run server with dependancy modules.
- `bundle exec jekyll build` :
- `jekyll serve` : run local server...
- options :
  + `--draft` : rendering md files located in `_drafts` directory.

## Posts

- How to make a Post :
    1. create md file on `_posts` directory. And any file could be moved to any directory. That directony name would be included when you access the page, and You could check url address of each page has hieracchy structure.
    2. make layout as "page" in frontmatter

## Permalinks : permanant link or URL of a page.
- Write `permalink: "/my-new-url/"` on frontmatter, Permalink is used primaliry over field of `categories`.
- Use variables defined in frontmatter, try this -->  `permalink: /:day/:year/:title.hello-World`
- In order to use a variable, try this --> `/:(variable name)`

## Files and Directories

Gemfile 
: necessary dependency modules for production could be defined.

_config.yml 
: theme, baseurl, plugins, extenstions and etc., a lot of specific configuration setting could be made with this file.

_posts (dir) 
: where posting files are located.


## Hosting through github
### Set baseurl as github repo name.
- The base URL of your site in `_config.yml`
- Fill in baseurl field with your repository name, just like `baseurl: "/repo_name"`

### create a repo in github and sync.
1. `git init`
2. `git checkout -b gh-pages(<=branch name)` : checkout with a branch named as 'gh-pages'
3. `git status` : checking git status
4. `git add` : adding all files which are untracked yet.
5. `git commit -m "initial commit"` : Do first commit.
6. `git remote add origin  (git repo address)`: linking a repository which is made for hosting this blog.
7. `git push origin gh-pages(branch name)` : push all files which is committed by user.