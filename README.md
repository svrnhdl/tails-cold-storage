# Bitcoin cold storage with Tails OS
A guide on how to create a cold storage on a Tails bootable USB.

## Persistence feature
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

If you decide not to use the persistent volume, your wallet will be more akin to a 'paper wallet' and the seed backup is your primary recovery mechanism. This is a great option if you don't intend to spend from your cold storage. If at any point in time, you decide you wan't to spend your coins, you can sweep your wallet using your seed backup.

If you decide to use the persistent storage, your Tails USB will contain a copy of the seed (and can thus be used for signing without importing your seed again). This is more similar to an air-gapped hardware wallet.

The choice is a personal one. If you want to be able to spend from the wallet occasionally, I suggest that you use the persistent volume with a **strong passphrase**.
