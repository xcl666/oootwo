---
title: Run JavaScript from command line in Linux
id: 57
categories:
  - computer_language
date: 2017-08-31 12:16:03
tags:
---

Javascrip is becoming a more and more popular language over time, and now use of Javascript is not limited to just browsers, even microcontrollers started running javascript.

There are many promising javascript based projects like,

Node-RED , visual IoT wiring platform, more here.
DVD.js to play DVDs in browser, more here.
Espruino , javascript for Microcontrollers, more here.
SMART.js , another javascript for microcontrollers, IoT specific.
BoneScript , node.js library for beagleboard with hardware access, more here.
As we can see javascript has a very bright future ahead, lets start playing with some javascript stuff in Linux, i.e. run javascript from command line.

Getting started with javascript on command line

First we need a javascript engine, which could interpret with the javascript from command line, and there are lot of them, list of javascript engines.

So it’s somewhat confusing to choose the proper javascript engine, first start with the two big brothers, v8 from Google and SpiderMonkey from Mozilla.

Note: v8 and SpiderMonkey runs the javascript in somewhat different way, some code may not be compatible or interchangeable between two engines.

The installation process is different for different GNU/Linux distros, but usually it’s easy. Here is how to install them on any Debian based distros like Ubuntu, Linux Mint etc. etc.

Run JavaScript with Node.js , v8 engine

Node.js uses the v8 engine and it’s very popular, though you could use v8 without Node.js, but that’s unnecessary.

sudo apt-get install nodejs
The best way to install the cutting edge Node.JS is read their installation instruction from source.

Example:~ You can use the node REPL prompt directly with the nodejs or node command, which is quite dubious, so write a little javascript code and execute it, a Hello, World! in javascript,

console.log(Hello, World!);
Now run the script like bellow

user@host:~$ node hello.js
Hello, World!
A very simple BMI calculator in javascript, not fault tolerant

var mass = +process.argv[2];
var height = +process.argv[3];
BMI = mass / Math.pow(height, 2);
console.log(BMI);
Save it as whatever you want and execute it like bellow

node bmi_calc.js mass_in_Kg height_in_meter
￼

Run JavaScript with the SpiderMonkey engine

This is the first ever javascript engine, created by Netscape, further developed by Mozilla. Install it in any Debian based distro with apt-get,

sudo apt-get install libmozjs-24-bin
The javascript interpret is /usr/bin/js24, again you could use the REPL prompt or write some javascript app.

Example:~ JavaScript code to calculate factorial from 1 to 10 and print the results.

function factorial(n)
{ if (n == 0)
return 1;
else
return n * factorial(n-1);
}
var i;
for (i = 0; i &lt;= 10; i++)
print(i + "! = " + factorial(i));
￼Read more about SpiderMonkey engine and it’s built in functions here, Introduction to the JavaScript shell .

Some other JavaScript engines worth to mention

As you can see there are lot of javascript engines available, it’s difficult to choose which one to use, currently Node.js gained more popularity than others.

Some javascript engines worth to mention

Nashorn, developed by Oracle, written in Java.
Rhino, also written in Java and developed by Mozilla.
Duktape, little and embeddable javascript engine.
v7, very lightweight yet powerful, only two files in the source code, v7.c and v7.h
Chakra, developed by Microsoft, recently open-sourced as ChakraCore .
Each of the engines includes own set of features or built in functions, so if a javascript app is written to use with Node.js/v8 engine, probably it will nor work with other engines.

Conclusion

That’s it, how to run javascript from command line, now javascript experts it’s your turn, write awesome apps with javascript let everyone know through the comments.

I’d also like to hear some suggestion or questions about this.

From:: https://www.pcsuggest.com/run-javascript-from-command-line-linux/