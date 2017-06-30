---
layout: post
title: "Why can't we store data on the Ethereum blockchain?"
permalink: /eth-storage
---

Ethereum presents a number of challenges to developers, not least of which is the fundamental difference between programming for a shared virtual computer versus, say, some high-powered machine in the cloud.  Indeed, beyond the fact that Ethereum is effectively a distributed computer, we also must contend with the vast limitations of that machine.  It's common to hear the comparison that Ethereum is effectively as powerful as a Commodore 64, and that may not be far from the truth.

One of the challenges of working with this platform is simple data storage.  In typical environments, devs can practically treat data storage as an unlimited resource:  Storage is *cheap*.  It's commonly stated that data storage can't work on-chain, but why is that?  The answer lies in the [Ethereum Yellow Paper](https://ethereum.github.io/yellowpaper/paper.pdf).

The yellow paper includes a specification of the underlying Ethereum virtual machine, including the gas fee associated with each specific opcode.  The fees are described in Appendix G in a table titled Fee Schedule.  The opcode we're concerned with is `SSTORE`, the operation through which a "storage value is set to non-zero from zero."  (Note that `SSTORE` stores data to storage, while `MSTORE` stores data to memory.  In the EVM, "storage" is analagous to a system's hard drive, while "memory" is analagous to its RAM).  We see that the gas fee associated with the operation is 20,000.

How much data can be stored with the `SSTORE` operation for this 20,000 gas fee?  The table on Page 24 titled "Stack, Memory, Storage, and Flow Operations" describes each of the opcodes in more detail.  We can see in the description that `SSTORE` stores a single *word* to storage (like most opcodes of this type).  In this case, a *word* is a unit of data whose size is fixed for easy handling by the processor.  Page 10 reveals, "the word size of the machine... is 256-bit."  That is, each word in the EVM is a 256-bit, or 8-byte, piece of data.

Now we know it costs 20,000 gas to store a single 8-byte piece of data.  Let's put that into perspective:

Gas price is variable, but let's assume a relatively thrifty 10 Gwei per gas (you are setting your own gas prices, right?).  ETH is currently hovering around $50, so that 8-byte piece of data costs `20,000 gas * (10 * 10^-9 ETH/gas) * (50 USD/1 ETH)` = 0.01 USD per 8-byte word.  That's 1.25 USD per kilobyte, and 1,250 USD per megabyte.  For a single gigabyte of storage, you can expect to pay *1,250,000 USD*.

Why can't we store data on-chain?  We can, the only thing stopping you is astronomical expense compared to every other option under the sun.  This is why we resort to clever solutions, like storing the bulk data off-chain and hashes of the data on-chain, allowing users to easily verify the integrity of the data without actually paying the massive costs of storing on the blockchain itself.  

*EDIT:  With ETH now around 300 USD (June 30), the figures above can be updated as follows:

1 KB = 7.50 USD
1 MB = 7,500 USD
1 GB = 7,500,000 USD
