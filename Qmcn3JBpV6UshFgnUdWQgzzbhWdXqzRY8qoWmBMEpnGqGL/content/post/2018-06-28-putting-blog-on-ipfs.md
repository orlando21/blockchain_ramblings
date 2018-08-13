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
3. Publish this blog on the Internet via hosting and DNS

### Adding this blog to IPFS

This blog uses Hugo to generate static files so I have these files to add:

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
ipfs add -r my_blog/
~~~

This recursively converts all files and subdirectories to hashes, adding them to IPFS:

~~~bash
added QmfLoX7TUHKWahmQK9zBmJSLmginoiUzCPWhT9ZsFoqn7u blockchain_ramblings/archetypes/default.md
added QmbmhGjFGuu6FrXyKprVbperkuzVW8UNXbfb88pHogMJQw blockchain_ramblings/config.toml
added Qmdf2c9yVjKcahYKi2swFk6t8Hb8WKTwBpbWWo7NkgvYvm blockchain_ramblings/content/_index.md
added QmR73szm6dMCZUXtr55ZFA1PtQmi3KA3vURiJ8G46U6EA5 blockchain_ramblings/content/post/2018-06-27-first-look-ipfs.md
added QmXAJS9gVn41XuKVHvGdy5JRZkZEvtN8gBXujUudqgLC6X blockchain_ramblings/content/post/2018-06-28-putting-blog-on-ipfs.md
added QmVMkg3C1kQ2Mcdz1sjLBWvQLPEXu7iHYJfYtewaALrgkY blockchain_ramblings/static/css/theme-override.css
added QmaHnndJLrMjgyVF11vEryUj9KvZ4ENEia9MPt7uX5XFst blockchain_ramblings/themes/hugo-classic/LICENSE.md
added QmRc7Teue2eDnyCAgAwpwpf5g7AiY98pmvuP7m3jKQYif2 blockchain_ramblings/themes/hugo-classic/README.md
added QmcC419gL8J4RMPn8UV9F7aW2SDe7pYW5EXFrzafRnvqSy blockchain_ramblings/themes/hugo-classic/archetypes/default.md
added QmUHd4GVD1dMzowp8bNnXHFvqW8SrFDkn7mUd1bFuqmhiL blockchain_ramblings/themes/hugo-classic/exampleSite/config.toml
added QmNiRtJfJQaBJjFMxeytwJ61F4XUMVbAuFoY6sNGkZBsZv blockchain_ramblings/themes/hugo-classic/exampleSite/content/_index.md
added QmXQBCG2vaoWYSKDZ1jotB5ryGszokjvGXmn7vovsMNDrk blockchain_ramblings/themes/hugo-classic/exampleSite/content/post/2012-01-23-juicy-code.md
added QmQKHftTAtkdaBcUebfFjaXpv8c6VncRLSd6CovM5gWMSr blockchain_ramblings/themes/hugo-classic/exampleSite/content/post/2012-04-23-hacker-with-horn.md
added QmNmu3Tms4VrN56vfcJmSe3hKBs29LpDTMGxtpf9pe6k9G blockchain_ramblings/themes/hugo-classic/exampleSite/content/post/2015-07-23-command-line-awesomeness.md
added QmfBHr9jk4N3MXoDvWaTCTEeaMGMVSgyXQzCHEycYyH1GL blockchain_ramblings/themes/hugo-classic/exampleSite/content/post/2016-02-14-markdown-guide.md
added QmVMkg3C1kQ2Mcdz1sjLBWvQLPEXu7iHYJfYtewaALrgkY blockchain_ramblings/themes/hugo-classic/exampleSite/static/css/theme-override.css
added QmPBbTCuPcQH8osyNH8Mw6PQh44ezSnJiyoTvRyKKVNjFd blockchain_ramblings/themes/hugo-classic/layouts/404.html
added QmTp9HkG7fpemRibMkywimkx6Hrt9uFUNrYW29a7chqqdi blockchain_ramblings/themes/hugo-classic/layouts/_default/list.html
added QmSzixQ4DqhFD7gmwHxnZ6ceSmprJRCTHwdsc8pueUhzqR blockchain_ramblings/themes/hugo-classic/layouts/_default/single.html
added QmcS3jbxuCXqPHFAnGs5F13EXUnSXHYvkpQs94UfErMsXY blockchain_ramblings/themes/hugo-classic/layouts/_default/terms.html
added QmR6tt8iPfQbC8tBVC7VN9UNbPMy2tEZ14WHyhJfRwSkHF blockchain_ramblings/themes/hugo-classic/layouts/partials/foot_custom.html
added QmbRCcKDkUibQY4iuxNaXFgMLykVaDFMSvQ7jCqYfL34Wo blockchain_ramblings/themes/hugo-classic/layouts/partials/footer.html
added QmYCMa72detTpQ7gQdvjg3CXgzfAphhhWy3tVxRLbDdaiv blockchain_ramblings/themes/hugo-classic/layouts/partials/head_custom.html
added QmdrTkLkdR9hstWr5cngtTowVPx1efDYyyDaAAK8mBh3vv blockchain_ramblings/themes/hugo-classic/layouts/partials/header.html
added QmRypkLZw1JL9Qb1cNTHasAvRsyrWGHJt8kUybmYiUsaX7 blockchain_ramblings/themes/hugo-classic/static/css/fonts.css
added QmZ5amcnGzNuYB5rnd6HkeFHAUHzfeEL3UoytyDP7VdKkm blockchain_ramblings/themes/hugo-classic/static/css/style.css
added QmTGNk3ACd1UnSru2ojjG7QK4HX1FPaUM3KfpT6SQcVDVr blockchain_ramblings/themes/hugo-classic/theme.toml
added QmXQBCG2vaoWYSKDZ1jotB5ryGszokjvGXmn7vovsMNDrk blockchain_ramblings/themes/hugo-classic/theme_posts/2012-01-23-juicy-code.md
added QmQKHftTAtkdaBcUebfFjaXpv8c6VncRLSd6CovM5gWMSr blockchain_ramblings/themes/hugo-classic/theme_posts/2012-04-23-hacker-with-horn.md
added QmNmu3Tms4VrN56vfcJmSe3hKBs29LpDTMGxtpf9pe6k9G blockchain_ramblings/themes/hugo-classic/theme_posts/2015-07-23-command-line-awesomeness.md
added QmfBHr9jk4N3MXoDvWaTCTEeaMGMVSgyXQzCHEycYyH1GL blockchain_ramblings/themes/hugo-classic/theme_posts/2016-02-14-markdown-guide.md
added Qmd7a6si9AxwjWZf4fuEWVUxjJ9G9C5pWJh7a3SCc2qr6V blockchain_ramblings/archetypes
added QmVjE4KDgkQAj6zSJVNo7ZbUFfHLNp1MnaxzLi27iiHVZc blockchain_ramblings/content/post
added QmUm4PwagiF9tBqSvzG4TtaFmNEyMqwTPcDKiKTNMLBeVF blockchain_ramblings/content
added QmUNLLsPACCz1vLxQVkXqqLX5R1X345qqfHbsf67hvA3Nn blockchain_ramblings/data
added QmUNLLsPACCz1vLxQVkXqqLX5R1X345qqfHbsf67hvA3Nn blockchain_ramblings/layouts
added QmNdeeHToTMRQRxPnSgZbJMm95jqAWwBUfR2bJQXKUvpVC blockchain_ramblings/static/css
added QmTQTecvCGKTxgjqsx3cew4AUuhKp7CRa7t4KB13gFN2kw blockchain_ramblings/static
added QmVP9ggRf3GGAseLrzUPoTkHDgwMwidMUpXpSFa6LfifzG blockchain_ramblings/themes/hugo-classic/archetypes
added QmQ5j4tWQ6PCPZCRniL3cjkHnFGvjp5VbfjPy6YmDW3RrL blockchain_ramblings/themes/hugo-classic/exampleSite/content/post
added Qmbw8hq5FZ8yHGcJ2Vhv9rpyV7494vaBvQKFzfVsRewAsw blockchain_ramblings/themes/hugo-classic/exampleSite/content
added QmNdeeHToTMRQRxPnSgZbJMm95jqAWwBUfR2bJQXKUvpVC blockchain_ramblings/themes/hugo-classic/exampleSite/static/css
added QmTQTecvCGKTxgjqsx3cew4AUuhKp7CRa7t4KB13gFN2kw blockchain_ramblings/themes/hugo-classic/exampleSite/static
added QmfToyn26mcF2bHnbnHPWnWFJJf4vvnA5F9dSK1zSsbAik blockchain_ramblings/themes/hugo-classic/exampleSite
added QmUNLLsPACCz1vLxQVkXqqLX5R1X345qqfHbsf67hvA3Nn blockchain_ramblings/themes/hugo-classic/images
added QmeNvYxWp3d35Z2mcZoSoA4MZJHV1oMdxEvcYHwmtMcZaM blockchain_ramblings/themes/hugo-classic/layouts/_default
added QmcAn7t8mQQNBGXiP59F1J6XXYHTiMqCm2egbz3P252tiT blockchain_ramblings/themes/hugo-classic/layouts/partials
added QmcVN12QYRnmbXvRxvSn51wticmgqLC54QsksvmLo7FLTy blockchain_ramblings/themes/hugo-classic/layouts
added QmabZ344Vnamxxje9P6FpD7ee6j2cBqmGah5WMF9erVEeb blockchain_ramblings/themes/hugo-classic/static/css
added Qmau5yWr9vLWQmEWNEgEByxeLHSG2w5i1ocX5sakEGEKwi blockchain_ramblings/themes/hugo-classic/static
added QmQ5j4tWQ6PCPZCRniL3cjkHnFGvjp5VbfjPy6YmDW3RrL blockchain_ramblings/themes/hugo-classic/theme_posts
added QmSGVn8rN7WZUtzSrV2GYw4M3xBxfMkvhzF1Eg13kaLFUu blockchain_ramblings/themes/hugo-classic
added QmRocSmG3kiwo6wR9c3Z2n7t2oDrw7aSmo2eZPbiXnvsHP blockchain_ramblings/themes
added QmU97CACrFytZop1st1i9RvSaAJrXqepqXRkBaMLhqmZBG blockchain_ramblings
~~~

And voilà, the bottom, last hash represents the top-level folder, so we'll use that to access the site on IPFS. To do so, I could use either the local (node) or IPFS gateway respectively:

http://localhost:8080/ipfs/QmU97CACrFytZop1st1i9RvSaAJrXqepqXRkBaMLhqmZBG

https://gateway.ipfs.io/ipfs/QmU97CACrFytZop1st1i9RvSaAJrXqepqXRkBaMLhqmZBG

You see, IPFS comes with an HTTP gateway that queries the decentralized hash table with the hash you provide, in order to request it from your machine and then send it to your browser. Although there's some centralizaton involved, it makes it easier to access files.

There's a good explanation of how these IPFS gateways work in the [Decentralized Web Primer](https://dweb-primer.ipfs.io/avenues-for-access). In particular, I found [this explanation](https://dweb-primer.ipfs.io/classical-web/lessons/local-gateway.html) for the working of the HTTP gateway on the local node helpful:

> You can use a local IPFS node to read content from the worldwide IPFS network. The two ways of interacting with your local node are 1) through the command line and 2) through the HTTP gateway. You can use either of those interfaces to pass IPFS the content-addressed (hash) identifiers of the content you want. The IPFS node will use those identifiers to find that content on the network and retrieve it for you.




~~~bash

~~~


