---
layout: post
title: "Foundational Research for Understanding & Contextualizing Ethereum"
permalink: /eth-research
---

In my time studying Ethereum, I've found that there's a relative lack of solid technical resources covering the technology.  This is especially unfortunate when you consider just how technical and nuanced the topic can get.  What follows is a reasonable reading list for bootstrapping your knowledge of blockchain technology and Ethereum, in particular.  The list assumes a relatively technical reader, but all of the papers listed are quite approachable (except perhaps the Ethereum Yellow Paper AKA The Crypto-currency-nomicon).

## Fundamental Topics

### Protocols for Public Key Cryptosystems

*Ralph Merkle*

[http://www.merkle.com/papers/Protocols.pdf](http://www.merkle.com/papers/Protocols.pdf)

Public key cryptography is the fundamental innovation enabling trustless communications without reliance on a central authority.  This form of cryptography is so foundational that it has become part of the fabric of modern secure digital communications.  In this paper, Ralph Merkle, inventor of the technique (and of [Merkle trees](https://en.wikipedia.org/wiki/Merkle_tree), another important concept for blockchains), offers a survey of public key techniques, making this a great starting reference for future research into the topic.

### Byzantine Consensus in Asynchronous Message-Passing Systems: a Survey

*Miguel Correia, Giuliana Santos Veronese, Nuno Ferreira Neves and Paulo Verissimo*

[http://www.gsd.inesc-id.pt/~mpc/pubs/survey-ba-journal-formated.pdf](http://www.gsd.inesc-id.pt/~mpc/pubs/survey-ba-journal-formated.pdf)

Consensus is a tough problem even in the best of conditions.  When you introduce the challenges of distributed systems, especially the inevitable asynchronicity of communications, you get a problem that has challenged researchers for many years.  "Byzantine consensus" is a model of distributed consensus based on an abstraction called the "[Byzantine Generals' Problem](https://en.wikipedia.org/wiki/Byzantine_fault_tolerance#Byzantine_Generals.27_Problem)."  The BGP models distributed consensus in the presence of any numbers of unknown, arbitrary faults.  This may include anything from simple communication problems between network nodes, observational inconsistencies between observing nodes, and even untrustworthy actors "breaking the rules" by working against the consensus network.  This paper, like Merkle's above, offers a survey of the existing research in Byzantine consensus, and should given the reader an idea of the challenges associated with designing an effective distributed consensus network.

### The Sybil Attack

*John R. Douceur*

[http://nakamotoinstitute.org/static/docs/the-sybil-attack.pdf](http://www.gsd.inesc-id.pt/~mpc/pubs/survey-ba-journal-formated.pdf)

A Sybil attack is an instance of a single antagonist subverting a peer-to-peer network by creating a large number of identities with which to gain disproportionate influence over the network.  Sybil attacks are among the most common, simplest attacks against decentralized networks of all kinds, and Ethereum is no different.  In his paper, Douceur formalizes the concept of Sybil attacks and describes why they are an inevitable characteristic of peer-to-peer networks.  As is the case with Byzantine fault tolerance, understanding Sybil attacks is an important aspect of designing functional distributed consensus systems.

## History

### b-money

*Wei Dai*

[http://www.weidai.com/bmoney.txt](http://www.gsd.inesc-id.pt/~mpc/pubs/survey-ba-journal-formated.pdf)

Ethereum White Paper:  "Wei Dai's b-money became the first proposal to introduce the idea of creating money through solving computational puzzles as well as decentralized consensus, but the proposal was scant on details as to how decentralized consensus could actually be implemented."

### Reusable Proofs of Work

*Hal Finney*

[http://nakamotoinstitute.org/finney/rpow/index.html](http://nakamotoinstitute.org/finney/rpow/index.html)

Ethereum White Paper:  "In 2005, Hal Finney introduced a concept of "reusable proofs of work", a system which uses ideas from b-money together with Adam Back's computationally difficult Hashcash puzzles to create a concept for a cryptocurrency, but once again fell short of the ideal by relying on trusted computing as a backend."

### Bitcoin:  A Peer-to-Peer Electronic Cash System

*Satoshi Nakamoto*

[https://bitcoin.org/bitcoin.pdf](https://bitcoin.org/bitcoin.pdf)

Satoshi Nakamoto built the first successful cryptocurrency by uniting the ideas of his predecessors:  Ralph Merkle's public key cryptography, Wei Dai's concept of decentralized consensus-based currency, and Ralph Finney's proofs of work.  Ethereum largely builds on the foundation laid by Bitcoin and extends it to a greater degree of complexity with the introduction of a distributed runtime.  Coming to grips with the relatively-simpler Bitcoin network is a great stepping stone towards understanding Ethereum.

### Formalizing and Securing Relationships on Public Networks

*Nick Szabo*

[http://nakamotoinstitute.org/formalizing-securing-relationships/](http://nakamotoinstitute.org/formalizing-securing-relationships/)

This is Nick Szabo in his element: fusing expertise in economics, political theory, and technology to create the concept of autonomous actors capable of formalizing business relationships, even going so far as to become extensions of contractual law, themselves (though this is still debated).  This early concept of smart contracts is still highly relevant in the modern Ethereum ecosystem.

## Ethereum: The Present & Future

### Ethereum White Paper

[https://github.com/ethereum/wiki/wiki/White-Paper](https://github.com/ethereum/wiki/wiki/White-Paper)

The Ethereum White Paper is a somewhat high-level overview of Ethereum, including (importantly) the vision of the project.  It touches on the most foundational technical underpinnings of Ethereum without getting bogged down in the implementation details, which makes this a great read for a reasonably technical reader who's interested in the project.

### Ethereum Yellow Paper

*Gavin Wood*

[https://ethereum.github.io/yellowpaper/paper.pdf](https://ethereum.github.io/yellowpaper/paper.pdf)

While the Ethereum White Paper is a moderately-technical treatment of the topic, the Ethereum Yellow Paper is the nitty-gritty specification of the nuts and bolts.  Gavin Wood describes, in great detail, each of the constituent elements of the Ethereum network, including a specification for the Ethereum virtual machine.  This is the reference by which Ethereum node software like Geth is written.  Of all of the papers in this list, this is probably the most challenging:  The math is rigorous, the material is dense, and Gavin leaves no stone unturned.  It's a notoriously difficult paper, but it's the most concentrated source of knowledge on Ethereum's underpinnings.

I found these two images from a [Stack Exchange thread](source: https://ethereum.stackexchange.com/questions/268/ethereum-block-architecture) extremely helpful in my understanding of Ethereum's architecture:

1. [Overall architecture](https://i.stack.imgur.com/afWDt.jpg) 
2. [Ethereum's Modified Merkle-Patricia-Tries](https://i.stack.imgur.com/afWDt.jpg)

### Proof of Stake

[https://github.com/ethereum/wiki/wiki/Proof-of-Stake-FAQ](https://github.com/ethereum/wiki/wiki/Proof-of-Stake-FAQ)

Proof of Work has proven effective at establishing consensus in a trustless distributed network. However, as networks like Bitcoin and Ethereum scale, it's become clear that PoW has some problems, especially with regard to energy consumption and centralization concerns (e.g. mining pools).  Proof of Stake, a leading theoretical alternative to PoW-based consensus, alleviates these problems (to some extent), but the jury is still out on how exactly to implement such a system, especially with regard to the "[nothing at stake](https://en.wikipedia.org/wiki/Proof-of-stake#Criticism)" problem.  Ethereum's proposed PoS algorithm, Casper, is planned to replace its PoW algorithm some time in the near future, so understanding the proposal is an important part of understanding Ethereum's future.

### Sharding

[https://github.com/ethereum/wiki/wiki/Sharding-FAQ](https://github.com/ethereum/wiki/wiki/Sharding-FAQ)

As alluded to above, scaling is a yet-unsolved problem that faces all growing blockchains.  Bitcoin's continued problems with network congestion and rising transaction fees are, in part, scaling problems.  The Ethereum Foundation has its eyes to the future, and has already begun research into a reliable means of scaling Ethereum to meet future transactional loads.  Currently, each node on the Ethereum network is verifying and propagating the transactions of the *entire* network.  The concept of sharding, on the other hand, involves splitting the network into individual sub-networks, such that each node is only responsible for a subset of the network's transactions.  The research into this topic is still early, but the Sharding FAQ offers a great mix of high-level concepts and technical discussion.
