# The Bitcoin hardware wallet industrial debacle

This blog post is about the catastrophic outcome of a particular widespread mainstream delusional belief: 

    The belief that the use of a Bitcoin hardware wallet increases the security of your coins.

It almost never will. On the contrary, your situation is more likely going to degenerate into a fully-fledged security nightmare.

## 1. The reproducible-build software engineering standard is not optional

>[reproducible-builds.org](https://reproducible-builds.org/)  
>
> Reproducible builds. Why does it matter?
>
> Whilst   anyone may inspect the source code of free and open source software  for  malicious flaws, most software is distributed pre-compiled with no   method to confirm whether they correspond.  
>  
>This   incentivises attacks on developers who release software, not only via traditional exploitation, but also in the forms of political influence,   blackmail or even threats of violence.

The wallet application, and the operating system on which it runs, must be reproducible-build, turtles all the way down. The hardware wallet's firmware must also be reproducable-build, for exactly the same reasons.


## 2. A hardware wallet is an strong attack magnet

Billions of dollars are at stake. Attackers will try to abscond with funds stored in hardware wallets by subverting its firmware with malware.

In theory, the Trezor hardware wallet comes preinstalled with reproducable-build firmware. Other hardware wallets do not even satisfy the requirements of the reproducible-build software engineering standard.

The user would have to verify upon arrival of the shipment of his hardware wallet that the firmware was not tampered with during production or shipping, by running the commands mentioned in the following page:

https://wiki.trezor.io/Developers_guide:Deterministic_firmware_build

Since the user will almost surely not take the effort to do that, there is no guarantee that his Trezor wallet will contain the uncorrupted reproducible-build firmware.

Given this reality, hardware wallets are a wholly unsuitable approach to the Bitcoin storage security problem except for the technically most savvy and sophisticated users. For ordinary users, hardware wallets must be considered to be a dangerous ambush.


## 3. Alternative to hardware wallets

The only software solution that currently satisfies the requirements of the reproducible-build standard are either:

1. Electrum
2. Bitcoin Core Qt

Running on either:

1. Debian
2. Linux Mint Debian Edition (LMDE)
3. Tails
4. Linux Arch
5. Linux Alpine

Example installation instructions for Debian-based distros:

```
$ sudo apt-get install electrum
```

>[https://packages.debian.org/sid/utils/electrum](https://packages.debian.org/sid/utils/electrum)  
>Package: electrum (4.0.2-2)  
>Easy to use Bitcoin client
>This   package provides a lightweight Bitcoin client which protects you from   losing your bitcoins in a backup mistake or computer failure. Also,   Electrum does not require waiting time because it does not download the   Bitcoin blockchain.


## 4. The use of a hardware wallet could literally constitute a death warrant for its users

[Crypto Wallet Provider Ledger Hacked: Customer Database Said to be Compromised](https://www.crowdfundinsider.com/2020/12/170498-crypto-wallet-provider-ledger-hacked-customer-database-said-to-be-compromised)

>December  21, 2020. Ledger stated yesterday that they have been alerted to the  dump of a customer database on Raidforum. Ledger reports more than 1.5  million wallets have been sold since 2014.

This  could clearly result in a good number of impromptu house visits, torture  fests, and resulting dead bodies, i.e. the notorious [$5 wrench attack](https://cryptosec.info/wrench-attack). There are people who kill other people for substantially less money than that. They may even liberally torture your wife and children before your eyes until you reveal the hardware wallet's password.


## 5. Mitigation strategy for Ledger victims

What can you do, if you happen to be one of the 1.5 million people at risk in the Ledger debacle?

First of all, the attacker will try to figure out which targets are worth visiting.

Therefore, the attacker will use social-media and other sources for indications of wealth. The idea will probably be that a wealthy person will most likely have invested in a larger amount of Bitcoins than a poorer one. Therefore, one solution consists in removing all online data that suggests wealth.

Secondly, it could be a solution to move.

If you no longer live at the address leaked, the attackers may not bother to figure out where you have moved. In the new location, you may want to rent or buy under a different name than the one that was leaked.


## 6. The KYC (Know Your Customer) regulations are a time bomb for users' personal security

The same problem occurs for customers of bitcoin exchange platforms such as Coinbase. What if that database gotleaked? In fact, what if the IRS' Bitcoin capital-gains tax database got leaked? Depending on how well their infrastructure happens to be secure or not, we may end up prematurely saying farewell to more than one person.


## 7. How to avoid a KYC-related $5 wrench attack?

You can avoid the $5 wrench-attack problem by avoiding KYC. In the following link, you can find a list of peer-to-peer exchanges that do not collect personally identifying data:

https://kycnot.me

So, good luck to everyone who may need it, now or in the future!

