---
layout: post
title: "DRAFT: Securely Transferring your ETH Off an Exchange (When a Hardware Wallet Isn't an Option)"
permalink: /paper-wallet
---

Storing large amounts of ETH on an exchange [is problematic](https://medium.com/@CodyBrown/how-to-lose-8k-worth-of-bitcoin-in-15-minutes-with-verizon-and-coinbase-com-ba75fb8d0bac).  With the rising value of ETH, it becomes more and more dangerous to store even small amounts on an exchange.  The most secure solution is to transfer your cryptocurrency to a hardware wallet.  Unfortunately, the Ethereum community's preferred hardware wallet, the [Ledger Nano S](https://www.ledgerwallet.com/products/12-ledger-nano-s), currently suffers a shipping time of over *two months* after placing your order.  Two months is a long time to leave your ETH on an exchange.

Assuming the proper steps are taken during creation, paper wallets can be nearly as secure (though less convenient) than a hardware wallet.  Most importantly, they require no special hardware, and they allow you to transfer your ETH off of an exchange *right now*.  Ultimately, I suggest storing any large amounts of cryptocurrency on a hardware wallet, but this guide will help you stay secure in the meantime.

*DISCLAIMER*:  This is crypto, and you are responsible for your own actions.  If you make a mistake, you might burn all of your ETH.  Depending on your level of confidence, it may be less risky to simply leave your ETH on an exchange.  I suggest reading through and [grokking](https://en.wikipedia.org/wiki/Grok) the entire guide before trying any of this.  It would be best to first run through the entire process on the testnet, or with only a negligible amount of ETH on mainnet, to ensure that you're not making a mistake along the way.

# Overview

1. Download & install Tails to a live USB.  Download Ian Coleman's BIP39 keypair generation tool and include this on the live USB.
2. Boot into Tails and generate a new 24-word mnemonic, keypair, and address.
3. Write this information on paper, quadruple-checking to ensure correctness.
4. Transfer ETH from exchange to this newly generated wallet.

# Gather Your Tools

## Create a Tails Live USB

One of the goals in the creation of a cold storage paper wallet is to generate a new private key that *never* touches the internet.  In the case of a paper wallet, we can also ensure that the private key does not persist on any electronic device, greatly minimizing our [attack surface](https://en.wikipedia.org/wiki/Attack_surface).

Your primary OS might sound like a fine environment for generating a new private key, but it's difficult to ensure it hasn't already been compromised by some malicious actor.  Instead, we will boot into [Tails](https://tails.boum.org), "The Amnesic Incognito Live System."  Tails boots directly from a live USB and the OS only touches your machine's RAM.  This ensures that there is no chance of your new keys being accidentally persisted on the host machine or the USB drive itself:  When Tails shuts down, all of the data loaded into RAM is lost.  Your host machine's hard drive and the USB device will remain exactly as they were before key generation.

Go ahead and follow the [Tails installation guide](https://tails.boum.org/install/index.en.html).  By the end, you should have a live USB from which you can boot directly into Tails.

## Download a BIP39 Keypair Generator

For key generation, we'll use [Ian Coleman's open-source BIP39 Tool](https://github.com/iancoleman/bip39).  Importantly, this tool can be run offline and will generate a BIP39 mnemonic, in addition to the corresponding private/public keypair and the public address.  The BIP39 mnemonic does not offer additional security over a raw keypair, but it does offer convenience:  The 24 words can be easily written and verified, unlike the raw keys and address.  This offers additional assurance that we won't make a mistake while writing our paper wallet. 

Go ahead and download the tool.  If you're familiar with the command line and Javascript, I suggest reviewing the source code (located in `src/`) to your satisfaction and compiling with `python compile.py`.  Otherwise, you can show your trust in Mr. Coleman and the community behind him by simply downloading the compiled .html file [here](https://github.com/iancoleman/bip39/blob/master/bip39-standalone.html).  Whichever you choose, place the `bip39-standalone.html` file on the live USB (TODO:  Where?).

# Enter Your Secure Environment

Have you got your tinfoil hat?  Good.  Turn your phone off (in fact, just leave it in another room), tape over any webcams in the room, throw your Amazon Echo in the dumpster (forever).  Tails won't automatically connect to a network unless it detects a wired connection, but why risk it?  Unplug all wired network connections and, if you're able, remove the wifi card from your computer.

Boot into Tails (the process for doing so is detailed in their installation guide).

# Generate & Record the Mnemonic, Keypair, and Address

Execute the `bip39-standalone.html` file.  This will open your web browser, but have no fear, it's simply serving the .html file from the USB drive, not via a network connection.

1. Next to "Generate a random mnemonic," select "24" words from the dropdown and click the "Generate" button.
    a.  For extra security, you may provide your own entropy before generation, rather than relying on the built-in random number generator.  As stated by the tool, this is an advanced feature and can be misused.  A well-shuffled deck of cards is a good source, and inputting each of the 52 cards' values as you draw them is more than enough entropy.

2. Next to "Coin," select "Ethereum" from the dropdown.  This configures the tool to use the standard Ethereum BIP39 derivation path `m/44'/60'/0'/0`. This standard is used across any (decent) wallet, ensuring that you can easily import your keys to another wallet via the BIP39 mnemonic.

3. Write down your BIP39 Mnemonic, shown in the "Mnemonic" section.  Write down the first address, public key, and private key listed in the Derived Addresses section (it's listed next to the `m/44'/0'/0'/0/0` path).  QUADRUPLE check that you've written the mnemonic, the keypair, and the address correctly.

4. Say your prayers, take your vitamins, and transfer your ETH from the exchange to the newly-generated address.  Your paper wallet is complete.

# How to Recover ETH from Your New Paper Wallet

When you're ready to to transfer your ETH to a hardware wallet, simply choose to import a wallet via the BIP39 mnemonic.  Type your 24-word phrase into the device, and your wallet is now ready for use.  If, for whatever reason, your wallet doesn't import correctly (i.e. you didn't copy the mnemonic correctly), you may also import via the raw private key.
