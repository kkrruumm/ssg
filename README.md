# ssg
~~shitty~~ shell site generator

this script is currently capable of producing the pages and atom feed for my website, https://kris.sh/

most likely, this script will grow as time goes on and it's used for more things.

this currently `cloc`s in at 98sloc, though extreme minimalism is, as per usual, not the primary goal here.

# dependencies

* `lowdown`
* any POSIX-capable shell

# usage

`ssg [ build | postlist | postindex | feed | posthdr FILE ]`

## directory layout

you're expected to have `layouts/` and `src/` directories where this script is executed from.

`layouts/` should contain the `footer.html` and `header.html` files that will be applied to every page.

the `src/` directory will contain various things, primarily markdown sources for your website, but also things like css and any other static content.

a standard setup, for example, may be:

```
.
├── layout
│   ├── footer.html
│   └── header.html
├── src
│   ├── css
│   │   └── main.css
│   ├── fonts
│   │   └── dejavusans
│   │       ├── AUTHORS
│   │       ├── DejaVuSans.woff2
│   │       └── LICENSE
│   ├── image.png
│   ├── index.md
│   ├── posts
│   │   └── writing-a-site-generator
│   │       └── index.md
│   └── services
│       └── index.md
└── ssg
```

the above setup depicts the skeleton of my website, `services`, `posts` being extra pages "under" the primary one.

anything that isn't a markdown file will be copied over verbatim, so `image.png` in this example will land at the top level, whereas any images in `writing-a-site-generator`, for example, will land in `posts/writing-a-site-generator/image.png`.

## placeholders

if you want to use them, there are `{{title}}` and `{{section}}` placeholders the script will replace during build for your `header.html`.

more of these should probably be added in the future, but these serve for kris.sh via:

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>{{title}}</title>
    <link rel="icon" href="/favicon.ico">
    <link rel="alternate" type="application/atom+xml" title="kris.sh" href="/posts/index.xml">
    <link rel="stylesheet" href="/css/main.css">
  </head>
  <body data-section="{{section}}">
    <header><div class="top">
        <a class="homeheader" href="/">kris.sh</a>
        <div class="nav">
          <a class="navContent" data-nav="home" href="/">~/</a>
          <a class="navContent" data-nav="posts" href="/posts/">~/blog</a>
          <a class="navContent" data-nav="services" href="/services/">~/services</a>
          <a class="navContent" href="/posts/index.xml" title="blog feed">~/rss</a>
    </div></div></header>
<main>
```

## pages

all websites should be written in standard markdown. this script is more or less similar to hugo in this regard, blogposts for example may have:
```
title: What Linux distro should I use? | kris.sh
date: 2025-07-30T09:57:13-05:00
pubdate: July 30, 2025
tags: Linux
```
at the very top.

there is currently no functional tag viewer, TODO.

## building

just run `./ssg` or `./ssg build` from the root of your website.

# contributing

the point of this isn't to have every feature in the world, but features that fit the vibe check will *absolutely* be accepted.

as a general guideline though, usage of non busybox compatible/POSIX shell features will be accepted.
