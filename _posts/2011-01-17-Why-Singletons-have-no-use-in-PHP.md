---

layout: post
title: Why Singletons have no use in PHP
tagline: unless you know what you are doing
categories: [oop, design-patterns, php]

---

I am pretty sure everyone working professionally or semi-professionally has heard, seen or worked with a [Singleton][1] before in one way or the other. For those of you who never heard of it, let me reiterate the purpose of that [Design Pattern][2]:

- Make sure there can be only one instance of a class at any time.
- Provide global access to that single instance from anywhere within your application.

You'll often find Singletons as wrappers around database adapters to limit the amount of connections. Another popular use is to make Front Controllers or a Registry into Singletons.

## Implementing Singletons

![UML diagram for a Singleton in PHP](http://getfile9.posterous.com/getfile/files.posterous.com/temp-2011-02-14/jpHEcldfsCfkDDhxfnEuAsiHqqzGgqgksqlxJGGtlyHBwwGidjBGjvpykeuj/Singleton.gif.thumb100.gif?content_part=ImwpIkmEGkfjnyHgJnHg)

Unlike some other patterns, creating a Singleton is easy.

- Add a static `getInstance()` method to allow global access.
  - Call the Singleton's constructor on first call
  - Assign the newly created instance to the static `$instance` property.
  - Return `$instance` on subsequent calls.
- Make `__construct()` private to prevent direct instantiation from outside.
- Make `__clone()` private to prevent cloning from outside.
- Make `__wakeup()` private to prevent deserializing from outside.

There used to be a similar sample implementation in the PHP Manual as well (now removed). [Variations of that implementation exist in other languages][3]. In PHP this one is the dominant variant though, mainly due to language constraints.

However, despite it's apparent usefulness and wide adoption, the Singleton is also controversial. Many developers see it as an AntiPattern nowadays and I tend to agree with them.

## Singletons are not unique snowflakes

In languages where objects live in an application server, Singletons can be used to keep memory usage low. Instead of creating two objects, you reference an existing instance from the globally shared application memory. In PHP there is no such application memory. A Singleton created in one Request lives for exactly that request. A Singleton created in another Request done at the same time will still be a completely different instance. And it will occupy it's own memory. Those instances are not linked to each other. They are completely isolated, because PHP is a Shared-Nothing architecture. You do not have one single unique instance, but many similar instances in parallel processes. Thus, one of the two main purposes of a Singleton is not applicable.

## Don't construct twice, it's all right

Advocates of the Singleton in PHP often argue it's still useful to be able to limit an instance within a single request. The aforementioned database classes being the most prominent example. But the much easier solution would be simply not to instantiate a second instance. If anyone can make sure there is just one instance, it's the developer. If you need to have the same instance in many classes, use [Dependency Injection][4]. [Just create one][5], inject everywhere. That will also save you the hassle of deconstructing your Singleton once you notice you need a second instance of it all of a sudden.

Another example where Singletons are often applied but don't make sense is classes like [FrontControllers][6]. While conceptually it makes sense to say "There may be only one FrontController", it is superfluous to ensure it from an architectural viewpoint. A FrontController is usually instantiated only once in your application's control flow anyway. If you don't write a new Foo; anywhere else, you already made sure there is just one instance. So [you ain't gonna need][7] the Singleton here. Don't express concepts in your code that are never used.

## Don't shoot yourself in the foot

The Singleton's other purpose (to have a global access point to the instance) is undesirable in PHP. The desire for that usually stems from having an architecture where objects pull in their dependencies. Like any globals and statics, the Singleton's `getInstance()` method creates coupling to the global scope. [This makes Unit-Testing harder][8]. There is ways to mitigate this, but in general, the cost to mitigate is higher than to simply avoid the Singleton in favor of Dependency Injection. This is especially true in those situations, where the Singleton is applied but never instantiated twice anyway.

## Closing Notes

When working with PHP, Singletons cannot live up to their full potential due to PHP's Shared Nothing architecture. They are also introducing a number of undesirable disadvantages that will make your application less maintainable and harder to change. And to add another sure sign that you should be wary of the Singleton: even [Erich Gamma][9], one of the pattern's inventors, [doubts the Singleton nowadays][10]:

> I'm in favor of dropping Singleton. Its use is almost always a design smell

Hopefully this is enough to make you reconsider next time you think about using a Singleton. Should you still have trouble deciding, use the following cheatsheet:

![Helpful diagram in case you forget whether you need a Singleton](http://getfile6.posterous.com/getfile/files.posterous.com/temp-2011-01-14/AjfBodqlAaipBjhuGbGIBwoFsuGgojjmoIGBAgjJkDwgttycEfGviAbrqAHC/Singleton.png.thumb100.png?content_part=fxtwkqnutaeahzvvGiFw)

[1]: https://secure.wikimedia.org/wikipedia/en/wiki/Singleton_pattern
[2]: https://secure.wikimedia.org/wikipedia/en/wiki/Design_pattern_%28computer_science%29
[3]: https://secure.wikimedia.org/wikibooks/en/wiki/Computer_Science_Design_Patterns/Singleton
[4]: http://fabien.potencier.org/article/11/what-is-dependency-injection
[5]: http://butunclebob.com/ArticleS.UncleBob.SingletonVsJustCreateOne
[6]: http://martinfowler.com/eaaCatalog/frontController.html
[7]: https://secure.wikimedia.org/wikipedia/en/wiki/You_ain%27t_gonna_need_it
[8]: http://sebastian-bergmann.de/archives/882-Testing-Code-That-Uses-Singletons.html
[9]: https://secure.wikimedia.org/wikipedia/en/wiki/Erich_Gamma
[10]: http://www.informit.com/articles/printerfriendly.aspx?p=1404056