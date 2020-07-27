Modern Android is pretty secure
===============================

When most people would describe the Android Platform, things like customizability, device diversity and pricing are usually named. Security on the other hand, most likely will not come to people’s mind. At least in my experience that is. Most people just don’t _perceive_ Android as being especially secure. The biggest reason could be the more open Google Play Store. Sneaking malware into there is just easier than on Apple’s AppStore. And it has happened. [Plenty](https://www.forbes.com/sites/zakdoffman/2020/06/03/beware-millions-of-android-users-must-delete-this-malicious-video-app-now/) times. 

And sure, malware in the App Store is definitely a problem. But in the end it’s just a drawback of the more relaxed platform rules that Google has put in place. [Although this seems to be changing](https://www.cnet.com/news/google-removes-600-apps-from-play-store-due-to-disruptive-ads/). One should always be conscious about what kind of software should be trusted anyways. On _any_ platform_._ 

Now, I am currently looking for a new phone and was interested just _how bad_ Security on the Android platform actually is, and what phone would be the least insecure.It actually turns out that Android has a very impressive Security Model!

For devices that shall run Android, a device maker has to make sure that their device and the Android they ship complies with the [Android Compatibility Definition Document](https://source.android.com/compatibility/cdd) (CDD). If a device is incompatible hardware wise, it can not run Android. If a vendor modifies Android in a way that violates the CDD, it is, by definition, not Android anymore. So if you buy a device that explicitly states that it runs Android, it means that compatibility with the CDD is ensured.

The CDD ensures Security
------------------------

Taking a look at the CDD for Android 10, there is a whole section on Security. This document is huge and references multiple other huge documents. I’ll try to summarize is as best as I can:

The Permission system has to be compliant with the [Android Security and Permission Reference](http://developer.android.com/guide/topics/security/permissions.html). This ensures things like being able to revoke permissions after they have been granted, how permission prompts work, which permissions can only be granted to system apps and much more.

Sandboxing has to be properly implemented. The Android sandbox is further explained in [this document](https://arxiv.org/abs/1904.05572). Essentially, every app has an unique UNIX User ID and directories that are owned by that user and that user alone. Because Android has no root user, other apps _can not_ access the data that is stored in these particular directories. Introducing root into the system would therefore break the security model. That’s why we will never see an Android phone which is rooted by default. On top of all that, there are also [SELinux](https://en.m.wikipedia.org/wiki/Security-Enhanced_Linux) policies to further improve the sandbox.

Speaking of which, SELinux’s Mandatory Access Controls (MAC) have to be fully functional. MAC must also be implemented to allow for sandboxing of kernel applications. These Mandatory Access Control policies allow for restrictions to be made and enforced by the system. They are applied for **everything** on the system. They can not be altered or overwritten by anything in userspace and thus can’t just be manipulated by malware or another threat actor.

And now: Encryption
-------------------

The CDD also requires that the /data and the /sdcard partitions of the built-in storage have to be encrypted _out of the box_. The /data partition houses the private data for each application. The /sdcard partition is for shared storage, such as your photos and documents.

So if your device is powered off and someone gets ahold of it, it will be hard if not nearly impossible to grab any meaningful data from the device’s onboard storage. Which brings us to the next thing:

Verified Boot
-------------

On top of all that, [verified boot](https://source.android.com/security/verifiedboot/) also has to be properly working. To quote:

> Verified Boot strives to ensure all executed code comes from a trusted source (usually device OEMs), rather than from an attacker or corruption. It establishes a full chain of trust \[…\] In addition to ensuring that devices are running a safe version of Android, Verified Boot checks for the correct version of Android with rollback protection. Rollback protection helps to prevent a possible exploit from becoming persistent by ensuring devices only update to newer versions of Android.
> 
> https://source.android.com/security/verifiedboot/avb

Many people seem to believe that verified boot only ensures the device’s security when an adversary has physical access to the machine. And dismiss the importance of verified boot because of that. But first of all, physical access is definitely worth considering when talking about mobile devices. And second of all, that’s just not true. Verified boot makes sure that no unwanted code is running while or directly after booting the device. This makes it much harder for any type of malware to achieve any form of privileged persistence. A simple reboot would just get rid of it. This can be observed with jailbreak exploits like [checkra1n](https://checkra.in/) which do not persist after a reboot, since iOS too uses verified boot.

Keep in mind that for all of that to work, your device’s bootloader has to be locked.

Key Management
--------------

Encryption requires Keys. Keys have to be stored _somewhere_. Android can utilize technologies such as [Keymaster and Strongbox](https://proandroiddev.com/android-keystore-what-is-the-difference-between-strongbox-and-hardware-backed-keys-4c276ea78fd0) to guard keys, even in case of Kernel Compromises or Hardware Exploits such as the infamous [Meltdown and Spectre](https://meltdownattack.com/). Samsung’s KNOX goes even further [and wipes the keys once tampering is detected](https://docs.samsungknox.com/admin/whitepaper/kpe/trusted-boot.htm#lockdown).

Avoiding Exploits that are based on memory safety bugs
------------------------------------------------------

There’s more!

[A recent study from Microsoft](https://www.zdnet.com/article/microsoft-70-percent-of-all-security-bugs-are-memory-safety-issues/) revealed that about 70% of all the vulnerabilities in Microsoft Products are related to memory safety.

[Another study from Google](https://www.zdnet.com/article/chrome-70-of-all-security-bugs-are-memory-safety-issues/) revealed the exact same, but for Chrome.

So there is definitely reason to assume that memory safety bugs are worth considering on Android as well. And Google did. For Android 11 [they announced](https://security.googleblog.com/2020/06/system-hardening-in-android-11.html) the use of a new hardened memory allocator, several safer ways to initialize the kernel and userspace as well as techniques to identify memory bugs in real time.

None of this _completely eliminates_ memory bugs, but they’re certainly going to appear much rarer once all of this is in place in Android 11.

And… even more
--------------

All of the above is just the tip of the iceberg really. There are a lot more things to learn about the Android Operating System in terms of security. And stuff like Samsung’s KNOX would be yet another rabbit hole to fall into. But in Summary:

### Contrary to popular belief, modern Android is pretty secure.

Thanks for reading
