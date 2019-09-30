## Google Dork's - Sometimes it really is that easy

One day, I was watching some DefCon talks at YouTube, as I often do. One
of the videos was titled "[Google Hacking for Penetration Testers](https://www.youtube.com/watch?v=N3dzVl40lQA "The video")". 
This title sounded very interesting, but also didn't tell me much about what
to actually see in there. So naturally, I watched it. It was amazing.

All I could think about was "huh it really is that easy sometimes". A
couple weeks later I made my first own Google Dork, found a good couple
of COMPLETELY wide-open databases for various sites, including some
decently sized forums, and reported the leak to the Owners.

But before I tell that story further, let me just tell you what "Google
Hacking" and "Google Dorks" are all about:

The concept is fairly simple. People put a lot of stuff on the internet.
And Google is highly effective at finding and indexing basically
everything there is. Additionally, Google offers some advanced search
Parameters that can make searches very effective. So if somebody posts
their Facebook password in a public pastebin under the wrong Impression
that these are private, you can literally just google for that password.
Some other thing that you might see a lot are so called "Open Web
Directories". These are folders on web servers that have auto-indexing
on. That sometimes is by design, but also often a misconfiguration. In
that case, finding someones juicy files is fairly trivial.

Now to show you an Example, let me show you the Google Dork that I used
to find those Databases as mentioned above:

``` 
inurl:"main.php?action=db"
```
Just put that in the Google Search and you may find similar things.
*Yes. Its really that easy sometimes.*

So let me explain how I found it: At work, we had to dump a database for
a customer. The server was not our own, and we did not have DB or SSH
Access. However we had FTP Access. So a colleague suggested to use a
tool named [MySQLDumper](http://www.mysqldumper.de/) "MySQLDumper").
This tool is designed to be put on a server, dump databases to SQL and
remove it again. Because of that it has **NO PASSWORD PROTECTION** by
default. It also provides some functionality very similar to PHPMyAdmin,
as in you can change or delete certain data sets from the tables.

So I asked myself "What if people just leave that thing on their
servers." As I recently learned about Google dorks, I found a
distinguishable factor that would allow me to find MySQLDumper in a
Google Search. There would probably be many other ways, but I chose to
use part of the URL to search for it.

And low and behold, I found lots. Many returned a 404, meaning the owner
removed the tool already, and some have put up an HTPASSWD protection.
But for a handful of sites I just was able to get to the site and was
effectively having control over their database. You could (in theory)
dump the Database and sell it, change the Password Hash for the Admin
User to your own and control the whole site / server and a lot of other
things. Dont do that though. It\'s illegal and immoral.

Sometimes...it really is *too easy.*

I have then submitted that dork and others I created to the [Google hacking database](https://www.exploit-db.com/google-hacking-database "Google Hacking Database").
Which makes me an official contributor of the "Exploit Database and
Google Hacking Database" apparently. It sounds cooler that it is to be
honest.

![screenshot of my profile on ghdb](/fileadmin/_processed_/4/b/csm_Screenshot_2019-03-31_12-47-40_a64a9ec18c.png)

Some other Dorks from me Include one that is capable of finding
incomplete Installations of the TYPO3 CMS that one would be able to
hijack by finishing the Installation. This would allow an attacker to
not just run the website but to Upload a webshell or other malicious PHP
code using the Extension System.

Here is a list of all my approved dorks so far:

- [KeePass files in open web directories](https://www.exploit-db.com/ghdb/4748)
- [rcon-passwords on PasteBin](https://www.exploit-db.com/ghdb/4750)
- [The MySQLDumper one](https://www.exploit-db.com/ghdb/4669)
- [Free web bases Proxies](https://www.exploit-db.com/ghdb/4749)
- [Nibbleblog based Websites](https://www.exploit-db.com/ghdb/4756)
- [TYPO3 sites, left alone while installing](https://www.exploit-db.com/ghdb/4751)

I recommend just surfing the
[GHDB](https://www.exploit-db.com/google-hacking-database "GHDB") as
well

Please use this knowledge responsibly and follow the laws of where you
live.

### Thanks for reading.
