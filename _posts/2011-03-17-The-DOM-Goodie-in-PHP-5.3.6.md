---

layout: post
title: The DOM Goodie in PHP 5.3.6
tags: [php, xml]

---

PHP 5.3.6 has been released today. There is a lot of improvement and bugfixes that are worth mentioning. But the one that made me particularly excited was this one:

> Implemented [FR #39771][1] (Made DOMDocument::saveHTML accept an optional DOMNode like DOMDocument::saveXML). (Gustavo)

If you have worked with [DOM][6] before, you know that this will ease working with broken HTML a lot, because now you can do

~~~ php
    $dom = new DOMDocument;
    $dom->loadHtml('<div id="content"><p>Some<br>HTML Fragment</p></div>');
    echo $dom->saveHTML($dom->getElementById('content'));
~~~

and get

~~~ html
    <div id="content"><p>Some<br>HTML Fragment</p></div>
~~~

## Why is it cool?

DOM is based on [libxml][7]. So it is primarily intended for working with XML. HTML isn't XML at all, but is based on SGML. Different rules. Unfortunately, even after years of advocating web standards, most of the web is still broken HTML. Pick a random site on the web and run it through validator.w3.org. My guess is at least eight out of ten sites will not validate (including this blog - not my fault though). And just to make this clear: I don't have any hopes that [TMFKAH][2] will improve the situation. A well formed web will forever be a Pipe Dream.

The good news is: despite common misbeliefs, DOM can also parse broken HTML. When you use `loadHTML()` or `loadHTMLFile()`, DOM will internally switch to it's [HTML Parser Module][3] and parse the markup as HTML4 Transitional.

The bad news is: when using the HTML Parser Module, libxml will also add a basic HTML skeleton to make sure it can parse the HTML somehow. This is a nasty unobvious side-effect, because when traversing the DOM with

~~~ php
    echo $dom->documentElement->firstChild->nodeName;
~~~

you would expect it to output 'p', but it will output 'body'. Consequently, when we used `saveHTML()`, we would get the following output (shortened DocType for readability):

~~~ html
    <!DOCTYPE html PUBLIC "blah">
    <html><body><div id="content"><p>Some<br>HTML Fragment</p></div></body></html>
~~~

To make matters worse: with `saveXML()` you can pass in a node to be dumped. With `saveHtml()` you couldn't (until now). So when you were dealing with HTML fragments, you had no way to get just a particular node or fragment back from DOM. You could get all or nothing. The only two options you had was [manually removing the HTML skeleton somehow][4] or dump the wanted nodes with saveXml instead. Using saveXml had the problem that it would format any markup according to XML rules as well, so `<br>` would become `<br/>`. If you didn't intend your markup to be XHTML, this is unwanted.

But with PHP 5.3.6 we can finally pass a node to `saveHtml`. And that's very cool!

Tweet a "Thank you" to [Gustavo][5] for implementing it.

  [1]: http://bugs.php.net/bug.php?id=39771
  [2]: http://blog.whatwg.org/html-is-the-new-html5
  [3]: http://xmlsoft.org/html/libxml-HTMLparser.html
  [4]: http://php.net/manual/en/domdocument.savehtml.php#85165
  [5]: https://twitter.com/cataphractpt
  [6]: http://www.php.net/manual/en/book.dom.php
  [7]: http://www.xmlsoft.org/