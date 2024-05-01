---
layout: post
title:  "Block any https website on DD-WRT router"
summary: "Block any https website (facebook, xxx sites, etc...) on DD-WRT router with iptables"
author: dieudv
date: '2020-11-25 00:00:00 +0700'
category: 'project'
thumbnail: /assets/img/posts/block-facebook.png
keywords: block https site, dd wrt, tptables
usemathjax: true
permalink: /blog/block-any-https-website-on-dd-wrt-router
---


DD-WRT is a kind of firmware that build on Linux operating system for wireless router and access point. It can replace with orginal firmware of manufacturers, and has more features. Nowaday, it applies for many models.

Firmware is software that's embedded in a piece of hardware. You can think of firmware simply as "software for hardware." However, firmware is not an interchangeable term for software.

Follow Block any https website in route with iptables on DD-WRT router for more interesting information.



Block any https website in route with iptables on DD-WRT router
Here is how I was able to do this
(1) Find out all the IP space that belongs to Facebook
---(a) Google'd for Facebook's BGP AS number -> AS32934
---(b) Looked up all the routes for AS32934 on as.robtex.com
---(c) Self aggregated all the IP space.

(2) Build a set of rules in IPTABLES that:
---(a) Define the FB destinations
---(b) Define the local sources
---(c) can be triggered into use based on a cron schedule.

In order to use the above configuration, there are some prerequisites
(1) This method of configuration is via the CLI interface. If someone wants to take the time to put this into GUI instructions, go right ahead. I'm old school.
---(a) Make sure that SSH is enabled.
----- Services
------- Services
--------- Secure Shell
----------- SSHd Enabled
----------- Password Login Enabled
----------- Default Port {22}
---(b) You'll need a SSH Client - I suggest PuTTY if using Windows.

(2) You'll need to check your memory usage and availability
---(a)
Code:

cat /proc/meminfo
---(b)
Code:

nvram show | grep free
--- (make sure you have at least 2K+ free)

(3) Due to some cron bugs, you'll need to be running v24-sp2

The way of configuration works
(1) The IPTABLES chain that looks at traffic that flows across your router is the "FORWARD" chain of the filter table. This procedure inserts a sequence of chains into this chain to intercept and check traffic that *might* be going to the FB IPs.

(2) The new sequence of chains are inserted after the normal DD-WRT Access Restrictions rules and before the rule that allows related and established connections.

In my router, the rule number to insert at is number 6 - yours may differ. This is how to check:

Code:

iptables -L FORWARD --line-numbers
Quote:

Chain FORWARD (policy ACCEPT)
num target prot opt source destination
1 {SNIP}
2 {SNIP}
3 {SNIP}
4 {SNIP}
5 lan2wan 0 -- anywhere anywhere
6 ACCEPT 0 -- anywhere anywhere state RELATED,ESTABLISHED
7 {SNIP}
8 {SNIP}
9 {SNIP}
10 {SNIP}
11 {SNIP}
12 {SNIP}

See here that the "lan2wan" target (normal DD-WRT Access Restrictions) is in line number 5 and the ACCEPT for RELATED and ESTABLISHED in in line number 6. I inserted to line 6 to get this (I'll show how here shortly):

Code:

iptables -L FORWARD --line-numbers
Quote:

Chain FORWARD (policy ACCEPT)
num target prot opt source destination
1 {SNIP}
2 {SNIP}
3 {SNIP}
4 {SNIP}
5 lan2wan 0 -- anywhere anywhere
6 FACEBOOK_CHK 0 -- anywhere anywhere
7 ACCEPT 0 -- anywhere anywhere state RELATED,ESTABLISHED
8 {SNIP}
9 {SNIP}
10 {SNIP}
11 {SNIP}
12 {SNIP}
13 {SNIP}

(3) Now packets will flow thru the rules and at rule 6 jump to check for facebook and block if told to:

How to know blocking ready for work?
When Blocking enforced

Quote:

FORWARD --> FACEBOOK_CHK: Told to "jump" to FACEBOOK_DST
FACEBOOK_CHK --> FACEBOOK_DST: If match, jump to FACEBOOK_SRC // No match, return to FORWARD
FACEBOOK_DST --> FACEBOOK_SRC: If match, drop/allow packets // No match, return to FACEBOOK_DST

When Blocking not enforced

Quote:

FORWARD --> FACEBOOK_CHK --> back to FORWARD

How to put it all into effect
I would highly suggest you test your configuration using the following procedure before saving to NVRAM:

Step 1: Build all the new IPTABLES Chains that you will need:
Code:

iptables -N FACEBOOK_CHK
iptables -N FACEBOOK_DST
iptables -N FACEBOOK_SRC
Step 2: Define the FACEBOOK_DST chain (you don't need to modify this)
Code:

iptables -A FACEBOOK_DST -d 31.13.24.0/21 -j FACEBOOK_SRC
iptables -A FACEBOOK_DST -d 31.13.64.0/19 -j FACEBOOK_SRC
iptables -A FACEBOOK_DST -d 66.220.144.0/21 -j FACEBOOK_SRC
iptables -A FACEBOOK_DST -d 66.220.152.0/21 -j FACEBOOK_SRC
iptables -A FACEBOOK_DST -d 69.63.176.0/21 -j FACEBOOK_SRC
iptables -A FACEBOOK_DST -d 69.63.184.0/21 -j FACEBOOK_SRC
iptables -A FACEBOOK_DST -d 69.171.224.0/20 -j FACEBOOK_SRC
iptables -A FACEBOOK_DST -d 69.171.240.0/20 -j FACEBOOK_SRC
iptables -A FACEBOOK_DST -d 74.119.76.0/22 -j FACEBOOK_SRC
iptables -A FACEBOOK_DST -d 103.4.96.0/22 -j FACEBOOK_SRC
iptables -A FACEBOOK_DST -d 173.252.64.0/19 -j FACEBOOK_SRC
iptables -A FACEBOOK_DST -d 173.252.96.0/19 -j FACEBOOK_SRC
iptables -A FACEBOOK_DST -d 204.15.20.0/22 -j FACEBOOK_SRC
Step 3: Define how you want to handle your local source (mod to suit):
---(a) Define hosts to block, allow all others:

Code:

iptables -A FACEBOOK_SRC -s 192.168.1.20 -j logdrop
iptables -A FACEBOOK_SRC -s 192.168.1.21 -j logdrop
iptables -A FACEBOOK_SRC -s 192.168.1.22 -j logdrop

---(b) Define hosts to allow, block all others:

Code:

iptables -A FACEBOOK_SRC -s 192.168.1.20 -j logaccept
iptables -A FACEBOOK_SRC -s 192.168.1.21 -j logaccept
iptables -A FACEBOOK_SRC -s 192.168.1.22 -j logaccept
iptables -A FACEBOOK_SRC -j logdrop
Step 4: Insert the FACEBOOK_CHK into the FORWARD chain. (Make sure you use the right number determined earlier)
Code:

iptables -I FORWARD 6 -j FACEBOOK_CHK
Step 5: (You are not blocking anything yet.) Decide if you want to start blocking right now, or wait until the schedule kicks in.
---(a) Start Blocking right now:

Code:

iptables -A FACEBOOK_CHK -j FACEBOOK_DST

---(b) Wait till schedule kicks in: Go to next section.

Step 6: Setup schedule
In my example, I allow FB access from midday to one o'clock on weekdays and all the time on weekends:

Here is the format for cron jobs (if you didn't already know)

minute (0-59)
|| hour (0-23)
|| | day of the month (1-31)
|| | | month of the year (1-12)
|| | | | day of the week (0-6 with 0=Sunday)
|| | | | | commands
---(a) Stop cron service:

Code:

stopservice cron

---(b) Recreate /tmp/cron.d subdirectory:

Code:

mkdir -p /tmp/cron.d

---(c) Recreate /tmp/cron.d/check_ps job

Code:

echo '*/2 * * * * root /sbin/check_ps' >> /tmp/cron.d/check_ps
---(d) Create /tmp/cron.d/cron_jobs job that holds custom cron jobs:

Code:

echo '00  12 * * * root /usr/sbin/iptables --flush FACEBOOK_CHK' >> /tmp/cron.d/cron_jobs
echo '00  13 * * 1-5 root /usr/sbin/iptables -A FACEBOOK_CHK -j FACEBOOK_DST' >> /tmp/cron.d/cron_jobs

---(e) Start cron service:

Code:

startservice cron

Now - if everything works as you desire, write it to NVRAM and commit:
(Double / Triple / Quadruple check this - you don't want to loose access to your router during a reboot)('Embarassed')

Code:

nvram set rc_firewall="iptables -N FACEBOOK_CHK
iptables -N FACEBOOK_DST
iptables -N FACEBOOK_SRC
iptables -I FORWARD 6 -j FACEBOOK_CHK
iptables -A FACEBOOK_CHK -j FACEBOOK_DST
iptables -A FACEBOOK_DST -d 31.13.24.0/21 -j FACEBOOK_SRC
iptables -A FACEBOOK_DST -d 31.13.64.0/19 -j FACEBOOK_SRC
iptables -A FACEBOOK_DST -d 66.220.144.0/21 -j FACEBOOK_SRC
iptables -A FACEBOOK_DST -d 66.220.152.0/21 -j FACEBOOK_SRC
iptables -A FACEBOOK_DST -d 69.63.176.0/21 -j FACEBOOK_SRC
iptables -A FACEBOOK_DST -d 69.63.184.0/21 -j FACEBOOK_SRC
iptables -A FACEBOOK_DST -d 69.171.224.0/20 -j FACEBOOK_SRC
iptables -A FACEBOOK_DST -d 69.171.240.0/20 -j FACEBOOK_SRC
iptables -A FACEBOOK_DST -d 74.119.76.0/22 -j FACEBOOK_SRC
iptables -A FACEBOOK_DST -d 103.4.96.0/22 -j FACEBOOK_SRC
iptables -A FACEBOOK_DST -d 173.252.64.0/19 -j FACEBOOK_SRC
iptables -A FACEBOOK_DST -d 173.252.96.0/19 -j FACEBOOK_SRC
iptables -A FACEBOOK_DST -d 204.15.20.0/22 -j FACEBOOK_SRC
iptables -A FACEBOOK_SRC -s 192.168.1.20 -j logdrop
iptables -A FACEBOOK_SRC -s 192.168.1.21 -j logdrop
iptables -A FACEBOOK_SRC -s 192.168.1.22 -j logdrop"

nvram set cron_jobs="00  12 * * * root /usr/sbin/iptables --flush FACEBOOK_CHK
00 13 * * 1-5 root /usr/sbin/iptables -A FACEBOOK_CHK -j FACEBOOK_DST"
nvram commit

You're Done!!!. Happy FB Blocking!! Laughing