---
layout: post
title: "Setting Ubuntu Time Zone"
date: 2012-12-04 20:49
comments: true
categories: [ubuntu,sysadmin]
---

You will eventually get tired of looking at UTC timestamps in your server log files.

[https://help.ubuntu.com/community/UbuntuTime](https://help.ubuntu.com/community/UbuntuTime) has a detailed guide for setting the time zone on your server and synchronizing it's clock.

Here are the commands I used to set my time zone and synchronize my clock on Ubuntu 12.04.1 LTS.

**Set time zone**
{% codeblock lang:bash %}
sudo dpkg-reconfigure tzdata
{% endcodeblock %}

**Synchronize clock**
{% codeblock lang:bash %}
sudo apt-get install ntp
{% endcodeblock %}
