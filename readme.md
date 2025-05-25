# A999 Activatior: A9, iOS 9, 9 Years Later

_By Alex Free_

A completely automatic solution that tether downgrades to iOS 9.2-9.3.3, jailbreaks, and activates any iPhone 6S, iPhone 6S Plus, or iPhone SE. Made possible by the work of many [others](#credits). iOS 9 WILL NEVER DIE. I had an iPhone 6S that I jailbroke with Pangu 9 on iOS 9.0.something back in the day, hence why I made this. I actually daily drove this for a bit before upgrading finally to an iPhone X. Instagram mostly works, imessage/ft/calls what else do you need for a daily driver??

For those unfamilar, A9 iOS 9 activation doesn't work normally anymore for many iPhones and no one really knows why. Apple seems to have broken something during downgrade party. After [turdus_merula](https://sep.lol) dropped there were more iOS 9 users then there had been in years, many now expierencing the activation issue (including myself). A999Activator takes all the public knowlege on activating A9 iOS 9 devices and uses some [new](#how-this-works) techniques to make the proccess as seemless as possible for the end user. I hope you enjoy this as much as I. I've been out of the scene mostly for years, so if you can contribute to this and make it better please do!

| [Github](https://github.com/alex-free/a999activator) | [Homepage](https://github.com/alex-free/a999activator) |

# Table Of Contents

* [Downloads](#downloads)
* [Usage](#usage)
* [Additional Info](#additional-info)
* [How This Works](#how-this-works)
* [What about iOS 9.0.x/9.1/9.3.4/9.3.5??](#what-about-ios-90x91934935)
* [Credits](#credits)
* [License](#license)
* [Building](build.md)

## Downloads

### Version 1.0 (5/25/2025)

[a999activator-v1.0-mac-os-universal.zip](https://github.com/alex-free/a999activator/releases/download/v1.0/a999-activator-v1.0-mac-os-universal.zip) _For Mac OS 10.12 and newer_

## Usage

Requirements: You need Mac OS 10.12 or newer, and you need either the [MacPorts](https://www.macports.org/install.php) or  [Homebrew](https://brew.sh/) package manager installed.

1) Download the latest release and extract it.

2) Execute it:

`a999activator/a999` or 

`cd a999activator`

`./a999`

3) Follow the prompts.

## Additional Info

* On the first run of a999activator, there are many additional steps in the proccess that will trigger automatically for you. Subsequent runs will be signifigantly shorter and take fewer steps as it caches needed data from the first run locally in the `data` folder. That `data` folder is very important and personalized to your iPhone. You should back it up because you can put it back in any future a999activator release and it will use that data when it detects your iPhone!.

* Certian aspects of Turdus_ra1n (exploiting SEP, booting exploited iOS) can fail the first time. This is why A999activator has very extensive if-fail-then-retry logic. It will eventually work, and it won't continue the proccess until it does. So don't be discouraged when it says `Something went wrong, lets try that again` because it's really just working as intended and trying again (sometimes many times to get that PTEBlock) does eventually work out. One exception to this is if turdusra1n/turdus_merula crashes at `- <Log> checkm8 setup stage`. If your stuck here for a long time (more then 30 seconds) I would `ctrl+c` to exit a999activator, unpulg the USB-A to Lightning cable from the USB port on the Mac, then plug it back in before running the `a999` command again. Unfortunately I don't have a better solution for this yet as it is a turdus merula problem.

* In a similar vein to above, if you fail to enter DFU mode when prompted or the custom ramdisk fails to boot a999activator notices this and goes back to correct it.

* Very rarely, the ramdisk may not be able to mount the iOS 9 filesystem after the restore. If this occurs you will see a bunch of errors and when iOS 9 boots you will see Setup.app. In this case, `ctrl+c` out of a999activator and run it again.

* I have extensively tested a999activator with 2 different iPhone 6S Pluses. I have literally activated iOS 15.8.4 100+ times with the same Apple ID. I have written support for iPhone 6S and iPhone SE because it should work the same. iPads in theory can work too in a future update, as well as any other A9 device not currently supported. But if your having some issues with a 6S or SE let me know because I don't have those yet. Also I use MacPorts, I added Homebrew support and it should work fine but again that wasn't tested...

* A999activator will ALWAY restore iOS 10.3.3 first, even if your already on iOS 9. This is required because espically on iOS 9.3.x you might get greyed out WiFi even after being on 9.3.x already.

## How This Works

Remember, this is all automatic (as possible)!

1) Restores iOS 15.8.4 if iPhone is not on iOS 15.8.4 and activation files have not yet been backed up.

2) Prompt user to activate, sign into iCloud on iOS 15.8.4 if activation check returns it has not been activated, and complete Setup.app. Additionally, If the user has a SIM with active service and desire to use it on the target iOS version, it needs to be installed while activating or when they first activated the device with iOS 15.8.4 so there is an option to restore iOS 15.8.4 here even if iOS 15.8.4 is detected.

3) Checks activation status of iOS 15.8.4, then boots a custom ramdisk in Recovery mode to create iOS 15.8.4 activation tarball files which are transferred to the computer.

4) Downgrades to iOS 10.3.3 1st to work around 2 issues (random rebooting to Recovery Mode and random disabled Wifi in iOS 9.3.x). This is also the first step if activation files have been backed up.

5) Downgrades to target iOS (9.2-9.3.3).

6) Boots a custom ramdisk in Recovery mode that puts the activation tarball files, an activation script, and a launch daemon all on /. Jailbreaks the iPhone (needs a trigger to enable it but bootstrap is installed), disables Setup.app, and then reboots into Recovery Mode.

7) Boots iOS 9.2-9.3.3.

8) User is prompted to sign in to Wi-Fi and then go to http://jbme.ddw.nu to enable the Jailbreak.

9) Jailbreak triggers the previously in-active launch daemon. Launch daemon extracts all activation tarball files that were put on / into the proper /var places. It then modifies a plist file for activation needed for 9.2.1-9.3.3. After that it deletes itself and all other temp files. Setup.app is then re-enabled, and the iPhone is rebooted into Recovery mode.

10) iPhone is booted into iOS 9.2-9.3.3. Activation status is checked and if successful a special boot script is created dynamically in the same directory as the a999 command which can be used to boot the device from Recovery Mode in the future.

## What about iOS 9.0.x/9.1/9.3.4/9.3.5??

So iOS 9.0.x/iOS 9.1/9.3.4/9.3.5 have jailbreaks. The problem here is that these jailbreaks require an activated iOS 9 iPhone. Chicken and egg problem, we need a jailbreak to activate. This could be developed in the future if it can be done from a ramdisk entrypoint similar to how iOS 9.2-9.3.3 are handled and then triggered with some kind of untether or Safari exploit.

## Credits

* [u/iPh0ne4s](https://www.reddit.com/user/iPh0ne4s/) and [u/_alecbaldwin](https://www.reddit.com/user/_alecbaldwin/) for the activation method posted by [u/roolw](https://www.reddit.com/user/roolw/): [How to fully activate iOS 9.2-9.3.5](https://www.reddit.com/r/setupapp/comments/1jwmv8s/how_to_fully_activate_ios_92_935/).

* [@John011235](https://x.com/John011235) for this [post](https://x.com/John011235/status/1756498551385755682) about plutil.

* [Sep.lol team](https://sep.lol/) for turdus merula.

* [LukeZGD](https://github.com/LukeZGD) for [Legacy-iOS-Kit](https://github.com/LukeZGD/Legacy-iOS-Kit).

## License

A999activator itself is released under the 3-BSD license, see [license.md](license.md). A999Activator uses many other dependency programs which are not under that license, such as:

* Turdus Merula (closed source, open source is planned).

* Legacy-iOS-Kit (GNU GPL v3.0). This uses my [forked version](https://github.com/alex-free/Legacy-iOS-Kit) by the way.