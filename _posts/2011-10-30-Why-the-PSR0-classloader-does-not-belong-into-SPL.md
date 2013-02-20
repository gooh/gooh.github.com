---
layout: post
title: Why the PSR-0 Classloader does not belong into SPL
---

There is currently an [RFC in the PHP Wiki proposed by the PSR Standards Group about
including a classloader into SPL][1] that will autoload classes following the PSR-0 File
and Class naming convention.

In case you dont know what the [PSR Group][2] is, here is some background

> In the mid of 2009, several lead developers started an initiative called PHP Standards Group (aka. Framework Interoperability Group), which is mainly focused on interoperability between different Open Source projects.

Let's not discuss whether it was a good idea to adopt the name PHP Standards Working
Group although they are not in the position to define anything official for PHP at all.
Rather, let's discuss whether we want to add code to native PHP that requires a
developer to adopt a certain [code convention][6]. The term convention is important here,
because that's what PSR-0 is. It is not a standard, but a convention; followed by
a certain interest group connected by a certain need: framework interoperability.

Framework interoperability is a reasonable goal. Being able to painlessly plug Doctrine
into Symfony and add ZF on top will surely make the lifes of those that need such setups
in their application easier. I'd claim though that for the majority of PHP users such
setups are not a requirement. Why would those people need to follow PSR-0 just to
use a piece of native PHP code then?

> Coding conventions are not enforced by compilers. As a result, not following some or all of the rules has no impact on the executable programs created from the source code.

PHP works with any convention, not just one convention. PHP does not define a particular
coding *standard* for userland code. There is a few tips and [guidelines for how to
name code in the global scope][3], but that is not a standard, nor a convention.
It's incomplete.

One could assume that since all examples in the PHP Manual follow PEAR convention, PEAR
is the agreed upon convention in PHP, but that is simply not true. In fact, a lot of the
projects that now participate in PSR did grow to reasonable size by inventing their own
coding convention or tweaking an existing one. They didn't need a general standard then,
so why force one unto us now? By their success they have already proven that we don't
need such a thing in PHP.

The C implementation of the suggested ClassLoader is from PEAR's own David Coallier.
Yet, despite PEAR and autoloading being around for much longer than the PSR group, we
do not have any code in PHP that requires us to follow PEAR convention. Ironically, if
all of the projects taking part in PSR had followed PEAR convention for file and
class naming right from the start they wouldnt have an interoperability problem now.
But apparently, they didnt feel PEAR was good enough then. Who guarantees that they
won't abandon PSR in five years again? I'd rather have developers [follow a convention by
conviction][4] than by [embedding it into PHP][5].

To stress this, I am not against having a native classloader. But I am against
putting it into SPL when it requires PSR-0. No other function in PHP requires us to use
a certain code convention. The argument that it is optional doesn't count. It is not
a general purpose classloader when I have to follow PSR-0 for it and thus it
shouldn't be in SPL.

Also, what the PSR group should take into account is that frameworks evolve and change
much faster and often than PHP. If they want their code to be in the PHP trunk, they
have to follow PHP's release cycles, which will make it a lot harder to introduce new
features and BC breaks. Putting the classloader into a PECL extension would make much
more sense then.

Incidentally, there [already is a project in PECL][7] that brings it's own classloader.
And in fact, YAF sounds a lot like where the PSR group is heading. The ClassLoader is
just the tip of the iceberg. [Once that one is in SPL, they want common interfaces to
follow][8]. Now why should PSR be in SPL, when YAF isn't? Where do we draw the line?

In that sense, please keep PHP free from framework interests.
Don't put the Classloader into SPL.
Thank you.

P.S. Some additional thoughts can be found in [ircmaxell's blog][9]

[1]: https://wiki.php.net/rfc/splclassloader
[2]: https://groups.google.com/group/php-standards
[3]: http://docs.php.net/manual/en/userlandnaming.php
[4]: http://martinfowler.com/bliki/EnablingAttitude.html
[5]: http://martinfowler.com/bliki/DirectingAttitude.html
[6]: https://secure.wikimedia.org/wikipedia/en/wiki/Coding_conventions
[7]: http://docs.php.net/manual/en/book.yaf.php
[8]: https://groups.google.com/group/php-standards/browse_thread/thread/44158f606ad39b1a
[9]: http://blog.ircmaxell.com/2011/11/on-psr-0-being-included-in-phps-core.html