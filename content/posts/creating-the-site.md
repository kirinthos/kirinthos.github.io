---
title: "Creating the Site"
summary: "What it took for me to finally get this blog thing off of the ground"
date: 2022-02-19T22:34:33-05:00
tags: [blog, hugo]
draft: true
---

I have finally done it. I've started a blog! I've been telling myself for years that I'd finally get to writing
one of these, now it seems that day has finally come. 

## What is this about?

This will be a collection of my thoughts on various topics. Most often it will be about programming, mathematics,
data science, and maybe a bit of physics if I get to writing about it. Some of the ideas may be half-baked,
others might be a hyper-technical dive into a weird problem I've encoutered, a couple of them might even be
entertaining.

Let's dive in with our first mini-article. Creating the blog!

## Creating the site

When creating this site I wanted to find something simple. I need a way that I can remove the most friction from
the workflow of creating and posting articles I write...otherwise I fear I'd never write them. I'm very much
the type of person who solves problems, does some exciting stuff, has a very brief celebration (maybe) and then
immediately moves on. 

_I'm trying to change, though._

Part of this change is writing my thoughts down as I discover and teach myself new things. I'm stringing you along
for the ride and maybe we can help each other learn some things along the way. So we'll talk about our first thing:
what went into creating this blog?

I said that I enjoy minimal friction to recording the events of my life. In this same vein, I set out to find easy
ways to host a website. I don't really want to setup something in AWS or GCP to host my content, even further than
that I don't want a "deployment process" at all! I want something that's so easy to use, I _must_ write articles, 
because there's nothing standing in the way! Blogs get posted easily, they are preferably organized, perhaps
searchable, maybe some tagging mechanisms, maybe a way to easily share my content to social media platforms
(though I'm not particularly a fan of those). This is a lot of little checkboxes, but we're now into the 2020s...
certainly it's possible to do this now!

I set out to search for a decent blog framework. Immediately as I started searching I realized...I really want
to write in [markdown](https://markdownguide.org) format. If you don't know (I'd be amazed), markdown is a common
plaintext format that allows for some decent text formatting options. Because this blog will be about some
programming stuff along the way, I want an option to write some code blocks. Support for many languages will
be ideal because we'll jump around a bit, but it definitely has to support my latest love: Rust!

```rust
#[derive(Debug)]
struct Data<'a> { v: &'a str }

let v = Data { v: "does!" };
println!("and it {:?}", v);
```

We'll work on getting a solid code theme into here eventually, though.

Armed with a few constraints I was able to narrow down my search to blog frameworks with markdown support.
Searching on google for "blog frameworks markdown" gets us a list of a few frameworks. Among these options are
[jekyll](https://jekyllrb.com/), [hugo](gohugo.io), [hexo](https://hexo.io/), and then
[some article](https://www.webfx.com/blog/web-design/open-source-blogging-platforms-for-developers/)
about common blog frameworks. When I read this article, it was really cemented that I'm looking for a mere
static content generator! Why do anything more than I have to? I'm kind of getting tired of the unnecessary
bloat of the latest web frameworks anyway...so let's keep it simple.

I ended up looking at `jekyll`, `hexo`, and `hugo` and went with `hugo` because, truth be told, we started using this
recently at my current job and it's worked well for us so far. It can be setup on `heroku` and `GitHub Pages`
(what's that? I ask myself) which will make for a simple hosting solution.

I set out to the [Quick Start Guide]() and start building a simple `hugo` app. It's this article! The test
is going well so far. I've got a simple theme setup, I get to write a post, and then explore some of the features
of the `hugo` system.

## Adding social links

I set off in search of features to allow me to add social link buttons to posts so I can generate some of that
fabled interest that could one day result in me developing content full time! When I found some
[random article](https://codingnconcepts.com/hugo/social-icons-hugo/) about adding social icons into a `partial`,
I thought to myself, 

> oh, alright, we're going to be diving into some templating stuff...do I have to compose my own footer?

I look into templates a bit and start by creating a default single page template. I guess this is what `hugo`
uses to render a single blog post. After I override the default single page template, I immediately lose all
of this article's content in the development server. Perhaps obviously, because I replaced the template with
the empty set, and that's exactly what I'm getting back out of it.

I wonder if the theme I chose (at this time it's [PaperMod](https://github.com/adityatelange/hugo-PaperMod))
has an option to show some share buttons in it...this seems like something a theme should include anyway, so
the share icons blend in with the content.

I do a quick [fd](https://github.com/sharkdp/fd) (a highly recommended replacement for `find`, if we want to
get real technical, I'm using `fzf` + `fd` in vim) for `single.html` and find one inside the layout. It also 
turns out that there are docs on how to enable this on the theme's github, but I didn't think to read that
far into a theme's docs, assuming they'd be rather empty. Nonetheless, at the bottom of this single page
template I see some `.Param` checks. One of them is `ShowShareButtons`! So, I move back over to my `config.toml`
and set this parameter inside the configuration. After searching through this template for other potential
`.Param`, my configuration now contains:

```toml
[params]
disableThemeToggle = true
showShareButtons = true
tags = true
showToc = true
showPostNavLinks = true
```

---
**Aside**

I have noticed a couple of articles talking about using `yaml` instead of `toml`...I wondered if this is just
an immediate switch that doesn't require much effort? I immediately attempt renaming my `config.toml` to 
`config.yaml` and do a bit of find/replace on ` =` => `:` which does most of the required transformation to yaml.
After that, I just adjust the bracketed `[params]` section and rebuild `hugo`.

It worked!

---

Doing a brief test on some of these links it appears to work alright, despite the use of `localhost` in the
domain, which I assume causes some confusion on these sites looking for content at a valid location. We'll have
to wait until I take the whole thing online, I suppose...

## GitHub Pages

Let's do it. We've got...at least kind of a blog post here, some minimal content in a first article, a home page,
a blog name, even a domain name!

Can we turn this into a real website? [information](https://gohugo.io/hosting-and-deployment/hosting-on-github/)

I'm going to give this an attempt, if you can see this on https://crosscompiled.com I guess we've made it!

This has been a rather long article that seems to make much ado about nothing. Perhaps if you're wondering how
to get a simple blog off of the ground this process could help you. It kind of shows how by "just starting"
you can get to a point where you can start making content and then refine the thing as you go. Stay tuned for
more articles!
