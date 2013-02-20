---
layout: post
title: Iterating File Contents with SPL
---

I noticed a lot of people are still using the classic filepointer approach to read a file line by line:

{% highlight php %}
    $handle = fopen ("file.txt", "r");
    while (!feof($handle)) {
        $buffer = fgets($handle);
        echo $buffer;
    }
    fclose ($handle);
{% endhighlight %}

While there is nothing wrong with doing things the old school way, PHP also offers `SplFileObject` for quite some time now:

{% highlight php %}
    $file = new SplFileObject("file.txt");
    while (!$file->eof()) {
        echo $file->fgets();
    }
{% endhighlight %}

Not only does this shorten your code by two lines, but it also let's you work with an Object instead of a Resource now. Almost all of the procedural functions available for file handling are also available as methods of `SplFileObject`.

If that's not enough reason to switch already, `SplFileObject` also implements the `Iterator` interface, which means you can shorten the above code to a simple `foreach` loop:

{% highlight php %}
    foreach (new SplFileObject("file.txt") as $lineNumber => $content) {
        printf("Line %d: %s", $lineNumber, $content);
    }
{% endhighlight %}

There is more. Because `SplFileObject` also implements `SeekableIterator` you can easily jump to specific lines without having to count lines via some temp variable in your loop. How much more convenient can it get?

{% highlight php %}
    $file = new SplFileObject("file.txt");
    $file->seek(9);        // zero-based, so it's line 10
    echo $file->current(); // outputs line 10
{% endhighlight %}

And of course you can stack an `SplFileObject` into other Iterators, for instance the `LimitIterator` to limit how many lines should be iterated over:

{% highlight php %}
    $linesTenToTwentyIterator = new LimitIterator(
        new SplFileObject("file.txt"),
        9, // start at line 10
        10 // iterate 10 lines
    );
    foreach ($linesTenToTwentyIterator as $line) {
        echo $line; // outputs line 10 to 20
    }
{% endhighlight %}

`SplFileObject` is complemented by `SplTempFileObject` and `SplFileInfo`. The first offers an object oriented interface for a temporary file, including in-memory files. As such it is similar to file pointers opened with `php://temp` or `php://memory` as file descriptors.

`SplFileInfo` offers a high-level object oriented interface to information for an individual file. This includes methods for getting the realpath, basename and so on. `SplFileInfo` is actually the parent class of the other two.

So next time you're going to whip out another file pointer, remember there is a nice OO alternative.

### Reference

- [The SplFileObject class](http://php.net/manual/en/class.splfileobject.php)
- [The SplTempFileObject class](http://php.net/manual/en/class.spltempfileobject.php)
- [The SplFileInfo class](http://php.net/manual/en/class.splfileinfo.php)
- [The SeekableIterator interface](http://php.net/manual/en/class.seekableiterator.php)
- [The Iterator Interface](http://php.net/manual/en/class.iterator.php)
- [The LimitIterator Class](http://php.net/manual/en/class.limititerator.php)

