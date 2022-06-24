---
layout: page
title: sanesite
tags:
  - sanesite
  - Java 
  - github
  - Jekyll
---

[Sanesite](https://github.com/bvarner/sanesite) is a static website content generator that turns [markdown documents like this](https://raw.githubusercontent.com/bvarner/bvarner.github.io/master/pages/sanesite.md) into this webpage.
It's a  bit like (and borrows ideas from) [Jekyll](https://jekyllrb.com) but it's heritage is wholly different.


### Why sanesite?
* Static site managment trumps live-code, every time. 
  I won't go into it here, but if you've ever been involved in creating, maintaining, managing, or using a non-static CMS, you know why.
* Jekyll won't do what I want, how I want, and the github pages support for it is several major releases behind. 
* I've done everything from custom CMS to Wordpress in the past, and even wrote my own static site generator years ago.
* I did the whole 'put stuff on social media'. That has become an inferior experience now.

#### Let's start at the beginning...

My HTML / website days go back the glory days of GeoCities.

After mangling my own HTML for what purposes I don't recall, I eventually landed on a custom PHP based CMS I wrote while I was in school, hosted on my own spare 486 machine that ran FreeBSD.

I limped that thing along for a few years, then broke down and started going things statically again, with server-side includes on Apache.

Eventually I self-hosted WordPress... which is a _nightmare_.

After that, I think around 2010 or 2011, I created a thing I called KickBlog. It was a static site generator created as a custom [Ant](https://ant.apache.org) task that used [Velocity](https://velocity.apache.org) templates to generate a site. Individual posts were in their own files, and contained their own very basic HTML that was managed with CSS from the theme. It actually worked really well, but the migration (an export) from WordPress left a lot to be desired. While it worked, it wasn't robust, and it appears many of my sites contents were ... truncated. It was around this time that I started posting things (photos / projects) on Facebook, which was easier, and the blog sat and rusted...

Somwhere near 2013 I quit self-hosting a server altogether, and mothballed the site.

Apparently in 2015 I got jaded enough with Facebook and it's audience being a walled garden that I fired up the Github personal page, [bvarner.github.io](https://bvarner.github.io)... and went the down rabbit hole of Jekyll.

### Why not Jekyll

The following opinions are why I chose to revive and dust off an old code-base, modernize some things, and flee from Jekyll.

#### The structure
I really don't care for the structure of a Jekyll site. Ramming all your posts into one `_posts` directory seems hamfisted and not very ... organized.
I've had issues with referencing files from the root url of the site, but that could be as much me as anything else.

#### The file naming conventions
Who in their right mind has time to try to remember how to name the files?
If I'm writing a post, I want to write a post, then name it when I'm done. I want the date to come from the filesystem attributes, not the file name.
If I want to tag it, then fine. Let me add tags.

I ended up making a shell script _just to create a post in the right spot_ with the right filename... and if I didn't get it finished, then the dates would be all sorts of crazy.
Trying to read a directory that only had a handful of posts, if you wanted to edit one, was... ugh.

In my mind, I'm writing documentation for projects, or a blog. The blog -- sure slam a bunch of that in one directory, but there comes a point where a directory with hundreds of small files is a nightmare.

If I'm documenting projects, I don't want to stick that in `_posts`. I want to create a directory to store the stuff relevant to that project (media, etc.) then be able to have the generator pull that in.

Sure, you can probably do that with Jekyll. You might even have an easier time doing it with newer versions of Jekyll.... but... 

#### Github Pages Compatibility Issues

Github Pages seems frozen in time with an old version of Jekyll that just doesn't cut the mustard for me.

#### The themes

Jekyll themes are not my bag. I hate centered content that doesn't scale to the screen. I get it, they're all 'responsive' and 'mobile-first'. This site may not be, but it's mine, and I like my boxy late 2000's asthetic.
	
#### The dependencies

Seems like every week I'm getting dependabot alerts on esoteric dependencies in a Gemfile. I'm not expecting my deps for sanesite to be much better, but at least it's in a different repository and I'm not getting CVE alerts about my static website. LOL

### How sanesite is different

* You can put content wherever you want it. Make a directory, fill it with images, add a markdown file, and *bam*.
* You can pull your site, run `java -jar /path/to/sanesite.jar` and it'll generate it. There is no 'live preview' or 'server' built in.
* Preview your site with a browser on your local filesystem, then `git commit` and `git push` to publish.
* You can embed Velocity Templates into your markdown. We _could_ make sanesite extensible with plugins, but that sounds like complexity I don't need in my life.


