## Bypassing Firewalls - But How?

In my last post I have elaborated multiple reasons as to *why* someone
would want to bypass a Firewall. Now that this is established, here
comes the part where we get to the "how".

If you don\'t care about the technology behind any of this, jump to the
[conclusion](/bypassing-firewalls-but-how#c70 "conclusion").

However, if you are interested in the theory behind Firewall bypassing,
go right ahead and read the rest of this article.

### Digging your way out

Network Firewalls act as a barrier between your client device and the
"bad, scary outside world". They require in- and outgoing traffic to be
passed through them to be able to achieve this. Now the general concept
to bypassing a firewall is using a
[proxy](https://en.wikipedia.org/wiki/Proxy_server "Proxy server - Wikipedia") or a
[VPN](https://en.wikipedia.org/wiki/VPN "VPN Server - Wikipedia") server.
These are uncensored servers on the outside of the restricted network,
which then will act as your gateway to the uncensored Internet.

But *"Just use a proxy or a VPN"* is obviously not the answer to our
question. That would be way too easy. Bypassing Firewalls is a never
ending game of cat and mouse, and so it gets quite a bit more complex
than that. 

For elaboration\'s sake, let's pretend your company has banned access to
the [NYTimes](https://www.nytimes.com/ "NYTimes") website for *whatever
reason*. If you want to connect to their website, the Firewall will see
that your Computer wants to connect to the NYTimes website. Upon seeing
this request, the Firewall will not let it pass to the open internet,
but rather reply with a very polite "lol no fuck you". Using a VPN /
Proxy however, you are requesting a connection to a domain like
myproxyserver.com, which then will forward your request to the NYTimes
website and the answer from their servers back to you. Because after all
*only* the NYTimes website is blocked, but your middlebox is not.

![That is the basic
idea](img/csm_fw2_1bb9f2a5af.png)

For a very unsophisticated Firewall, all of this might already be enough
to bypass it. Any VPN or Proxy Server may suffice. But a more advanced
Firewall is able to tell that you tried to bypass it by inspecting your
traffic, and stop you from doing so. Or your server might be set up in a
way that gets blocked for some other reason that isn\'t even related to
your attempt to bypass the Firewall.

### Staying undetected, and overcoming obstacles

To actually escape such Firewalls effectively, what we need to know are
the restrictions and methodologies used against us first. Once we have
an understanding what could make us fail, we can work towards getting
around this.

The following list of two Security measures which a Firewall might put
into place is far from complete. These are things I have personally
dealt with or that I was otherwise able to find out about during my
research. There is probably an infinite amount of stuff that *might*
happen to stop you in your tracks, and just as much to bypass that
again.

### Blocked ports

A very common practice in Firewalls is to block, or whitelist, certain
ports. Many resources, like
[this](https://www.watchguard.com/wgrd-resource-center/security-fundamentals/what-is-a-port "Port article"),
exist about this topic, some targeted specifically at Firewall admins.
Blocked ports are a common thing to encounter in any kind of restricted
network. Even some
[ISPs](https://en.wikipedia.org/wiki/Internet_service_provider "ISP - Wikipedia") are
[blocking
ports](https://www.quora.com/What-are-ISP-blocking-ports "ISP blocking ports").
It\'s usually not specifically done to stop people from bypassing their
Firewall, it's just an overall used practice, following [the principle
of least
privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege "The principle of least privilige").
Avoiding blocked ports is easy, just use one on your VPN / Proxy Server
that is used for a very common service, and therefore is very likely not
to be blocked.

Examples are:

-   Port 53 for
    [DNS](https://en.wikipedia.org/wiki/Domain_Name_System "DNS")
-   Port 80 for
    [HTTP](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol "HTTP - Wikipedia")
-   Port 443 for
    [HTTPS](https://en.wikipedia.org/wiki/HTTPS "HTTPS - Wikipedia")

These ports are almost always unrestricted. I personally use Port 443,
but the other ones should work as well.

### Protocol Fingerprinting

A slightly more advanced method of restricting users is by identifying
the protocol their connection is using. Connecting to port 443, the one
commonly associated with https traffic is neat, but if the Firewall
notices that your connection clearly is **NOT https traffic**, that
isn't so neat anymore. In fact, it might make you look even more
suspicious. For example, The
[OpenVPN](https://openvpn.net/what-is-a-vpn/ "OpenVPN - What is a VPN")
protocol can often be identified when using default settings. To hide
what you are doing, many solutions already exist. I have split them into
these two categories:

1.  Make your traffic look like a different protocol
2.  Make your traffic look like random shit (aka
    [Obfuscation](https://en.wikipedia.org/wiki/Obfuscation "Obfuscation - Wikipedia"))

OpenVPN for example, does use
[SSL](https://en.wikipedia.org/wiki/Secure_Sockets_Layer "SSL _ Wikipedia")
for their authentication, which does look very similar to HTTPS traffic
at first glance, but analyzing the traffic can reveal the differences
between a SSL Handshake performed by a regular https Website and one
made via OpenVPN. There are ways to wrap OpenVPN traffic into different
protocols like SSH, or use Obfuscation to combat this.

Obfuscation seems to be the more widespread and also more useful method.
A famous tool for that are the 'Pluggable Transports' made and used by
the [TOR Project](https://www.torproject.org/ "TOR Project"). The one
that is currently in use by TOR is obfs4 also referred to as the
'Obfourscator'. This obfuscation layer for the
[TCP](https://en.wikipedia.org/wiki/Transmission_Control_Protocol "TCP - Wikipedia")
protocol does transform the traffic in such a way that it is not easily
identifiable anymore. Stuff like packet size, packet timing and more can
be randomized, and the payloads are heavily encrypted.

Another project that uses obfuscation to avoid detection is
[ShadowSocks](https://shadowsocks.org/en/index.html "ShadowSocks Website").
Originally made to bypass the
[GFW](https://en.wikipedia.org/wiki/Great_Firewall "Great Firewall of China - Wikipedia"),
it also is hard to be detected by
[DPI](https://en.wikipedia.org/wiki/Deep_packet_inspection "Deep Packet Inspection - Wikipedia").
By using a pre shared key, every single part of the communication,
including the TCP handshake, are always encrypted and
randomized. Message length and other factors are being randomized as
well. Although there seem to be ways to fingerprint vanilla ShadowSocks
traffic with DPI, most notably by the GFW itself, for most
networks ShadowSocks is a very effective and surprisingly simple way of
bypassing Firewalls. Setting up ShadowSocks-libev Server on a Debian 10
VPS took me a whopping 5 minutes last time I did it.

To tackle even the most sophisticated Firewalls like the GFW, you can
also use [Shadowsocks
Plugins](https://shadowsocks.org/en/spec/Plugin.html "ShadowSocks Plugins")
to make it even harder to get detected. These plugins do even more
things, such as making your traffic look like actual https instead of
just obfuscating it, [Domain
Fronting](https://en.wikipedia.org/wiki/Domain_fronting "Domain Fronting") and
much more. But this is currently only neccessary for the most nefarious
types of Firewalls.

### Some additional things to consider.

There are some more things you should consider when choosing and setting
up a method for bypassing. Some proxies commonly installed in networks
may have problems dealing with
[UDP](https://en.wikipedia.org/wiki/User_Datagram_Protocol "UDP - Wikipedia")
traffic. So setting your connection to TCP only may help. Also, it might
be a good idea to only fire up a connection to your Server when it\'s
actually needed, as being connected to the same server for hours at end
will look suspicious too. Especially when a human might take a look into
some traffic logs. And as a last tip, changing your
[MAC Address](https://en.wikipedia.org/wiki/MAC_address "MAC - Wikipedia")
is good for ban evasion.

### Conclusion

Now all of this is a lot of information, but what is the conclusion?
What do I actually recommend? Well all things considered, I believe
using a ShadowSocks Server that is listening on port 443, TCP only, is a
very solid start. When dealing with an especially sophisticated
Firewall, the various ShadowSocks Plugins will be of help.

For self-hosting, I recommend to get a KVM-VPS running Debian 10.
Shadowsocks-libev is in the debian repos, making it a breeze to install.
And a KMS Server has the least amount of problems for proxies and / or
VPNs. In my experience at least. 

If you don\'t want or can't selfhost [mullvad.net offers ShadowSocks
bridges](https://mullvad.net/en/guides/intro-shadowsocks/ "Mullvad ShadowSocks").
And just before anyone asks, I am not affiliated with them.

### Thanks for reading
