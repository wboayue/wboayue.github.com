---
layout: post
title: "Ruby performance patches"
date: 2013-03-02 13:00
comments: true
categories: [ruby,rails,rvm]
---

There are a several ruby performance patches, like the [falcon patches](https://gist.github.com/funny-falcon), that may improve the performace of your application.

I use rvm and was pleased to learn that rvm supports compiling ruby with serveral of these performance patches. Using rvm with the *railsexpress* patch, I saw a 20% reduction in the time required to run the test suite for a large rails project. 

Here is how you can install ruby with the *railexpress* patch using rvm.

First make sure you have the latest version of rvm.

{% codeblock lang:bash %}
rvm get head
{% endcodeblock %}

Next install ruby 1.9.3 with the railsexpress patch. At this step rvm may have dependencies that require installation.

{% codeblock lang:bash %}
rvm install 1.9.3 --patch railsexpress
{% endcodeblock %}

The *railsexpress* patch contains the following patches. 

* [01-fix-make-clean.patch](https://github.com/skaes/rvm-patchsets/blob/master/patches/ruby/1.9.3/p392/railsexpress/01-fix-make-clean.patch)
* [02-railsbench-gc.patch](https://github.com/skaes/rvm-patchsets/blob/master/patches/ruby/1.9.3/p392/railsexpress/02-railsbench-gc.patch)
* [03-display-more-detailed-stack-trace.patch](https://github.com/skaes/rvm-patchsets/blob/master/patches/ruby/1.9.3/p392/railsexpress/03-display-more-detailed-stack-trace.patch)
* [04-fork-support-for-gc-logging.patch](https://github.com/skaes/rvm-patchsets/blob/master/patches/ruby/1.9.3/p392/railsexpress/04-fork-support-for-gc-logging.patch)
* [05-track-live-dataset-size.patch](https://github.com/skaes/rvm-patchsets/blob/master/patches/ruby/1.9.3/p392/railsexpress/05-track-live-dataset-size.patch)
* [06-webrick_204_304_keep_alive_fix.patch](https://github.com/skaes/rvm-patchsets/blob/master/patches/ruby/1.9.3/p392/railsexpress/06-webrick_204_304_keep_alive_fix.patch)
* [07-export-a-few-more-symbols-for-ruby-prof.patch](https://github.com/skaes/rvm-patchsets/blob/master/patches/ruby/1.9.3/p392/railsexpress/07-export-a-few-more-symbols-for-ruby-prof.patch)
* [08-thread-variables.patch](https://github.com/skaes/rvm-patchsets/blob/master/patches/ruby/1.9.3/p392/railsexpress/08-thread-variables.patch)
* [09-faster-loading.patch](https://github.com/skaes/rvm-patchsets/blob/master/patches/ruby/1.9.3/p392/railsexpress/09-faster-loading.patch)
* [10-falcon-st-opt.patch](https://github.com/skaes/rvm-patchsets/blob/master/patches/ruby/1.9.3/p392/railsexpress/10-falcon-st-opt.patch)
* [11-falcon-sparse-array.patch](https://github.com/skaes/rvm-patchsets/blob/master/patches/ruby/1.9.3/p392/railsexpress/11-falcon-sparse-array.patch)
* [12-falcon-array-queue.patch](https://github.com/skaes/rvm-patchsets/blob/master/patches/ruby/1.9.3/p392/railsexpress/12-falcon-array-queue.patch)
* [13-railsbench-gc-fixes.patch](https://github.com/skaes/rvm-patchsets/blob/master/patches/ruby/1.9.3/p392/railsexpress/13-railsbench-gc-fixes.patch)
