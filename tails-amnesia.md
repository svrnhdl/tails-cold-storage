Welcome to the tails-cold-storage wiki!

# Introduction
In this guide we will create a cold storage Bitcoin wallet using Tails. Tails is a live operating system that you can start on almost any computer from a USB stick or a DVD.

Before you start creating your keys, read through the entire guide first. If you have any questions you can ask them through 'Issues'. In no way, am I responsible for anything that might go wrong with your cold storage.

# Requirements

* 1 Computer
* 1 USB stick
* 1 Extra backup device (USB, SD-card, ...)
* Dice (6-sided) for generating entropy

Ideally, the computer has the wifi-adapter and hard-drive physically removed. Make sure you trust the hardware you are using to generate your wallet. If you don't know how to remove the wifi-adapter, search around on YouTube for video's on how to replace it for your specific computer model. If you don't have an old laptop or computer lying around, you may also use your normal computer.

# Tails
## Description
> Tails is a live operating system that you can start on almost any computer from a USB stick or a DVD.
>
> It aims at preserving your privacy and anonymity, and helps you to:
> * use the Internet anonymously and circumvent censorship;
> * all connections to the Internet are forced to go through the Tor network;
> * leave no trace on the computer you are using unless you ask it explicitly;
> * use state-of-the-art cryptographic tools to encrypt your files, emails and instant messaging.

[Source](https://tails.boum.org/index.en.html)

## Installation
To install Tails OS, follow the steps on [this page](https://tails.boum.org/install/index.en.html). Alternatively, ask a friend [to clone the installation](https://tails.boum.org/install/win/clone-overview/index.en.html) on your USB.

Starting Tails can be tricky sometimes on certain computer models. You need to tell the computer to boot from the USB stick. This can be chosen during the boot-up by pressing F2 or F10 (but this varies greatly by computer models). Refer to [this page](https://tails.boum.org/install/win/usb/index.en.html#start-tails) for more information or if you are experiencing issue when starting tails.

## Persistent storage
> If you start Tails from a USB stick, you can create a persistent volume in the free space left on the USB stick. The files in the persistent volume are saved encrypted and remain available across separate working sessions.
>
> You can use this persistent volume to store any of the following:
> * Personal files
> * Some settings
> * Additional software
> * Encryption keys
> 
> The persistent volume is an encrypted partition protected by a passphrase.
> 
> Once the persistent volume is created, you can choose to activate it or not each time you start Tails. 

[Source](https://tails.boum.org/doc/first_steps/persistence/index.en.html)

When you succeed in booting up the operating system from the USB, you will be presented with the Tails Greeter. At this point, you need to chose if you want to use the persistent storage feature or not. 

If you don't use this, you will have to re-create your wallet with your backed-up seed whenever you want to do an outgoing transaction (or alternatively, you can sweep the entire wallet when you want to spend your coins).

If you decide to enable the persistent storage, a copy of the wallet (including the seed) will be kept in the encrypted volume of your USB stick. This way, you don't need to access the seed whenever you want to do an outgoing transaction. This is more similar to the experience of using an air-gapped hardware wallet.

![Tails Greeter](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/tails-greeter.png)

Since we won't be using the persistence feature in this guide, you can simply start Tails. If you are using a computer that still has a wifi-card or has a wired connection to the internet, make sure to DISABLE ALL NETWORKING in the Tails Greeter.

# Creating a wallet
## Air-gapped cold storage wallet
You should now have a trusted computer and a trusted Tails OS on USB.

Tails OS (version 4.1) has Electrum wallet installed by default. To create a wallet, follow these steps:
* Start Electrum in Tails
[insert picture]

* Press Ctrl+N to create a new wallet.

![Create a new wallet](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/tails-create.png)

* Select 'Standard wallet'

![Select type of wallet: Standard wallet](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/tails-standard.png)

* Select 'Create a new seed'

![Create a new seed](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/tails-seed.png)

* Select 'Segwit'

![Select Segwit](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/tails-segwit.png)

* Electrum returns 12 words that represent a mnemmonic device for your seed. 

Now that we have generated a seed, it is time to think about how we want to back-up this seed.

## Generating entropy
In the next step, we will need a strong passphrase to encrypt the mnemmonic seed phrase for our backup.

To get an idea of what a strong passphrase is, you can check out [this page](https://coldbit.com/can-bip-39-passphrase-be-cracked/). For the purpose of this guide, we will use the ['EFF Diceware Short Wordlist'](https://www.eff.org/files/2016/09/08/eff_short_wordlist_1.txt).

Ideally, you want to be using **casino-grade** dice for generating entropy. Roll 4 dice on a fair surface and read the word from the printed wordlist. Write the word down carefully and continue until you have sufficient entropy. For instance, if you roll '1111', you write down 'acid' from the list.

**I recommend using at least six words from the short wordlist**. This corresponds to 1296^6 combinations or 62 bits of entropy.

## Backup Seed
This guide will use 2 backup methods. You may choose to use both or use only one, depending on your preference for storing the backups and your personal considerations regarding their trade-offs.

Backup #1
* Open a text editor
* Copy the 12 words into the editor
* Confirm the 12 words in the Electrum Install Wizard.
* There is no need to encrypt the Electrum wallet file since we are not using the persistence feature. Tails will forget everything that you did during this session.
* Your seed should still be in the clipboard. Select 'Encrypt Clipboard with Passphrase'
* Enter a passphrase. This need not be the same passphrase as your persistent volume above (but it can be).
* Confirm the passphrase
* Select the seed in the text editor and paste your clipboard. Your file should now contain a passphrase-encrypted PGP message.
* Save the file into your extra backup device (USB #2, SD-card, ...)

Backup #2
* Write down the 12 words on paper. You can also stamp or engrave your seed phrase in metal for durability.

That's it. We now have multiple ways of recovering our coins:
* Backup #2: a clear-text copy of your mnemmonic. **Anyone who has access to these words has access to your coins.**
* Backup #1: a passphrase-encrypted file that contains a clear-text copy of your mnemmonic. **Anyone who has access to the storage device AND the passphrase has access to your coins.**

Finally, it's time to set up a wallet on our normal computer that we can use to generate addresses and transactions that does NOT contain the seed (private keys).

## Watch-only wallet
Next, save the master key of your wallet onto the extra backup device. This needn't be encrypted but this information is sensitive in the sense of your personal privacy. **Anyone with this master key can track the balances of your wallet.**

If you are running Tails on a seperate computer, you can plug in the device into your normal computer or laptop. If you are using your normal computer for Tails, verify that you have correctly backed up your seed and restart your PC with your normal operating system. Mind that Tails will forget everything you did during this session.

If you saved the master key of your wallet, you may create a watch-only wallet on a second computer.
* Open Electrum
* Create New Wallet (Ctrl+N)
* Give your wallet a good name

* Select option 1: 'Standard wallet'

![Select standard wallet](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/win-standard.png)

* Select option 3: 'Use a master key'

![Select 'Use a master key'](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/win-masterkey.png)

* Copy the master key from your extra backup device into the dialog box. Press 'Next'

![Watch-only wallet - insert zpub](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/win-zpub.png)

* Optionally, encrypt the local wallet file with a password (recommended)

![Succesfully created a watch only wallet](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/win-watchonly.png)

IMPORTANT: 

Run your own node and connect Electrum to this node (preferably over Tor)

If you connect to public Electrum servers (the default behavior) then you are giving away your master key to strangers. This means they can trivially track your balances and link this back to your IP address.

# Test your wallet
If you decided not to use the persistent storage and you already restarted your Tails OS, you will need to create a new wallet and import the seed words again. This is not recommended.

* Send a small transaction to an address in your wallet and wait for confirmation. You can do this on both the offline computer as from the watch-only wallets. Compare the addresses on both wallets, they should be identical.

![Unconfirmed transaction in the mempool...](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/tails-texttx.png)

* From your watch-only wallet, construct a Bitcoin transaction from the received funds after it is confirmed on the blockchain. Depending on your fee and the traffic on the network, this can take a few hours.

![Watch-only wallet - spend from wallet](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/win-spendfrom.png)

* Export the transaction to an empty USB-stick or SD-card. We are creating a transaction on your normal computer and transfer the transaction in a file to the offline machine.

* Back on your Tails OS, open the wallet (that contains your seed) from the persistent storage and go to 'Tools > Load transaction > From file'
* Sign the transaction

![Sign and Export your transaction](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/tails-signtx.png)
* Export the transaction back to the USB-stick or SD-card.
* Back on your regular PC, from your watch-only wallet, load the signed transaction from file.

![Watch-only wallet - load transaction](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/win-loadtx.png)

* Broadcast your transaction to the network. Preferably this is done with your own personal node using Tor.

![Broadcast transaction](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/win-broadcast.png)

# Store your backups
