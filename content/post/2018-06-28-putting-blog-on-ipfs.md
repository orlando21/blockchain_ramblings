---
title: Getting this blog on IPFS
author: Greg Babb
date: '2018-06-28'
categories:
  - File storage
slug: putting-blog-on-ipfs
---

Enough of preliminaries, let's get this party started! We're going to use [IPFS](https://github.com/ipfs/ipfs) for what it was made: to store some content.

The first thing I did was to head over to the [IPFS home page](https://ipfs.io/) and install it on my macbook. There, IPFS concepts are clearly explained and I'd recommend watching the [demo video](https://youtu.be/8CMxDNuuAiQ) to get started.

I'm not going to cover the install steps for IPFS here as it's [adequately done elsewhere](https://ipfs.io/docs/install/). One resource I found useful after installation was the IPFS tutorials [listed here](https://ipfs.io/docs/examples/), which show you the mechanics of IPFS and different use cases.

Also, Coral Health has written a good primer on how to use IPFS to [exchange encrypted files with someone](https://medium.com/@mycoralhealth/learn-to-securely-share-files-on-the-blockchain-with-ipfs-219ee47df54c). The tutorial combines both IPFS and [GNU Privacy Guard](https://www.gnupg.org/) for encrypting and decrypting files.

### Steps

I'm going to follow some broad steps in setting this up:

1. Add this blog to IPFS
2. Create a permanent top-level address (hash) for this blog using IPNS
3. Publish this blog on the internet via hosting and DNS

### Adding this blog to IPFS

This blog uses Hugo to generate static files so I basically have these files to add:

~~~bash
blockchain_ramblings
├── archetypes
│   └── default.md
├── config.toml
├── content
│   ├── _index.md
│   └── post
│       ├── 2018-06-27-first-look-ipfs.md
│       └── 2018-06-28-putting-blog-on-ipfs.md
├── data
├── layouts
├── static
│   └── css
│       └── theme-override.css
└── themes
    └── hugo-classic
        ├── LICENSE.md
        ├── README.md
        ├── archetypes
        │   └── default.md
        ├── exampleSite
        │   ├── config.toml
        │   ├── content
        │   └── static
        │       └── css
        │           └── theme-override.css
        ├── images
        ├── layouts
        │   ├── 404.html
        │   ├── _default
        │   │   ├── list.html
        │   │   ├── single.html
        │   │   └── terms.html
        │   └── partials
        │       ├── foot_custom.html
        │       ├── footer.html
        │       ├── head_custom.html
        │       └── header.html
        ├── static
        │   └── css
        │       ├── fonts.css
        │       └── style.css
        ├── theme.toml
~~~

The command to add a directory with files and subfolders to IPFS is:

~~~bash
ipfs add -r blockchain_ramblings/
~~~

This converts everything into hashes:

