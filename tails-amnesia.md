Tails cold storage guide without persistence volume.

# Introduction
In this guide we will create a Bitcoin wallet generated on an offline Tails USB stick. [Tails](https://tails.boum.org/) is a live operating system that you can start on any computer from a USB stick or a DVD.

Before you start creating your keys, read through the entire guide first. If you have any questions you can ask them via 'Issues'. In no way, am I responsible for anything that might go wrong with your cold storage. Securing your keys is your personal responsibility.

# Requirements

* 1 Computer
* 1 USB stick (min. 8GB)
* 1 Extra storage device (USB, SD-card, ...)
* Dice (6-sided) for generating entropy

Ideally, the computer is an old laptop that has the wifi-adapter and hard-drive physically removed. Make sure you trust the hardware you are using to generate your wallet. If you don't know how to remove the wifi-adapter, search around on YouTube for video's on how to replace it for your specific computer model. If you don't have an old laptop or computer lying around, you may also use your normal computer (not recommended).

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
To install Tails OS, follow the steps on [this page](https://tails.boum.org/install/index.en.html). Alternatively, ask a friend [to clone his installation](https://tails.boum.org/install/win/clone-overview/index.en.html) onto your USB.

Starting Tails can be tricky sometimes on certain computer models. You need to tell the computer to boot from USB. This can be chosen during the boot-up by pressing F2 or F10 (but this varies greatly by computer models). Refer to [this page](https://tails.boum.org/install/win/usb/index.en.html#start-tails) for more information or if you are experiencing issue when starting tails.

## Persistent storage
When you succeed in booting up the operating system from the USB, you will be presented with the Tails Greeter.

![Tails Greeter](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/tails-greeter.png)

At this point, you need to chose if you want to use the persistent storage feature or not. If you don't use this, you will have to re-create a wallet with your backed-up seed whenever you want to do an outgoing transaction (or alternatively, you can sweep the entire wallet when you want to spend your coins). If you decide to enable the persistent storage, a copy of the wallet (including the seed) will be kept in an encrypted volume of your USB stick. This way, you don't need to access the backed-up seed whenever you want to do an outgoing transaction. This is more similar to the experience of using an air-gapped hardware wallet. If you want to use the persistence feature, check out the other guide [here](https://github.com/SovereignNode/tails-cold-storage/blob/master/tails-persistence.md).

Since we won't be using the persistence feature in this guide, you can simply press 'Start Tails' and continue with this guide.

Important notes:
* If you are using a computer that still has a wifi-card or has a wired connection to the internet, make sure to **disable all networking** in the Tails Greeter by pressing on the '+' button under 'Additional settings' (option 3).
* If you are not used to the American keyboard layout, it could be worthwile to select your preferred layout.

# Creating a wallet
## Air-gapped cold storage wallet
You should now have a trusted computer and a trusted Tails OS on USB that is not connected to the internet.

Tails OS (version 4.1) has [Electrum wallet](https://electrum.org/#home) installed by default. To create a wallet, follow these steps:

* Start Electrum in Tails (Applications > Internet > Electrum Bitcoin Wallet)

![Start Electrum](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/start_electrum.png)

* Tails will give you a warning message stating that the persistence is disabled. Launch anyway.

![Tails warning](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/electrum_persistence_disabled.png)

* Enter a name for your wallet (not very important as the wallet will be deleted upon restart of Tails)

![Create a new wallet](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/electrum_new_wallet.png)

* Select 'Standard wallet'

![Select type of wallet: Standard wallet](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/electrum_standard.png)

* Select 'Create a new seed'

![Create a new seed](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/electrum_new_seed.png)

* Select 'Segwit'

![Select Segwit](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/electrum_segwit.png)

* Electrum returns 12 words that represent a mnemmonic device for your seed. 

![Receive mnemmonic seed phrase](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/electrum_wallet_seed.png)

Now that we have generated a seed, it is time to think about how we want to back-up this seed.

## Generating entropy
In the next step, we will need a strong passphrase to encrypt the mnemmonic seed phrase for our backup. To get an idea of what a strong passphrase is, you can check out [this page](https://coldbit.com/can-bip-39-passphrase-be-cracked/). For the purpose of this guide, we will use the ['EFF Diceware Short Wordlist'](https://www.eff.org/files/2016/09/08/eff_short_wordlist_1.txt).

Ideally, you want to be using **casino-grade** dice for generating entropy. Roll 4 dice on a fair surface and read the word from the printed wordlist. Write the word down carefully and continue until you have sufficient entropy. For instance, if you roll '1111', you write down 'acid' from the list. **I recommend using at least six words from the short wordlist**. This corresponds to 1296^6 combinations or 62 bits of entropy.

**IMPORTANT:** If you did not change the language and region settings in the Greeter, be careful when you type your passphrase in the next step. This is important for users who are used to different keyboard layouts for typing (like AZERTY).

## Backup Seed
This guide will use 2 backup methods. You may choose to use both or use only one, depending on your preference for storing the backups and your personal considerations regarding their trade-offs.

**Backup #1**
* Write down the 12 words on paper. You can also stamp or engrave your seed phrase in metal for durability.

**Backup #2**
* Open a text editor

![Open text editor](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/tails_open_text_editor.png)

* Copy the 12 words into the editor

![Copy seed in editor](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/tails_clipboard_seed.png)

* Confirm the 12 words in the Electrum Install Wizard.

![Confirm seed](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/electrum_confirm_seed.png)

* There is no need to encrypt the Electrum wallet file since we are not using the persistence feature. Tails will forget everything that you did during this session.

![Encrypt wallet file](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/electrum_encrypt_wallet.png)

* Back in the text editor click anywhere and press `Ctrl+A` and `Ctrl+C`.
* Select 'Encrypt Clipboard with Passphrase'

![Encrypt clipboard](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/tails_encrypt_clipboard.png)

* Enter your passphrase.

![Enter passphrase](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/tails_enter_passphrase.png)

* Confirm your passphrase

![Confirm passphrase](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/tails_confirm_passphrase.png)

* Paste your clipboard (press `Ctrl + V`) into the text editor (replacing the clear-text seed phrase). Your file should now contain a passphrase-encrypted PGP message.

![Paste encrypted](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/tails_paste_encrypted.png)

* Save the file onto your `extra backup device` (USB #2, SD-card, ...)


That's it. We now have multiple ways of recovering our coins:
* Backup #1: a clear-text copy of your mnemmonic. **Anyone who has access to these words has access to your coins.**
* Backup #2: a passphrase-encrypted file that contains a clear-text copy of your mnemmonic. **Anyone who has access to the storage device AND the passphrase has access to your coins.**

Finally, it's time to set up a wallet on our normal computer that we can use to generate addresses and transactions that does NOT contain the seed (private keys).

## Watch-only wallet
Next, save the master key of your wallet onto the `extra backup device`. This needn't be encrypted but this information is sensitive in the sense of privacy. **Anyone with this master key can track the balances of your wallet.**

* In Electrum, go to 'Wallet > Information'.

![Find wallet information](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/electrum_save_masterkey.png)

* Copy the `master public key`.

![Copy master public key](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/electrum_save_zpub.png)

* Open a new text editor and paste the `master public key`.

![Paste the master public key](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/tails_save_masterkey2.png)

If you are running Tails on a seperate computer, you can plug the `extra backup device` into your normal computer or laptop. If you are using your normal computer for starting Tails, verify that you have correctly backed up your seed and restart your PC with your normal operating system. Mind that Tails will forget everything you did during this session. This means that you will be unable to do a test transaction for your wallet without importing your seed backup into a new wallet after restarting. **To properly test your wallet setup, you will need two separate computers.**

If you saved the master key of your wallet, you may create a watch-only wallet on a second computer. To install Electrum, [click here](https://electrum.org/#download).

* Open Electrum
* Create New Wallet (Ctrl+N)
* Give your wallet a good name

![Name your wallet](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/win-new_watch_only_wallet.png)

* Select option 1: 'Standard wallet'

![Select standard wallet](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/win-standard.png)

* Select option 3: 'Use a master key'

![Select 'Use a master key'](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/win-masterkey.png)

* Copy the master key from your extra backup device into the dialog box. Press 'Next'

![Watch-only wallet - insert zpub](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/win-zpub.png)

* Optionally, encrypt the local wallet file with a password (recommended)

![Succesfully created a watch only wallet](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/win-watchonly.png)

IMPORTANT: 

If you connect to public Electrum servers (the default behavior) then you are giving away your master key to strangers. This means that they can trivially track your balances and link this back to your IP address. You are giving away your privacy by doing this.

**Run your own node** and connect Electrum to this node (preferably over Tor).

* [Bitcoin.org - Running a full node](https://bitcoin.org/en/full-node)
* [Bitembassy - Home node](https://github.com/bitembassy/home-node/blob/master/README.md) - Advanced
* [Mynodebtc](https://mynodebtc.com/) - Advanced
* [Nodl.it](https://www.nodl.it/) - Expensive
* [Casa node](https://store.casa/lightning-node/)

# Test your wallet
If you decided not to use the persistent storage and you already restarted your Tails OS, you will need to create a new wallet and import the seed words again. This is not recommended.

* Send a small transaction to an address in your wallet and wait for confirmation. You can do this on both the offline computer as from the watch-only wallets. Compare the addresses on both wallets, they should be identical.

![Unconfirmed transaction in the mempool...](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/win-test-tx-unconfirmed.png)

* From your watch-only wallet, construct a Bitcoin transaction from the received funds **after it is confirmed** on the blockchain. Depending on your fee and the traffic on the network, this can take a while.

![Watch-only wallet - spend from wallet](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/win-spendfrom.png)

* Export the transaction to an empty USB-stick or SD-card. We are creating a transaction on your normal computer and transfer the transaction in a file to the offline machine.

* Back on your offline machine, inside the wallet (that contains your seed), go to 'Tools > Load transaction > From file'
* Sign the transaction

![Sign and Export your transaction](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/tails-signtx.png)

* Export the transaction back to the USB-stick or SD-card.
* Back on your regular PC, from your watch-only wallet, load the signed transaction from file.

![Watch-only wallet - load transaction](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/win-loadtx.png)

* Broadcast your transaction to the network. Preferably this is done with your own personal node using Tor.

![Broadcast transaction](https://github.com/SovereignNode/tails-cold-storage/blob/master/images/win-broadcast.png)

# Store your backups

We now have the following objects to secure:
1. Clear-text copy of our `mnemmonic seed phrase`
2. A `storage device` with a passphrase-encrypted file (containing our mnemmonic seed phrase)
3. A `passphrase` to decrypt the passphrase-encrypted file on the USB-stick


* Securely store the `mnemmonic seed phrase` in a safe place. Consider storing this inside a tamper-evident bag and using a vault or bank-deposit box.
* Keep your `storage device` safe. This can be a USB-stick or an SD-card.
* Keep your `passphrase` safe and store it AWAY FROM the `storage device`. You may want to keep a copy of your passphrase inside a password manager and in clear-text.

Keep in mind that an attacker can access your coins if he/she:
* has access to your `mnemmonic seed phrase` (in clear-text)
* has access to both your `storage device` (containing your passphrase-encrypted file) AND your `passphrase`.

Congratulation! You've successfully created an offline wallet to store your bitcoins.