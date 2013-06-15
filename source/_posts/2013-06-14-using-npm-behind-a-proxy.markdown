---
layout: post
title: "Using npm behind a corporate proxy"
date: 2013-06-14 23:12
comments: true
categories: [nodejs,npm,javascript]
---

On a recent assignment, I needed to install npm behind a corporate proxy. I had already set the environment variables `HTTP_PROXY` and `HTTPS_PROXY`. Other command line utilities, like ruby gems, recognized these environment variables. Npm did not.

After some googling, I found the following way to configure the proxy for npm.

{% codeblock lang:bash %}
npm config set proxy http://proxy.company.com:8080
npm config set https-proxy http://proxy.company.com:8080
{% endcodeblock %}

If you need to specify credentials, they can be passed in the url using the following syntax.

`http://user_name:password@proxy.company.com:8080`

Further exploration of the [npm config documentation](https://npmjs.org/doc/config.html) showed that the `npm config set` command sets the proxy configuration in your `.npmrc` file. You can also set the proxy configuration as a command line argument or environment variable.

Configuration parameters can be specified using `--` when executing npm. So the proxy could also be specified as follows.

{% codeblock lang:bash %}
npm --https-proxy=http://proxy.company.com:8080 -g install karma
{% endcodeblock %}

 To pass configurattion parameters to npm as environment variables, they must be prefixed with `npm_config_`. The proxy configuration could be set with environment variables as follows.

{% codeblock lang:bash %}
export npm_config_proxy http://proxy.company.com:8080
export npm_config_https_proxy http://proxy.company.com:8080
{% endcodeblock %}
