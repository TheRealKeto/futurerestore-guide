# Futurerestore Guide
Futurerestore is a tool that allows iOS devices to upgrade, downgrade, or re-restore to any iOS unsigned firmware, through the usage of SHSH blobs. This guide will teach you on how to use Futurerestore to upgrade, downgrade, or re-restore to an unsigned firmware. 

Before continuing, keep in mind that this guide is based off of [this one](https://docs.google.com/document/d/1WHuwuvnkcEUCwaDuck2dy-MR7q4em38uL4_4Utx2QZ8/mobilebasic), and contains information that can change your device's behavior and even damage it. Note that if anything happens to your device, **you** will be held resposible for the damaged caused. 

## Background Info
Before you begin following this guide, keep in mind that: 
- This guide was created to teach users (specially beginners) how to use Futurerestore in order to downgrade their devices to iOS 12.2. However, the methods used in this guide are **not** limited to these users only, as they are essensially the same for other firmwares.
- **iOS 12.4.1's SEP and Baseband are fully compatible when attempting to downgrade to iOS 12.2.** This means that you're able to use the latest SEP and Baseband without having to worry about the "fortnight bug", a bug which causes your device to stop working after 2 weeks. 
- If you're planning to backup your device in order to use that backup after futurerestoring, note that said backup **must not include any jailbreak data**. Modern jailbreaks have an option to "uninstall" or remove the jailbreak, and there are many tools out there that can delete your jailbreak without losing data.

#### For Windows users
- If you're a Windows user, **avoid having the Microsoft version of iTunes installed.** If you have it installed, uninstall it, then download the latest iTunes release from Apple's website in order to install its drivers correctly. 
- If you're on Windows, avoid having a 32-bit system, as Futurerestore does not work on them. 

## Getting ready to Restore
In order to use Futurerestore to upgrade, dowgrade, or re-restore to your desired unsigned firmware, there are a few things you will need, such as: 

- [Futurerestore](https://github.com/s0uthwest/futurerestore/releases)'s latest release.
- Your SHSH blob file from [TSSSaver](https://tsssaver.1conan.com), or [shsh.host](https://shsh.host/).
- The IPSW from [ipsw.me](https://ipsw.me/) contaning the SEP and Baseband that is compatible with the unsigned firmware you're trying to upgrade, downgrade, or re-restore to.

Additionally, if you know you have to specify an specific SEP and Baseband, you will need: 
- The SEPOS, which is a `.im4p` file
- The baseband firmware, which is a `.bbfw` file.
- The `BuildManifest.plist` file from said IPSW.

In order to obtain additional files, you'll have to extract the IPSW. You can use [extract.me](https://extract.me/) in order to download these additional files without having to extract an IPSW on your system. 

These files have differrent names for different devices inside different IPSW, which is why it's recommended to use [r/Jailbreak's Telegram Bot](https://t.me/rjailbreakbot) in order to find the correct file names for your SEP and Baseband. You can find the specific names of your SEP/Baseband by running `/sepbb` when using the Telegram bot.

Once you have these files, its a good practice to put them inside a folder located on your desktop, named `futurerestore`. 

### Finding your Nonce Generator
Your nonce generator is a 16-character string used by the device's bootloaders in order to authenticate a legitimate restore with Apple, which is why its so critial to have SHSH blobs saved, as they contain this string.

In order to find your nonce generator: 
1. Open your downloaded blob from TSSSaver, or shsh.host with any kind of text editor.
2. **(On Windows)** Press `Ctrl + F`, **(On macOS)** `Press Command + F`, then search for the word "generator"

Next to, or underneath, you'll find your nonce generator. Copy the 16-character string onto a text file inside your `futurerestore` folder, as you will need this string later on. 

### Setting your Nonce Generator
Now that you have found your nonce generator, its time to specify it on your device NVRAM. In order to specify your nonce generator, you will need a nonce setter. 

Nonce setters are often applications somewhat like jailbreaks, but only grant access to your device's NVRAM in order to change your current nonce. There are many nonce setters released supporting many fimrwares. Here's a list of a few released by respected jailbreak developers: 

- [PhœnixNonce](https://github.com/Siguza/PhoenixNonce/releases) for iOS 9.x (Created by Siguza and Tihmstar)
- [NonceSet](https://julioverne.github.io/description.html?id=com.julioverne.nonceset) for iOS 10.x (Created by Julioverne)
- [NonceSet112](https://github.com/julioverne/NonceSet112) for iOS 11 - 11.1.2 (Created by Julioverne)
- [GeoNonceSetter](https://github.com/GeoSn0w/GeoNonceSetter12/releases) for iOS 12 - 12.4 (Created by GeoSnow)

You can install and use a nonce setter that supports your iOS firmware by downloading the application from Cydia, or by sideloading it with [Cydia Impactor](http://www.cydiaimpactor.com/) or [ReProvision](https://github.com/Matchstic/ReProvision/releases). Alternatively, modern jailbreaks, such as [unc0ver](https://github.com/pwn20wndstuff/Undecimus/releases) or [Chimera](https://chimera.sh/), have an option to set your nonce generator on supported firmwares, so you can use your jailbreak tool as well. 

In order to set your nonce generator:
1. Open your nonce setter tool (or modern jailbreak tool).
2. Find a text field with the words "generator", "boot nonce" or "set nonce".
3. Within that region, type in your string that you saved from your SHSH blob.
4. Press "Set Nonce" (or hit "Jailbreak" if you're using a jailbreak tool).

Once you've set your nonce generator, you're ready to begin the restoration process. Note that **if you power off your device, or it turns off for any given reason, you will need to set your nonce again.**

## Restoration
You're finally ready to start using Futurerestore in order to upgrade, downgrade, or re-restore to your desired unsigned firmware. Before you move forward, keep in mind that: 
- Failing to disable "Find my iPhone/iPod/iPad" and/or having [NO PLS Recovery](https://cydia.akemi.ai/?page/net.angelxwind.noplsrecovery) installed can cause the process of Futurerestore to not begin, or fail.
- If you're device is put into "Recovery Mode", **do not panic. This is entirely normal.**
- If you receive any pop-ups from iTunes attempting to update/restore your device, simply hit "Cancel" and close iTunes.

With that out of the way, lets cut to the chase. There are 2 ways you can use Futurerestore in order upgrade, downgrade, or re-restore to an unsigned firmware. This guide will explain both. 

### Automatic SEP & Baseband 
This method is used when you are certain that the latest iOS release has an SEP and Baseband that is **fully** compatible with the version you're trying to upgrade, downgrade, or re-restore to. Often times, this is the most common method used by many. 

In order to upgrade, downgrade, or re-restore using this method: 
1. Open Command Prompt/Terminal.
2. Drag Futurerestore from your `futurerestore` folder onto your terminal, then type `-t`.
3. Drag your SHSH blob from your `futurerestore` folder onto your terminal.
4. Type `--latest-sep --latest-baseband`, then drag your IPSW from your `futurerestore` folder onto your terminal.

In the end, your result should look something like this: 
```
$ futurerestore -t [your blob] --latest-sep --latest-baseband [IPSW]
```

For **iPods and Wifi-Only iPads**, do not specify a baseband: 
```
$ futurerestore -t [your blob] --latest-sep --no-baseband [IPSW]
```
Once you are sure that you have the right command, hit "Enter" and the process should begin.

### Manually specify SEP & Baseband
This method is used when the latest iOS release has an SEP and Baseband that is **not compatible** with the version you're trying to upgrade, downgrade, or re-restore to. The neat thing about this is that its similar to the previous method, except there are some alternations. 

In order to upgrade, downgrade, or re-restore using this method: 
1. Open Command Prompt/Terminal.
2. Drag Futurerestore onto your terminal from your `futurerestore` folder, then type `-t`.
3. Drag your SHSH blob from your `futurerestore` folder onto your terminal.
4. Type `-s`, then drag your SEP from your `futurerestore` folder onto your terminal.
5. Type `-b`, then drag your Baseband from your `futurerestore` folder onto your terminal.
6. Type `-p`, then drag your `Buildmanifest.plist` file from your `futurerestore` folder onto your terminal.
7. Type `-m`, drag your `Buildmanifest.plist` file (again), then drag your IPSW from your `futurerestore` folder onto your terminal.

In the end, your result should look something like this:
```
$ futurerestore -t [your blob] -s [SEP] -b [Baseband] -p [BuildmManifest] -m [BuildManifest] [IPSW]
```

For **iPods and Wifi-Only iPads**, do not specify a baseband: 
```
$ futurerestore -t [your blob] -s [SEP] --no-baseband -p [BuildmManifest] -m [BuildManifest] [IPSW]
```
Once you are sure that you have the right command, hit "Enter" and the process should begin.

If you run into any issues during the Futurerestore process, please refer to [this](https://gist.github.com/TheRealKeto/e4d2e0c18caea7399dcd028e803f7e9e), which includes the most common errors you can encouter when using Futurerestore, and how to fix them. 

##
### About this guide 
This guide was updated on **August 27th, 2019**, and continues to be updated with the lastest SEP/Baseband compatiblity and other info. 

If you have any questions, head over to [r/Jailbreak's Discord Server](https://discordapp.com/invite/jb) for support under their futurerestore-help channel.