---
title: Some details of IPFS
author: Greg Babb
date: '2018-08-10'
categories:
  - File storage
slug: details-of-ipfs
---

The concepts behind IPFS are explained at length in the [whitepaper](https://ipfs.io/ipfs/QmR7GSQM93Cx5eAg6a6yRzNde1FQv7uL6X1o4k7zrJa3LX/ipfs.draft3.pdf) but I just want to cover some of its highlights here. I won't go into these in too much detail -- the whitepaper, along with plenty of other sources would provide better descriptions of these concepts.

### Distributed hash tables (DHTs)

The white paper lays out a concept for a routing system that can "find (a) other peers' network addresses and (b) peers who can serve particular objects." This routing system is based on various flavors of hash tables (key, value pairs -- where a key is the hash over the content, and a value can be either the content of the block itself, or a reference to the node ID containing the content in case of larger file sizes) that are distributed on the vast, peer-to-peer network of IPFS. That is, each node in the network contributes to the distributed hash table that is used to find the location of a given block of content.

This [Wikipedia article](https://en.wikipedia.org/wiki/Distributed_hash_table) has a good description of distributed hash tables in general.

The whitepaper describes several implementations of DHT, all of which IPFS uses: Kademlia, Coral DSHT, and S/Kademlia.

IPFS offers a number of commands to directly query or write to the DHT, all beginning with `ipfs dht`:

- `ipfs dht findpeer`
- `ipfs dht findprovs`
- `ipfs dht get`
- `ipfs dht provide`
- `ipfs dht put`
- `ipfs dht query`

IPFS' DHT works with a messaging system to alert other nodes of new data in order to ensure efficient routing and location of content among the nodes.

### BitTorrent

For exchanging data (blocks) among nodes, IPFS makes use of a customized version of BitTorrent. We've all heard of BitTorrent in the context of downloading movies from the web, but IPFS uses it to organize a big swarm of peers and enforce file sharing rules.

According to the IPFS whitepaper, its flavor of BitTorrent data exchange protocol (referred to as "BitSwap") has two main features -- both of which being standard BitTorrent features apparently:

- It uses a "quasi tit-for-tat strategy that rewards nodes who contribute to each other, and punishes nodes who only leech others' resources."
- Its peers track "the availability of file pieces, prioritizing sending rarest pieces first."

All of this comes together to create a network that shares content while being resilient against abuse. BitSwap implements a credit and debit system, based on past data exchanges, to decide who shares which content.

There are even protocols that implement cryptocurrencies (such as [Filecoin](https://filecoin.io/)) to optimize file sharing in alternative ways.

### Version control

Some people have called IPFS "git for the Web," and this point is easily seen as IPFS implements the Git protocol, which incorporates "a powerful Merkle DAG object model that captures changes to a filesystem tree in a distributed friendly way" as the IPFS whitepaper puts it.

What does this mean? Again, quoting the whitepaper:

>1. Immutable objects represent Files (blob), Directories
(tree), and Changes (commit).
2. Objects are content-addressed, by the cryptographic
hash of their contents.
3. Links to other objects are embedded, forming a Merkle
DAG. This provides many useful integrity and workflow
properties.
4. Most versioning metadata (branches, tags, etc.) are
simply pointer references, and thus inexpensive to create
and update.
5. Version changes only update references or add objects.
6. Distributing version changes to other users is simply
transferring objects and updating remote references.

[This thread](https://github.com/jbenet/random-ideas/issues/20) gives a simplified description of the Merkle DAG implemented in IPFS, though one can peruse other sources to get finer details.

With git version control, IPFS keeps track of both changes in content as well as the locations (hashes) of each version of changed content.

Currently though, it seems versioning has not yet been fully implemented and is a [work in progress](https://gist.github.com/flyingzumwalt/a6821e843366d606aeb1ba53525b8669).

### Self-certified filesystems (SFS)

The naming system of IPFS -- IPNS -- is implemented via SFS. This allows users to generate an address for a remote filesystem in such a way that they can verify the address' validity. Per the whitepaper: "The user can verify the public key offered by the server, negotiate a shared secret, and secure all traffic. All SFS instances share a global namespace where name allocation is cryptographic, not gated by any centralized body."

The name allocation is cryptographic to allow verification and prevent imposter nodes from showing up and claiming they're legitimate.

SFS creates a system of pointers to these cryptographic addresses to content, much as git creates branches and tags, and these pointers are updated to reflect new content (addresses). In this way, the content remains immutable, while the pointers can represent the latest version of the content.

This ties into IPNS, as the content that the top-level IPNS address (root address of a node) points to gets updated when you publish an IPFS object to this address.

### IPFS design

IPFS is designed as a peer-to-peer system with no privileged nodes. It incorporates a protocol stack of sub-protocols handling the following aspects (descriptions taken from the whitepaper):

- Identities -- manage node identity generation and verification.
- Network -- manages connections to other peers, uses
various underlying network protocols.
- Routing -- maintains information to locate specific
peers and objects. Responds to both local and remote
queries. Defaults to a DHT, but is swappable.
- Exchange -- a novel block exchange protocol (BitSwap)
that governs efficient block distribution. Modelled as
a market, weakly incentivizes data replication. Trade
Strategies swappable.
- Objects -- a Merkle DAG of content-addressed immutable
objects with links. Note this layer of the stack is (or will be) implemented by [IPLD](https://ipld.io/). Used to represent arbitrary
datastructures, e.g. file hierarchies and communication
systems.
- Files -- versioned file system hierarchy inspired by Git.
- Naming -- a self-certifying mutable name system.


