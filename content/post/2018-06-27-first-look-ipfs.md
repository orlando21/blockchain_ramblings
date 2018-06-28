---
title: A first look at IPFS
author: Greg Babb
date: '2018-06-27'
categories:
  - File storage
slug: first-look-at-ipfs
---

I have often read of bitcoin's blockchain as being inherently unscalable, with transactions needing around 12 minutes to settle, and in some cases much longer. Although you can apparently use this blockchain for file storage, waiting so long to access your files can be a bummer.

This might also be because the network was [not intended](https://bitcoin.stackexchange.com/questions/32253/how-does-a-blockchain-store-any-data) for file storage in the first place (e.g., max block size being 1MB).

### Decentralized file storage

The idea is to create a file storage system that is similarly decentralized as the blockchain is, where content is also encrypted and where it's basically broken up into little pieces ("sharded") and stored on the computers of other network participants.

In this way, bringing down one node (such as your computer) won't mean you've lost your content. In fact, these bits are often copied and recopied on different computers for redundancy - although in IPFS' case, your content [just might get lost if it's unpopular](https://groups.google.com/forum/#!topic/ipfs-users/J0ns9RVzQi4).

Furthermore, by encrypting your content with [GNU Privacy Guard](https://en.wikipedia.org/wiki/GNU_Privacy_Guard) or similar encryption software, you also get a good dose of security and privacy.

The above implies you're basically storing your files on the decentralized network and they are not meant to be shared with anyone else. But you can also put files out there to share with some specific person by encrypting these with the person's public key. And vice versa if they want to share something with you.

For me, all this implies either complete privacy or one-to-one sharing. But what if you want to share your content with several people, i.e., certain people but not everyone? On this issue my research has unfortunately come up with nothing satisfactory at this time.

Another question is, how can you mesh a decentralized file storage scheme with a given blockchain? One way of doing it sounds quite easy with [this example](https://ethereum.stackexchange.com/questions/7664/how-can-we-integrate-ipfs-with-ethereum-in-dapps): If you are storing, say, a contract on the Ethereum blockchain, you can insert links to related content stored on IPFS directly into that contract. In the case of IPFS, such links would be expressed as hashes (more on that below).

### What is IPFS?

Let's first discuss what IPFS is, and then what it isn't. According to [Wikipedia](https://en.wikipedia.org/wiki/InterPlanetary_File_System), the InterPlanetary File System:

> is a protocol and network designed to create a content-addressable, peer-to-peer method of storing and sharing hypermedia in a distributed file system.

It's basically peer-to-peer sharing of files (like Bittorrent). IPFS however uses [Bitswap](https://github.com/ipfs/go-ipfs/tree/master/exchange/bitswap) for managing the requesting and sending of content blocks.

IPFS is also a distributed hash table (DHT) that stores the locations of each block as a unique cryptographic hash of the content itself. The entire DHT is implemented as a direct acyclic graph (DAG) called a "Merkle DAG," and IPFS traverses this graph to find and resolve hashes (retrieve content it's looking for).

An example of another application using Merkle DAG is GitHub, which allows users to duplicate and edit multiple versions of a file, store those versions and later merge edits with the original file.

So how does IPFS implement versioning? In my short experience with IPFS, it seems that users won't explicitly specify version numbers per se, but instead simply update the content to generate a different hash number pointing to that content. There's a good explanation of content and hash updating in a tutorial named ["Decentralized Web Primer."](https://flyingzumwalt.gitbooks.io/decentralized-web-primer/content/files-on-ipfs/lessons/add-and-retrieve-file-content.html)

(You might be thinking at this point, "how will people find my content if I update it?" as the hash pointing to your content will change. Something called "IPNS" solves this, which we'll cover later.)

What IPFS is not: it's not a distributed ledger like bitcoin that permanently stores your content in the cloud; there's no blockchain involved. There are ways to store your content more or less permanently, which involve either "pinning" your content in your own permanently online host (pinning avoids it from getting garbage collected), or having other people pin your content (i.e., it becomes popular).

### Why I've chosen to play with IPFS

For sure there are other protocols for decentralized file hosting out there, like [Storj](https://storj.io/), [SIA](https://sia.tech/), and [MaidSafe](https://maidsafe.net/), among others. IPFS seems to be quite prevalent and it's open source. It's also supported by [Filecoin](https://filecoin.io/), which I want to look further into.

Another interesting idea is [BockchainDB](https://www.bigchaindb.com/), a MongoDB-based decentralized storage database that uses a NoSQL query language. Wow. I definitely will bookmark this and look at it later.

For now I'm focusing on IPFS and will start my small project to put this blog on it.

