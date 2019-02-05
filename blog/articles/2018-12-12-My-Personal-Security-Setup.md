## My Personal Security Setup

12/12/2018

Over the last year or so, I have seriously stepped up my security game. These days, fraudsters have an exceptionally easy job of getting your data. With all these data breaches reaching from small websites that have bad encryption (if any) to online stores. This data can be used as a whole to create so called "fullz". You cannot really stop them breaching databases really, thats out of your possibilities.

However, you can still protect yourself. The most Important part is a:

## Password Manager

The most important thing to do right is a good personal (and professional) password policy. Most people know what they *should* do. But they don't.

Use long random passwords. And even more important: **DO NOT RE USE PASSWORDS!**

This small Pokemon fan forum you registered in 2009 might have been breached, and if you use the same password, they also have your PayPal, Gmail, twitter and god knows how many other accounts. And while the mentioned big sites have done a good job protecting you, the Pokemon fan forum got pwned still.

Even better: There have been cases where such fan forums for World of Warcaft (WoW) where run by russian groups with their one and only goal being that you register on the forum with the same username, e-mail and password than your WoW account.

Don't fall for that. Use a password manager.

There are many of them. Some are commercial and extremely convenient. They do host the passwords on their servers, however these are encrypted before even storing them. Personally though, I don't want to pay, nor do I want to just trust these companies.

So as my Password manager I chose KeePass2. It's Free and Open Source Software and has a very nice client for Windows and Android (a web UI as well but I do not use that). The Android client can be unlocked with your fingerprint, which is VERY convenient. And the Windows client has auto-type for username+password. Now I can login faster with KeePass than I could before using any sort of Password management.

I encrypt my KeePass database file with the default AES-256 bit based algorithm and use 10 000 000 iterations.

Also, I was very surprised to see just HOW MANY accounts I have when I migrated to a password manager. My KeePass database contains a 100+ accounts with Passwords. The best thing about it is that I also never need to remember my username ever again! Did this website use my email? First-name [dot] Last-name? Or my username with some random number behind it I always forget? Doesn't matter. Use a password manager!

For synchronization I use Google Drive. The reason why I will explain next:

## The safety net

When setting up KeePass for the first time, I needed a way to synchronize and backup the database file. Because when I lose that file, I have a problem. Also, I want the password for the account I just created to be synced on all my devices of course. I chose GDrive for that. Not only that, but my Google Account is my safety net in case EVERYTHING goes wrong.

My Idea is to have the most secure account I have, to NOT be managed by my password manager. But rather it being the only account where I stillhave to remember the password to. So if I ever lose ALL my backups of my database file. I can retrieve it back from Google Drive. If I forget the password to the file, I can use my G-Mail to reset *most* of accounts passwords.

The Google account uses non SMS based 2FA which is a bit safer than SMS based one. This physically ties it to my phone + number. I'd have to forget my password, lose my phone, every device currently locked into my Google Account (3 PCs + 1 at work) the phone number AND access to my phone provider to be fully locked out. That's not likely to happen.

The third reason to use Google is their data security. You might lose data when your owncloud breaks. But how likely is it that Google Drive will break?

## VPNs

Now that my passwords are secured, I also want them to stay secured. Part of that is to make sure you use a encrypted connection whenever you enter a password. In 2018, and with GDPR in place, every website is legally required to use HTTPS to ensure your passwords to be encrypted. This encryption however CAN be broken by installing a self signed certificate in the network your in (and probably other ways I have never heard of).

This is common in public Free-WiFi. It can make MitM attacks a reality again, although you think you use HTTPS. To bypass that risk, you can use a VPN whenever you are in a Network you don't 100% trust. Personally, I have a openvpn server running on my VPS that I connect to. Otherwise, how would you ensure that the VPN provider you use is trustworthy? Also the clients, both on windows and android, are just phenomenal.

## Drive Encryption

Lastly, what happens when you lose a device or it gets stolen? Especially important if you have a business laptop. Getting into a windows when having physical access is trivial, and that might give an attacker access to outlook data (and thus your email), SSH keys and whatever you might have saved.

Turning on FDE (Full Drive Encryption) is made VERY easy these days too. iOS and macOS devices are encyrpted by default. Newer android devices are either encrypted by default or offer a very simple process in the device settings. On windows you have either the (almost) Open Source Tool Veracrypt or Microsofts BitLocker (only on certain versions).

I personally use BitLocker on windows. Some people say that there might be goverment backdoors in there (same could be the case in VeraCrypt. Its not fully open source and sneaking code in a massive Open Source Project ain't that hard) but these don't concern me. I am concerned about a regular attacker stealing stuff. Also BitLocker is just convenient to set up and it builds an additional chain of trust between the OS and the UEFI by using the TMP chip. This is not the case with VeraCrypt as far as I have heard

## Final words

That about wraps it up. In summary: Personal IT security is important, surprisingly simple and sometimes even more convenient than the not-so-secure way of doing things, in the case of a password manager remembering and autotyping your username + password.

Thanks for reading!