---
layout:     post
title:      "Missing Padlock"
subtitle:   "A tool to find mixed content issues"
date:       2017-10-25 12:00:00
author:     "Chris"
header-img: "img/home-bg.jpg"
---

I'm currently working on a project to transition hundreds of client sites to HTTPS. We've been able to fully automate most of the process,
but there's still the tricky issue of mixed content. This is when an HTTPS page still has a reference to an HTTP asset and, as a result,
the insecure asset is either blocked or the entire page is marked as insecure by browsers.

There are a few common culprits. Often, the site has a reference to something like Google Fonts or Recaptcha that's included on every page.
It's pretty common, too, to have a few stray pages across a site that are directly referencing images from another site or are trying to
include some sort of third-party script that's using HTTP. The trick is finding all of these mixed content issues ahead of time.

To make that a bit easier, I put together a tool called [Missing Padlock](https://www.missingpadlock.com). It will crawl an entire site
(well, up to a point) and identify all the mixed content references. You can even run it before implementing HTTPS on a site to proactively
fix those references.

I've also put together a site called [Mixed Content Examples](https://www.mixedcontentexamples.com) that's in the spirit of [Bad SSL](https://www.badssl.com).
It contains a bunch of pages with examples of mixed content errors.
