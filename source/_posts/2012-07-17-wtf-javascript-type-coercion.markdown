---
layout: post
title: "WTF Javascript - Type Coercion"
date: 2012-07-17 01:27
comments: true
categories: [javascript]
---

I recently came across the site wtfjs.com. It highlights some idiosyncrasies of the Javascript language. It’s worth a look, you’ll get a deeper understanding of the Javascript language.

This entry submitted by @diogobaeder held my attention. The solutions was not immediately obvious to me so I did some digging. Once I found the correct type coercion rules the result were logical.

{% codeblock lang:javascript %}
var foo = [0];
console.log(foo == foo); 	// true
console.log(foo == !foo);	// true - ???
{% endcodeblock %}

These examine this step by step.

{% codeblock lang:javascript %}
foo == foo
{% endcodeblock %}

The above was obvious. References to the same object evaluate to true.

{% codeblock lang:javascript %}
foo == !foo
{% endcodeblock %}

The expression above took a little longer to decipher. 

<!-- https://developer.mozilla.org/en/JavaScript/Reference/Operators/Comparison_Operators -->

First the precedence rules come into play.

{% codeblock lang:javascript %}
![0];         // conversion to Boolean(), false
[0] == false; // true
{% endcodeblock %}

If either operand is a number or a boolean, the operands are converted to numbers.

{% codeblock lang:javascript %}
Number(false) == 0;
Number([0]) == 0;

0 == 0;
{% endcodeblock %}

