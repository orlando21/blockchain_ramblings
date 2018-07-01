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

The first version of IPFS was written in the Go language, so I'm going with that and installing Go on my mac as a prerequisite. I'm not going to cover the install steps for IPFS here as it's [adequately done elsewhere](https://ipfs.io/docs/install/). One resource I found useful after installation was the IPFS tutorials [listed here](https://ipfs.io/docs/examples/), which show you the mechanics of IPFS and different use cases.

Also, Coral Health has written a good primer on how to use IPFS to [exchange encrypted files with someone](https://medium.com/@mycoralhealth/learn-to-securely-share-files-on-the-blockchain-with-ipfs-219ee47df54c). The tutorial combines both IPFS and [GNU Privacy Guard](https://www.gnupg.org/) for encrypting and decrypting files.

### Steps

I'm going to follow some broad steps in setting this up:

1. Add this blog to IPFS
2. Create a permanent top-level address (hash) for this blog using IPNS
3. Publish this blog on the internet via hosting and DNS

### Adding this blog to IPFS

This blog uses Hugo to generate static files so I have these files to add:

~~~bash
my_blog
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
ipfs add -r my_blog/
~~~

This recursively converts all files and subdirectories to hashes, adding them to IPFS:

~~~bash
added QmfLoX7TUHKWahmQK9zBmJSLmginoiUzCPWhT9ZsFoqn7u my_blog/archetypes/default.md
added QmbmhGjFGuu6FrXyKprVbperkuzVW8UNXbfb88pHogMJQw my_blog/config.toml
added Qmb3SuYbav8Kj6t9oVjGj832Uvu35CKNFC1iVK9JLLwXBy my_blog/content/_index.md
added QmZAPCrNEZ62ZrjcusznKaMMkMkXQ2TEBuHf3KpW5L4dkp my_blog/content/post/2018-06-27-first-look-ipfs.md
added QmeRWGwEohppNXdUxgn1E8Dy9RM8jFoyvJwveKem3BiqHT my_blog/content/post/2018-06-28-putting-blog-on-ipfs.md
added QmVMkg3C1kQ2Mcdz1sjLBWvQLPEXu7iHYJfYtewaALrgkY my_blog/static/css/theme-override.css
added QmaHnndJLrMjgyVF11vEryUj9KvZ4ENEia9MPt7uX5XFst my_blog/themes/hugo-classic/LICENSE.md
added QmRc7Teue2eDnyCAgAwpwpf5g7AiY98pmvuP7m3jKQYif2 my_blog/themes/hugo-classic/README.md
added QmcC419gL8J4RMPn8UV9F7aW2SDe7pYW5EXFrzafRnvqSy my_blog/themes/hugo-classic/archetypes/default.md
added QmUHd4GVD1dMzowp8bNnXHFvqW8SrFDkn7mUd1bFuqmhiL my_blog/themes/hugo-classic/exampleSite/config.toml
added QmNiRtJfJQaBJjFMxeytwJ61F4XUMVbAuFoY6sNGkZBsZv my_blog/themes/hugo-classic/exampleSite/content/_index.md
added QmXQBCG2vaoWYSKDZ1jotB5ryGszokjvGXmn7vovsMNDrk my_blog/themes/hugo-classic/exampleSite/content/post/2012-01-23-juicy-code.md
added QmQKHftTAtkdaBcUebfFjaXpv8c6VncRLSd6CovM5gWMSr my_blog/themes/hugo-classic/exampleSite/content/post/2012-04-23-hacker-with-horn.md
added QmNmu3Tms4VrN56vfcJmSe3hKBs29LpDTMGxtpf9pe6k9G my_blog/themes/hugo-classic/exampleSite/content/post/2015-07-23-command-line-awesomeness.md
added QmfBHr9jk4N3MXoDvWaTCTEeaMGMVSgyXQzCHEycYyH1GL my_blog/themes/hugo-classic/exampleSite/content/post/2016-02-14-markdown-guide.md
added QmVMkg3C1kQ2Mcdz1sjLBWvQLPEXu7iHYJfYtewaALrgkY my_blog/themes/hugo-classic/exampleSite/static/css/theme-override.css
added QmPBbTCuPcQH8osyNH8Mw6PQh44ezSnJiyoTvRyKKVNjFd my_blog/themes/hugo-classic/layouts/404.html
added QmTp9HkG7fpemRibMkywimkx6Hrt9uFUNrYW29a7chqqdi my_blog/themes/hugo-classic/layouts/_default/list.html
added QmSzixQ4DqhFD7gmwHxnZ6ceSmprJRCTHwdsc8pueUhzqR my_blog/themes/hugo-classic/layouts/_default/single.html
added QmcS3jbxuCXqPHFAnGs5F13EXUnSXHYvkpQs94UfErMsXY my_blog/themes/hugo-classic/layouts/_default/terms.html
added QmR6tt8iPfQbC8tBVC7VN9UNbPMy2tEZ14WHyhJfRwSkHF my_blog/themes/hugo-classic/layouts/partials/foot_custom.html
added QmbRCcKDkUibQY4iuxNaXFgMLykVaDFMSvQ7jCqYfL34Wo my_blog/themes/hugo-classic/layouts/partials/footer.html
added QmU13puBLEQKT7dgsjo2MTxETV2gPD4sBEn6FF82CUsDLG my_blog/themes/hugo-classic/layouts/partials/head_custom.html
added QmdrTkLkdR9hstWr5cngtTowVPx1efDYyyDaAAK8mBh3vv my_blog/themes/hugo-classic/layouts/partials/header.html
added QmRypkLZw1JL9Qb1cNTHasAvRsyrWGHJt8kUybmYiUsaX7 my_blog/themes/hugo-classic/static/css/fonts.css
added QmZ5amcnGzNuYB5rnd6HkeFHAUHzfeEL3UoytyDP7VdKkm my_blog/themes/hugo-classic/static/css/style.css
added QmTGNk3ACd1UnSru2ojjG7QK4HX1FPaUM3KfpT6SQcVDVr my_blog/themes/hugo-classic/theme.toml
added QmXQBCG2vaoWYSKDZ1jotB5ryGszokjvGXmn7vovsMNDrk my_blog/themes/hugo-classic/theme_posts/2012-01-23-juicy-code.md
added QmQKHftTAtkdaBcUebfFjaXpv8c6VncRLSd6CovM5gWMSr my_blog/themes/hugo-classic/theme_posts/2012-04-23-hacker-with-horn.md
added QmNmu3Tms4VrN56vfcJmSe3hKBs29LpDTMGxtpf9pe6k9G my_blog/themes/hugo-classic/theme_posts/2015-07-23-command-line-awesomeness.md
added QmfBHr9jk4N3MXoDvWaTCTEeaMGMVSgyXQzCHEycYyH1GL my_blog/themes/hugo-classic/theme_posts/2016-02-14-markdown-guide.md
added Qmd7a6si9AxwjWZf4fuEWVUxjJ9G9C5pWJh7a3SCc2qr6V my_blog/archetypes
added QmdNivpjNgtAPHRvwgUL2iSsw4vawNUbWiqwFgfK24AzTS my_blog/content/post
added Qmeab2t3kDSrtWwZw7YEA8NFMKg8A9KgiBJw9axLqABrmo my_blog/content
added QmUNLLsPACCz1vLxQVkXqqLX5R1X345qqfHbsf67hvA3Nn my_blog/data
added QmUNLLsPACCz1vLxQVkXqqLX5R1X345qqfHbsf67hvA3Nn my_blog/layouts
added QmNdeeHToTMRQRxPnSgZbJMm95jqAWwBUfR2bJQXKUvpVC my_blog/static/css
added QmUNLLsPACCz1vLxQVkXqqLX5R1X345qqfHbsf67hvA3Nn my_blog/static/img
added QmeR3BusgtxTXVivARRDu8fRSqLBBjQ6vruVAiqSizSAaj my_blog/static
added QmVP9ggRf3GGAseLrzUPoTkHDgwMwidMUpXpSFa6LfifzG my_blog/themes/hugo-classic/archetypes
added QmQ5j4tWQ6PCPZCRniL3cjkHnFGvjp5VbfjPy6YmDW3RrL my_blog/themes/hugo-classic/exampleSite/content/post
added Qmbw8hq5FZ8yHGcJ2Vhv9rpyV7494vaBvQKFzfVsRewAsw my_blog/themes/hugo-classic/exampleSite/content
added QmNdeeHToTMRQRxPnSgZbJMm95jqAWwBUfR2bJQXKUvpVC my_blog/themes/hugo-classic/exampleSite/static/css
added QmTQTecvCGKTxgjqsx3cew4AUuhKp7CRa7t4KB13gFN2kw my_blog/themes/hugo-classic/exampleSite/static
added QmfToyn26mcF2bHnbnHPWnWFJJf4vvnA5F9dSK1zSsbAik my_blog/themes/hugo-classic/exampleSite
added QmUNLLsPACCz1vLxQVkXqqLX5R1X345qqfHbsf67hvA3Nn my_blog/themes/hugo-classic/images
added QmeNvYxWp3d35Z2mcZoSoA4MZJHV1oMdxEvcYHwmtMcZaM my_blog/themes/hugo-classic/layouts/_default
added QmdqoPChpr1DagXYp7q1q1HY6rfcwA82XFD2UQWQ1bHvSh my_blog/themes/hugo-classic/layouts/partials
added Qmc4q3exZjNeZX3Uxb5v92rYZYRApNrFV6qnXCWidnXAgZ my_blog/themes/hugo-classic/layouts
added QmabZ344Vnamxxje9P6FpD7ee6j2cBqmGah5WMF9erVEeb my_blog/themes/hugo-classic/static/css
added Qmau5yWr9vLWQmEWNEgEByxeLHSG2w5i1ocX5sakEGEKwi my_blog/themes/hugo-classic/static
added QmQ5j4tWQ6PCPZCRniL3cjkHnFGvjp5VbfjPy6YmDW3RrL my_blog/themes/hugo-classic/theme_posts
added QmeTaM8URvA4D7UaBHDX4cxy9uNAbTxSgbxWg2TQGQ7hv5 my_blog/themes/hugo-classic
added QmeGQ6WF6cWgjTTinASM5Lpvg7aqYXkQESPAm1QwqjiuRB my_blog/themes
added Qmcn3JBpV6UshFgnUdWQgzzbhWdXqzRY8qoWmBMEpnGqGL my_blog
~~~

And voilà, the bottom, last hash represents the top-level folder, so we'll use that to access the site on IPFS. To do so, I could use either the local (node) or IPFS gateway respectively:

http://localhost:8080/ipfs/Qmcn3JBpV6UshFgnUdWQgzzbhWdXqzRY8qoWmBMEpnGqGL

https://gateway.ipfs.io/ipfs/Qmcn3JBpV6UshFgnUdWQgzzbhWdXqzRY8qoWmBMEpnGqGL

You see, IPFS comes with an HTTP gateway that queries the decentralized hash table with the hash you provide, in order to request it from your machine and then send it to your browser. Although there's some centralizaton involved, it makes it easier to access files.

There's a good explanation of how these IPFS gateways work in the [Decentralized Web Primer](https://dweb-primer.ipfs.io/avenues-for-access). In particular, I found [this explanation](https://dweb-primer.ipfs.io/classical-web/lessons/local-gateway.html) for the working of the HTTP gateway on the local node helpful:

> You can use a local IPFS node to read content from the worldwide IPFS network. The two ways of interacting with your local node are 1) through the command line and 2) through the HTTP gateway. You can use either of those interfaces to pass IPFS the content-addressed (hash) identifiers of the content you want. The IPFS node will use those identifiers to find that content on the network and retrieve it for you.

After adding the website to IPFS, entering a command such as the following should return the contents of that hash. Below, I use the `ipfs ls` command to list the contents of the top-level address for the blog.


~~~bash
$ ipfs ls Qmcn3JBpV6UshFgnUdWQgzzbhWdXqzRY8qoWmBMEpnGqGL
Qmd7a6si9AxwjWZf4fuEWVUxjJ9G9C5pWJh7a3SCc2qr6V 148   archetypes/
QmbmhGjFGuu6FrXyKprVbperkuzVW8UNXbfb88pHogMJQw 808   config.toml
Qmeab2t3kDSrtWwZw7YEA8NFMKg8A9KgiBJw9axLqABrmo 18813 content/
QmUNLLsPACCz1vLxQVkXqqLX5R1X345qqfHbsf67hvA3Nn 4     data/
QmUNLLsPACCz1vLxQVkXqqLX5R1X345qqfHbsf67hvA3Nn 4     layouts/
QmeR3BusgtxTXVivARRDu8fRSqLBBjQ6vruVAiqSizSAaj 221   static/
QmeGQ6WF6cWgjTTinASM5Lpvg7aqYXkQESPAm1QwqjiuRB 27553 themes/
~~~

### Getting a permanent address for this blog (in IPFS)

The thing is, every time I update my blog, the hashes for the respective files will change (the old hashes are still valid for previous versions of the content). What's needed is a DNS-like permanent pointer that enables everyone to access the blog. For that we'll use the [Interplanetary Naming System](https://ipfs.io/ipfs/QmNZiPk974vDsPmQii3YbrMKfi12KTSNM7XMiYyiea4VYZ/example#/ipfs/QmP8WUPq2braGQ8iZjJ6w9di6mzgoTWyRLayrMRjjDoyGr/ipns/readme.md).

~~~bash
$ ipfs name publish Qmcn3JBpV6UshFgnUdWQgzzbhWdXqzRY8qoWmBMEpnGqGL
Published to QmZUfPKG3B5D3QWRq4ytDHiUhJyFQE48avxpz6zGuZQe5f: /ipfs/Qmcn3JBpV6UshFgnUdWQgzzbhWdXqzRY8qoWmBMEpnGqGL
~~~

Here, I've supplied the hash of the `my_blog` folder, and can now give this hash to anyone who wants to access the blog.

In the line `Published to` above, the first hash is actually my peer ID, which was generated when I ran `ipfs init` back in the IPFS installation steps. Initializing an IPFS repo in such a way creates both a hash of my public key (this hash becomes my peer ID), as well as a private key (stored in `$HOME/.ipfs`).

For now on, I can also access my blog using the gateway:
https://gateway.ipfs.io/ipns/QmZUfPKG3B5D3QWRq4ytDHiUhJyFQE48avxpz6zGuZQe5f

Notice the hash provided is my peer ID. It should be mentioned that here, I'm publishing my site under my peer or node ID. This is fine for now if I have only one site, but what if I have several? Then I would generate a separate key for each site and publish under each key, as described in this [Reddit thread](https://www.reddit.com/r/ipfs/comments/74mur0/howto_putting_my_blog_on_ipfs/).

Actually let's try that:

~~~bash
$ ipfs key gen -t rsa -s 4096 my_blog
QmeeDDVNoHZkuweMbcBaiFqxwQNUr7RemgLHp6Zz8qx43S
$ ipfs key list -l
QmZUfPKG3B5D3QWRq4ytDHiUhJyFQE48avxpz6zGuZQe5f self
QmeeDDVNoHZkuweMbcBaiFqxwQNUr7RemgLHp6Zz8qx43S my_blog
~~~

The name of the key I just generated is `my_blog`, so we can publish the hash of the top folder to that key on IPNS:

~~~bash
$ ipfs name publish --key=my_blog Qmcn3JBpV6UshFgnUdWQgzzbhWdXqzRY8qoWmBMEpnGqGL
Published to QmeeDDVNoHZkuweMbcBaiFqxwQNUr7RemgLHp6Zz8qx43S: /ipfs/Qmcn3JBpV6UshFgnUdWQgzzbhWdXqzRY8qoWmBMEpnGqGL
~~~

There we go. The folder is now associated with the RSA key I just created. This seems somehow cleaner than referencing my blog with my peer ID of my local node.

### Issues with IPNS

It's not all roses though. When I afterwards ran `ipfs ls` on the public key I just created, it seemed to hang forever (running this on the original hash for my_blog produces the expected results howver).

Also, IPNS records [apparently expire](https://discuss.ipfs.io/t/ipfs-name-failing-to-resolve/1524/5) after every 24 hours, and if I don't run IPFS daemon they'll disappear entirely. This means that if I want to keep using IPNS, I will have to re-run the daemon, as well as re-run the `ipfs name publish` command on the public key.

