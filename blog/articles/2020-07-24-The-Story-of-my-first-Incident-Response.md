The Story of my first “Incident Response”
=========================================

Today, I felt like sharing one of my favourite experiences that I had in my still short career as a Web Developer. It’s a Story in which I am tasked with investigating a server issue, which quickly lead to me detecting a hacked system.

Prologue
--------

The Summer rolled around and schools closed for the summer break. So this was the time of the year where people went on their hard earned vacations. Both of my co-developers, but also a lot of Customers, would be unavailable for some time. I finally had some time to work on that ticket that was sitting patiently in my backlog for about a week. This ticket was created by our internal IT department that provided us with our virtual web servers, database servers and the load balancer.

One day, their monitoring detected that one of the older database servers would freak out every other weekend. The [MySQLbinlogs](https://dev.mysql.com/doc/refman/5.7/en/mysqlbinlog.html) would grow rapidly to be several hundred gigabyte in size, eventually filling up all the space and crashing the server. Since it was actually my department’s job to care for those servers, the task was given to me. MySQLbinlogs were temporarily disabled before I would start my investigation on the issue.

The Investigation
-----------------

I already had an vague idea about what might have caused these problems. Since the actual databases were not increasing in size at all, and the behaviour was _only_ present on the weekend, I suspected one of our bigger customers was behind all of that. Said customer was a fairly big retailer of sports gear, and their eCommerce platform was connected to their inventory management system. Updating large amounts of stock on the weekends would explain the spike.

To prove my Theory, I wrote a simple bash one-liner that would count each occurrence of any database name in the logs. The second highest count of database transactions were indeed from the sports gear retailer I suspected. Each weekend, a couple thousand database events were logged for that database. However, the database with the _most_ logged events had _several millions events_ recorded in a matter of minutes.

So this one was definitely the culprit. The weird part was that this was only a small landing page for a specific product, which was discontinued many years ago. The database for this site had nothing in it except one single table containing about a dozen image paths. This made no sense at all.

At this point, it made ‘click’. I navigated to the site in question and listed all .php files using [find](https://linux.die.net/man/1/find). The names Dude.php, lndex.php (with an L) and fuck.php appeared on my screen. Those were webshells. This site was hacked.

It turned out, that one of the Webshells had a feature that tried to dump the database of a WordPress installation. If it didn’t succeed, it would just…try again indefinitely for whatever reason. But this was not a WordPress installation. So once _someone_ started that script, it would run and run and while doing so, fill up the logs very rapidly.

Securing the area
-----------------

After finding out about the Hack, I immediately informed our project manager and after sitting down with the IT department we started to plan pur next steps. Basically the plan was to analyse the whole scale of the attack, finding the root cause of it and finally securing the affected systems.

Additionally, the whole process had to be documented and the customer was immediately notified and to be updated regularly. As of that moment, there was NO indication of user data being affected. Thankfully, our systems are compartmentalized, and the affected hosting only included three fairly old landing pages and no important infrastructure.

To find other potentially compromised sites, we would build some scripts that would scan all of our hostings for signs of compromise. Webshells are essentially made to have someone run commands through them. Just like a Shell, hence the name. So these scripts typically included commands like `system`, `exec` and similar. Some webshells are obfuscated and included commands like `str_rot13`, `base64_decode` and almost always `eval`. [IonCube](https://www.ioncube.com/) protected scripts were also identifiable.

Running scripts on every single file that would check for the above mentioned criteria, and then manually inspecting the result to filter out false positives left us happy. Only the system we initially discovered to be hacked seemed to be affected. The (more experienced) IT Team also re-did a full system scan a couple days later with some more sophisticated scanning software. This did not find anything either.

We also searched all available MySQLbinlogs for events that mirrored those we found for the hacked system. None of them were executed against a different database.

Everything came up clean.

The root cause of the hack was also quickly discovered. This particular hosting was not originally developed or hosted by us. The customer moved away from another agency to partner up with us, and the already existing sites were migrated over to our systems _years_ ago. The sites were put into version control as soon as they were migrated over to our systems. And this proved that the malicious files were already present on day one. Because the _very first commit_ already included them!

It was however not clear to us, why the webshells were never touched for years (the server only started acting up the two weeks before) and why someone would try to run a database extraction script multiple times, while the script was failing each time.

Cleaning up
-----------

This part was pretty easy. The affected sites were not of any importance anymore, and so it was no issue for us to use [HTTrack](https://www.httrack.com/) to make a static version of this once dynamic website and disable PHP for the hosting.

It was thanks to the great work of our IT Department and our just as great Senior Developer that this hack has caused so little damage! They are the ones that properly compartmentalized the hostings, locked down the [php.ini](https://docs.jelastic.com/php-security-settings/), ran proper monitoring and much more. If the hostings would have been improperly secured and unmonitored, this could have been a lot worse than it turned out to be.

Thats about it.

Thanks for reading
