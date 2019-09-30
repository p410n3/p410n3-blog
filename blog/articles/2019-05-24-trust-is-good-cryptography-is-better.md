## Trust is good, cryptography is better

Recently, I have seen a lot of people in the InfoSec- and Online Privacy
Community having lenghty discussions about which companies we can trust
these days.

At the very least, since Snowden has leaked various documents,  many
companies have been labeled as either "trustworthy" or "not
trustworthy". These companies and services are rated by their past
actions, and the main factors seem to be how they handle personal data,
and how much they value their security. Let's look at some examples:

- "GMail is a privacy nightmare but is a very secure service"
- "Yahoo was totally pwned a few Years back and the hid it for 3 YEARS! Oh and they spy on you"
- "ProtonMail is anonymous and safe"

And so on and so forth. Any discussion or article about this topic
includes tons of links to all kinds of sources, personal experiences and
quite often very, VERY heated tempers.

And it surely doesn't end with E-Mail Services. VPN Providers, ISPs,
Cloud Storage Providers and Server Hosts are frequently discussed in the
realms I lurk around.

But, in the end, it's all about TRUST. Yes, Yahoo is not as trustworthy
as ProtonMail these days, after having every single User Account they
had in [2013 being hacked, and trying to sweep it under the
Rug](https://en.wikipedia.org/wiki/Yahoo!_data_breaches#August_2013_breach "The Yahoo! hack"). 

Let me elaborate this with an example: Imagine we have a 50GB folder
full of documents, images or otherwise valuable data on our harddrive.
Now, we might back that up to an extrenal HDD, but as any responsible
IT-Person would tell us, a local backup is pretty much like having no
backup at all. Houses burn down, HDDs get confiscated or stolen and
viruses nuke any file they come in contact with. What we need to do is a
so called "offsite backup". This means storing our data at a different
physical location.

For personal use, one of the many cloud storage providers seems to be a
good choice for our problem at first, but if we do some research we
might notice that some of these options are [pretty
invasive](https://support.google.com/photos/answer/6128838?co=GENIE.Platform%3DAndroid&hl=en "Google Image facial recognition").
And even If we don't care about the privacy aspect of it, we still have
to consider that accounts can be breached, passwords hijacked and data
stolen. Maybe having our vacation pictures stolen isn't that big of a
deal, but having our tax info stolen for example, can be quite a pain in
the ass, as this information can be used to commit tax fraud under your
name. Actually, any type of personal Information leaked might help
Criminals to build a [synthetic
profile](https://www.businessnewsdaily.com/10973-synthetic-identity-fraud.html "synthetic Tax Fraud")
or even just help them answer some [KBA
Questions](https://en.wikipedia.org/wiki/Knowledge-based_authentication "KBA")
to get into other Accounts we own. What exactly can be done with our
data depends entirely on the data that would actually be uploaded and
differs from person to person. This is what many people refer to as a
"Threat Model".

What I am saying is: When choosing a cloud storage provider, we should
think about our personal privacy and security, as these two things go
hand in hand these days.

Now so far we have only built our threat model and have been getting
more and more paranoid. Doesn't exactly sound like fun to me.

At this point, one might be inclined to do some research to find the
most trustworthy cloud provider. Is Google a good choice? Or use the
(way more expensive) MEGA? Is DropBox even still a thing?

*BUT* trust is something we shouldn't rely on. Trust is definitely not
worthless¹, but its based on assumption and goodwill, not on facts. I
looked up a definition in a dictionary:

> TRUST - noun
>
> reliance on the integrity, strength, ability, surety, etc., of a
> person or thing; confidence. confident expectation of something; hope.

I think this summarizes it pretty well. So what is the solution to our
little Backup problem?

**CRYPTOGRAPHY IS!**

If we upload our files zipped and encrypted with a strong passphrase and
decent Algorithm, we don't need to hope that our storage provider
doesn't snoop around in the files. And if our account gets hacked, that
is certainly annoying, but without the keys, the attacker will only be
able to steal useless data junk from us.

*Disclaimer: In theory an Attacker could, with enough sophisitication and resources, decrypt our files. If we choose a strong passphrase however, we would need to be an exceptionally high value target to justify such measures.*

When we trust a service, we are giving control away. If we don't want
our data to be accesed by ANY third party, including hackers and the
storage provider, the easiest way is to take matters in our own hands.
By encrypting the data we want to protect.

For this specific scenario I personally use GPG with symmetric
encryption, using a 200+ char long password. GPG's default algorithm is
considered safe, but it's possible to just use AES256 or others.

For emails, one can use PGP, for websites make sure they run HTTPS. If
they do, the connection to the server is encrypted. I recommend using
[HTTPS
Everywhere](https://www.eff.org/https-everywhere "HTTPS Everywhere") to
make sure all connectioons are safe. And as described in an [earlier
blog post of mine](/my-personal-security-setup), I also recommend anyone
to use full drive encryption in case of a stolen hard drive.

TLDR: Encrypt your shit

### Thanks for reading!

¹~[Thanks to this guy for correcting me!](https://www.reddit.com/r/privacy/comments/bsf3kv/trust_is_good_cryptography_is_better/eon881b/)~
