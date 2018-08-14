---
title: Getting this blog on IPFS
author: Greg Babb
date: '2018-06-28'
categories:
  - File storage
slug: putting-blog-on-ipfs
---

Enough of preliminaries, let's get this party started! We're going to use [IPFS](https://github.com/ipfs/ipfs) for what it was made: to store some content.

The first thing I did was to head over to the [IPFS home page](https://ipfs.io/) and install it on my Macbook. There, IPFS concepts are clearly explained and I'd recommend watching the [demo video](https://youtu.be/8CMxDNuuAiQ) to get started.

The first version of IPFS was written in the Go language, so I'm going with that and installing Go on my Mac as a prerequisite (I know, that sounds arbitrary!). I'm not going to cover the install steps for IPFS here as it's [adequately done elsewhere](https://ipfs.io/docs/install/). One resource I found useful after installation was the IPFS tutorials [listed here](https://ipfs.io/docs/examples/), which show you the mechanics of IPFS and different use cases.

Also, Coral Health has written a good primer on how to use IPFS to [exchange encrypted files with someone](https://medium.com/@mycoralhealth/learn-to-securely-share-files-on-the-blockchain-with-ipfs-219ee47df54c). The tutorial combines both IPFS and [GNU Privacy Guard](https://www.gnupg.org/) for encrypting and decrypting files.

### Steps

I'm going to follow some broad steps in setting this up:

1. Add this blog to IPFS
2. Create a permanent top-level address (hash) for this blog using IPNS
3. Publish this blog on the Internet via hosting and DNS

### Adding this blog to IPFS

This blog uses Hugo to generate static files so I should add the generated files in the `./public` subdirectory:

~~~bash
public
.
├── 404.html
├── categories
│   ├── file-storage
│   │   ├── index.html
│   │   └── index.xml
│   ├── index.html
│   └── index.xml
├── css
│   ├── fonts.css
│   ├── style.css
│   └── theme-override.css
├── img
├── index.html
├── index.xml
├── post
│   ├── 2018
│   │   ├── 06
│   │   │   ├── 27
│   │   │   │   └── first-look-at-ipfs
│   │   │   │       └── index.html
│   │   │   └── 28
│   │   │       └── putting-blog-on-ipfs
│   │   │           └── index.html
│   │   └── 08
│   │       └── 10
│   │           └── details-of-ipfs
│   │               └── index.html
│   ├── index.html
│   └── index.xml
├── sitemap.xml
└── tags
    ├── index.html
    └── index.xml
~~~

The command to add a directory with files and subfolders to IPFS is:

~~~bash
ipfs add -r public
~~~

This recursively converts all files and subdirectories to hashes, adding them to IPFS:

~~~bash
added QmVedFEQrND4Nr8w8ELFDLoPuXupc6FkEM821XJ7x3JdmR public/404.html
added QmbEX1G6EYdhkPiPsjTtHXeSVuDWq7nEyrbLyHNuGJyUkL public/categories/file-storage/index.html
added QmU6UnRCunGvWdYBuA5hpWGNcydngGDtGFLfaEqFaTDJ6v public/categories/file-storage/index.xml
added QmfGbdxwHCbABj3AzUZi8RZbCS2ccDr64YH3EFh4yxK6jU public/categories/index.html
added QmTnowVWaPRYgygE2jLpvdqfcqZfuAEwZ89WPRHQJgqUPF public/categories/index.xml
added QmRypkLZw1JL9Qb1cNTHasAvRsyrWGHJt8kUybmYiUsaX7 public/css/fonts.css
added QmZ5amcnGzNuYB5rnd6HkeFHAUHzfeEL3UoytyDP7VdKkm public/css/style.css
added QmVMkg3C1kQ2Mcdz1sjLBWvQLPEXu7iHYJfYtewaALrgkY public/css/theme-override.css
added QmX5YyE9CuyGpAzsy6iMaiRGsqDJWGBKURxLqF7zs4jjog public/index.html
added QmQkDmVgXRdQEs3Wo7nUqt14k7U4jRBUrKKrUWRK7TXzRT public/index.xml
added QmXWvtwnHD479kQMGMq3XKyqCFWLkLKe9pF9tWZRCqLNXh public/post/2018/06/27/first-look-at-ipfs/index.html
added QmYBVTXdUJ8MkhLxCyfupMTKnbLySMxjiecEuNz9aFGont public/post/2018/06/28/putting-blog-on-ipfs/index.html
added QmPTft89CFjMnRSV7aK6L3NWjuni7opH1cgvQNPmid8bWN public/post/2018/08/10/details-of-ipfs/index.html
added QmQx4L8o8bMR3HMajTRxrZWZFRaUDfZRvQGfXc2S2Pe5Ng public/post/index.html
added QmYokEVQHEtoT9mxwZM8ntja1TKM5Z37uyZqbVeZHK3k7r public/post/index.xml
added QmTG3i4Lob16YL6QhEHDnTzHw3pgiCKjBdbPvhhQe4msLF public/sitemap.xml
added QmPBHbuXfTjTdcnF4pHPQf1LUC4N8W2hx3XpKi5otju3Wp public/tags/index.html
added QmTSiCVPdFgtrnohx11XFuAijMJ9xUBFk8npsV9tqbAFzm public/tags/index.xml
added QmVqEtdPjTELYgZNfFUKHqXszULxd78r6hADq2zpv5Wfda public/categories/file-storage
added QmbmVetF6DYv4nKog5oujYtdpRu64FZyMt9DHGkjKonQiL public/categories
added QmcbY2JVo4WD8pW7UQYUiqCPHuqWk1Paix3ES8mkwnTsAc public/css
added QmUNLLsPACCz1vLxQVkXqqLX5R1X345qqfHbsf67hvA3Nn public/img
added QmVdP1zMMevZRqJ2681CxTSJ4hoSWhKSxEHp19kRHoZR84 public/post/2018/06/27/first-look-at-ipfs
added QmeTssqiHTa6kz3eFYQDQdUHpNybydCoJ1urXT18DSmMtu public/post/2018/06/27
added QmUWp3zdAfvDekXSJgSWympRNXyqdgj8hLDsX3nTndetrT public/post/2018/06/28/putting-blog-on-ipfs
added QmYGd4M1LQ47zDs4TpoE6GoCzX854emM5soxuKPjGMpvVL public/post/2018/06/28
added QmahRqby8utv2zyZxDN8PavjwUTKayg2YVYHPNFgaUMJG5 public/post/2018/06
added QmUe6qURFEj85K8YZUeSXXrDKtVnJ6Z7yob839qKFPduvx public/post/2018/08/10/details-of-ipfs
added QmNYKQCKfMuGtoWBiZNEpyLDT8GoQKdi6ntXTGM3DsKsco public/post/2018/08/10
added QmcJ3Tes4UGPHwUoBL498GYk7pwgeWguusyHRuFhUG7RmT public/post/2018/08
added QmbBSN441bGFjwm12qf2WaBa4uscf3uXh1G9diNPkqrgUV public/post/2018
added QmQ3kxAqPHtYQ9Ke4v3ftoNTdpzrvSa7uQMNaho1NPzcyD public/post
added QmeMuCYFVF7fTPJRAZgQLS8PX9Xjcj4Ytni63B8BcK8Z7X public/tags
added QmU6U2YsxY3Ebs87mzeh2ztRbkEXtGsR3UiVMUWpLnzPML public
~~~

And voilà, the bottom, last hash represents the top-level folder, so we'll use that to access the site on IPFS. To do so, I could use either the local (node) or IPFS gateway respectively:

http://localhost:8080/ipfs/QmU6U2YsxY3Ebs87mzeh2ztRbkEXtGsR3UiVMUWpLnzPML

https://gateway.ipfs.io/ipfs/QmU6U2YsxY3Ebs87mzeh2ztRbkEXtGsR3UiVMUWpLnzPML

You see, IPFS comes with an HTTP gateway that queries the decentralized hash table with the hash you provide, in order to request it from your machine and then send it to your browser. Although there's some centralizaton involved, it makes it easier to access files.

There's a good explanation of how these IPFS gateways work in the [Decentralized Web Primer](https://dweb-primer.ipfs.io/avenues-for-access). In particular, I found [this explanation](https://dweb-primer.ipfs.io/classical-web/lessons/local-gateway.html) for the working of the HTTP gateway on the local node helpful:

> You can use a local IPFS node to read content from the worldwide IPFS network. The two ways of interacting with your local node are 1) through the command line and 2) through the HTTP gateway. You can use either of those interfaces to pass IPFS the content-addressed (hash) identifiers of the content you want. The IPFS node will use those identifiers to find that content on the network and retrieve it for you.

After adding the website to IPFS, entering a command such as the following should return the contents of that hash. Below, I use the `ipfs ls` command to list the contents of the top-level address for the blog.


~~~bash
$ ipfs ls QmU6U2YsxY3Ebs87mzeh2ztRbkEXtGsR3UiVMUWpLnzPML
QmVedFEQrND4Nr8w8ELFDLoPuXupc6FkEM821XJ7x3JdmR 1995  404.html
QmbmVetF6DYv4nKog5oujYtdpRu64FZyMt9DHGkjKonQiL 8730  categories/
QmcbY2JVo4WD8pW7UQYUiqCPHuqWk1Paix3ES8mkwnTsAc 2416  css/
QmUNLLsPACCz1vLxQVkXqqLX5R1X345qqfHbsf67hvA3Nn 4     img/
QmX5YyE9CuyGpAzsy6iMaiRGsqDJWGBKURxLqF7zs4jjog 4329  index.html
QmQkDmVgXRdQEs3Wo7nUqt14k7U4jRBUrKKrUWRK7TXzRT 3053  index.xml
QmQ3kxAqPHtYQ9Ke4v3ftoNTdpzrvSa7uQMNaho1NPzcyD 43956 post/
QmTG3i4Lob16YL6QhEHDnTzHw3pgiCKjBdbPvhhQe4msLF 1033  sitemap.xml
QmeMuCYFVF7fTPJRAZgQLS8PX9Xjcj4Ytni63B8BcK8Z7X 2584  tags/
~~~

### Getting a semi-permanent address for this blog (in IPFS)

The thing is, every time I update my blog, the hashes for the respective files (blocks) will change -- the old hashes are still valid for previous versions of the content. What's needed is a DNS-like permanent pointer that enables everyone to access the blog. For that we'll use the [Interplanetary Naming System](https://ipfs.io/ipfs/QmNZiPk974vDsPmQii3YbrMKfi12KTSNM7XMiYyiea4VYZ/example#/ipfs/QmP8WUPq2braGQ8iZjJ6w9di6mzgoTWyRLayrMRjjDoyGr/ipns/readme.md).

~~~bash
$ ipfs name publish QmU6U2YsxY3Ebs87mzeh2ztRbkEXtGsR3UiVMUWpLnzPML
Published to QmZUfPKG3B5D3QWRq4ytDHiUhJyFQE48avxpz6zGuZQe5f: /ipfs/QmU6U2YsxY3Ebs87mzeh2ztRbkEXtGsR3UiVMUWpLnzPML
~~~

Here, I've supplied the hash of the `public` folder, which is published to my IPFS peer ID (`QmZUfPKG3B5D3QWRq4ytDHiUhJyFQE48avxpz6zGuZQe5f` -- that was generated when I first ran `ipfs init` back in the IPFS installation steps). Running `ipfs init` creates both a hash of my public key (this hash becomes my peer ID), as well as a private key (stored in `$HOME/.ipfs`).

For now on, I can also access the files of my blog using the gateway:
https://gateway.ipfs.io/ipns/QmZUfPKG3B5D3QWRq4ytDHiUhJyFQE48avxpz6zGuZQe5f

This is fine for now if I have only one site, but what if I want to publish several sites to one node? Then I would generate a separate key for each site and publish under each key, as described in this [Reddit thread](https://www.reddit.com/r/ipfs/comments/74mur0/howto_putting_my_blog_on_ipfs/).

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
$ ipfs name publish --key=my_blog QmU6U2YsxY3Ebs87mzeh2ztRbkEXtGsR3UiVMUWpLnzPML
Published to QmeeDDVNoHZkuweMbcBaiFqxwQNUr7RemgLHp6Zz8qx43S: /ipfs/QmU6U2YsxY3Ebs87mzeh2ztRbkEXtGsR3UiVMUWpLnzPML
~~~

There we go. The folder is now associated with the RSA key I just created. This seems somehow cleaner than referencing my blog with my peer ID of my local node.

### Issues with IPNS

It's not all roses though. When I afterwards ran `ipfs ls` on the public key I just created, it seemed to hang forever (running this on the original hash for my_blog produces the expected results however -- it seems this product is still in Alpha phase).

Also, IPNS records [apparently expire](https://discuss.ipfs.io/t/ipfs-name-failing-to-resolve/1524/5) after every 24 hours, and if I don't keep the IPFS daemon locally they'll disappear entirely. This means that if I want to keep using IPNS, I will have to re-run the daemon, as well as re-run the `ipfs name publish` command on the public key.

Therefore if you can't find the files of this blog at:
https://gateway.ipfs.io/ipns/QmeeDDVNoHZkuweMbcBaiFqxwQNUr7RemgLHp6Zz8qx43S (just-generated public key)...

...it's a safer bet you can find them using my peer ID: https://gateway.ipfs.io/ipns/QmZUfPKG3B5D3QWRq4ytDHiUhJyFQE48avxpz6zGuZQe5f

### Linking IPNS to DNS

If I wanted to take out a dedicated domain name for this blog (especially for a human-readable domain name rather than an ugly IPNS hash), I could go through the regular motions of buying a domain name but then link this domain to IPNS.

To do so, I would add a TXT record in DNS that contains a [dnslink](https://github.com/ipfs/go-dnslink) to have the blog domain name point to the published IPNS hash. You can find an example of this [here](https://blog.de-swaef.eu/using-ipfs-to-host-your-dapp/).

### A web GUI for IPFS

I should also mention that the webUI ([http://localhost:5001/webui](http://localhost:5001/webui)) also provides some useful information at a glance, such as your peer ID and related network addresses in the swarm.

**Note**: You must have `ipfs daemon` running to view the webUI.

**Up next**: [Some details of IPFS](https://frozen-oasis-28875.herokuapp.com/post/2018/08/10/details-of-ipfs)
