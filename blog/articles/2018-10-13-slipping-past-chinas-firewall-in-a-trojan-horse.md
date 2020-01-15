# Slipping past China’s Firewall in a Trojan Horse

Sometime in 1260–1180 BC some smart Greek dudes used a “Trojan Horse” to smuggle their soldiers inside of the city of Troy. In 2019 some smart Chinese dudes use a software called “Trojan” to smuggle their TCP/IP Packets outside of the country. And I think that’s just as exciting.

Continuing to research about Firewalls and bypassing them just as in my previous two blogposts, I was made aware of the [Trojan Project on Github](https://github.com/trojan-gfw/trojan) by a guy called [itshaadi](https://github.com/itshaadi). He and another Chinese guy confirmed that Trojan could successfully hide their traffic well enough to bypass their respective censorship machines.

What does Trojan do?
--------------------

The theory behind Trojan is fairly simple, yet brilliant. Trojan, like many other tools that are made for censorship circumvention, imitates HTTPS traffic. The catch however is, that a Trojan Server also serves a legitimate Website or Service at the same time. If a normal user connects to a Trojan Server on the HTTPS port 443, he will be served a legitimate website or service. It’s worth noting that you can redirect such requests to ANY service on your server that you want to. It can work with any web server (NGINX, Apache2, Caddy etc.) or just about any service. As long as you have control over Port 443 and Trojan configured properly, you can do what you want really.

When a non-Trojan request happens, Trojan handles it seamlessly. No weird redirects or anything happen which might raise some suspicions. It just behaves normal. So if you host a website on that server, all the user will see is a normal website, just as expected. If YOU however connect to the same server on the same port, using a correctly structured request and a valid password, you will be able to use the Trojan server as a proxy and finally bypass these Firewalls! All this closely imitates normal HTTPS traffic, so neither a firewall or a SysAdmin will be able to tell that you are actually bypassing a firewall right now.

itshaadi made a boilerplate for using Trojan alongside NGINX. This differs from the original implementation, but it does show a very useful setup, and is actively deployed to circumvent censorship as I write this text. Here is a illustration from his project:

![image](https://user-images.githubusercontent.com/10201704/66357447-c6f98000-e97b-11e9-9d28-ddc32205cc62.jpg)

Make sure to [check his repo out!](https://github.com/itshaadi/trojan-autoconf/)

In that particular setup, traffic is divided into HTTP and HTTP**S**. On port 80, the server runs NGINX, to be able to serve normal websites. Port 443 is where Trojan resides. If it receives non-Trojan traffic, it will _internally_ [reverse proxy](https://de.wikipedia.org/wiki/Reverse_Proxy) it to NGINX. This way, a normal user of the website will still be using a HTTPS connection. Now if you connect to that server using Trojan, it acts as a proxy to the outside world for you. The traffic you get using Trojan looks like a standard HTTP keep-alive or WebSocket connection.

Why is that so great.
---------------------

The way Trojan works is great to avoid a proxy server being identified as such. This hopefully stops anyone from blacklisting your proxy. Ideally, you serve a legitimate website or service on such a server. This may be a Blog, a gitea instance or hundreds of pictures of cats in skirts. Now add a nice looking domain name and maybe even a bought SSL Certificate from a respected CA and you are golden. Hiding in all that legit traffic is just like hiding in a big ’ol Trojan Horse. Just with less angry Greeks this time.

Installing and using Trojan
---------------------------

I am not going to give you an in-depth install guide here. Trojan is a very versatile and flexible piece of software. You have to think about what kind of solution YOU want to build with it, what YOUR threat model is and so on and so forth. Even according to their own website, Trojan is kinda complex. To quote them:

> Unless you are an expert, you shouldn’t configure a Trojan server all by yourself.

The aforementioned project by itshaadi can help you lots, but it’s still recommended to avoid setting up a Trojan server if you aren’t all that experienced with servers. Especially when using something like Trojan might get you in trouble.

It’s quite the contrast to setting up ShadowSocks, which usually takes me about 5 minutes, and I think even a newbie can do in an hour or two.

Something that you should also keep in mind, is that while there is an [Android app](https://github.com/trojan-gfw/igniter/releases "Trojan Android App") it is currently in Pre-Alpha. So most likely barely usable. To connect to your Trojan server, I recommend that you use a proper computer with Trojan installed. The Trojan website mentions that they work on making Trojan a ShadowSocks plugin, which would make all the various ShadowSocks clients work with it. But that isn’t usable as of now.

### Thanks for Reading!

Big thanks to itshaadi for helping me out on this one!
