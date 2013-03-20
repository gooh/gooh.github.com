---

layout: post
title: Always Return Something?
tags: [oop, php]

---

There was a [blog post recently by Brandon Savage][SAV1] suggesting that

> You should always return something when writing a function or a method.

I don't think this is particular good advice and will outline my reasons below.

## Command Query Separation (CQS)

Always returning values, is a direct contradiction to [Bertrand Meyer's Command Query Separation principle][MEY1],
which states that a method should either be

- a command, changing observable state but not returning anything
- or a query, returning something but not changing observable state.

But not both. Following CQS adds an extremely valueable characteristic to the application: you can
safely query your application at any given point in time without fear of changing the application state
in any way. This lowers the complexity of your API immensly and [protects from WTF moments][WTF1].

Just as with all principles, CQS is not a dogma though. Treat it as a *pretty good guideline*. If you find
yourself in a situation where not adhering to the principle adds a pragmatic benefit, then you may of course
not follow it. However, none of the arguments given in Brandon's post are particularly pragmatic in my opinion.

## Sanity Check

Brandon suggests that "when you’re writing code, you should always do a sanity check to verify that
the functions you’ve executed have been successful." I have a hard time imagining what my code would have
to look like then. It sounds awfully like

{:.prettyprint .linenums .lang-php}
    if (doSomething()) {
        if (doSomethingElse()) {
            // more nesting
        } else {
            // log and die
        }
    } else {
        // log and die
    }

Why not just raise an Exception when something goes wrong? It's a tried and tested mechanism. Just returning
`FALSE` will only tell me *that* something went wrong. An exception will tell me *why* an error occurred. So
instead of cluttering the caller with conditionals (cf. Martin, Clean Code, pg. 103), I will write

{:.prettyprint .linenums .lang-php}
    function doSomething()
    {
        // assert preconditions or throw Exception
        // do something
        // assert postconditions or throw Exception
    }

This way my consuming code can simply `try` to `doSomething()` and `catch` any exceptional situations. It will
also keep the messages about stuff I can anticipate to go wrong close to where it happens. So I don't
have to repeat the error messages each time I enter the `else` block.

## Returning null

There is one thing that struck me throughout the post. It constantly says `return null`, when it should mean
`return void`. Granted, `void` is only a pseudotype in PHP. PHP *will* return `null` whenever you don't
include an explicit return statement. And there is value in Brandon's suggestion not to return `null`.
It just should not lead you to the conclusion that you should *always return something*. In order to cut
down on `if`'ing on return values, your **Queries** should return one type only though. That is, if you have
a function that should produce an array, have it return an empty array (given nothing went wrong). If you
cannot reasonably do that in a function or method, consider this advice from Michael Feathers:

> If you are tempted to return `null` from a method, consider throwing an Exception or returning a
> Special Case object instead. *Source: Martin, Clean Code, pg 109*

Following this advice yields the same benefit as not sanity checking your code. You cut down on cluttering
the caller with conditionals. It will make your code more readable, less complex and thus, more robust.

## Testing Setters

Brandon further suggests that testing a non-returning setter will be hard to test. And that having to retrieve
the value to an additional getter is just adding dependencies. I find that argument weird. What dependency does
it add? If you have the Getter in the class anyway, there is no additional dependency. You just use what is
there.

If you add the Getter just for the sake of being able to query the object, you are doing it wrong. [PHPUnit
supports reading protected and private attributes through `assertAttributeEquals()`][BER1]. But even if
it wouldn't, there is no real problem. And that's not because you could use Reflection to set the property
accessible. No, it's because the object that has the Setter will have a method through which you can verify
that the Setter worked implicitly:

{:.prettyprint .linenums .lang-php}
    class Link
    {
        public function setUrl($url)
        {
            $this->url = $url;
        }
        public function setLinkText($linkText)
        {
            $this->url = $url;
        }
        public function getHtml()
        {
            return '<a href="{$this->url}">{$this->linkText}</a>'
        }
    }

Let's ignore that ctor injection would probably be a better approach here. The point is, the setters in
the example class above do not need to return anything. You can easily test them through your `getHtml()`
method. In fact, doing so is the only *important* test in the entire TestCase.

## Fluent Interfaces

The next argument in Brandon's article is that non-returning methods will break [Fluent Interfaces][FOW2].
That's true and it's one of the scenarios in which the benefit trumps CQS. The purpose of a Fluent Interface
is to build an internal Domain Specific Language (DSL) though. The point of a DSL is to provide a terse and
semantically meaningful API with little syntactic noise. A Fluent Interface will sit on top of a
Semantic Model that is hopefully build on sound design principles (like CQS). Think of a Fluent Interface
as a semantic Facade for your Domain Model.

Chaining Setters, like in Brandon's example, is not a Fluent Interface though. It's merely chaining and the
example he gives is what Uncle Bob would identify as a *sloppy Train Wreck* (cf Martin, Clean Code, pg 98).
Fowler also warns about chaining methods like this due to the negative readability impact it has on
the code. He also warns mixing chained APIs with CQS APIs. The inconsistency could confuse developers because
they will not know when and when not they can chain (cf. Fowler, Domain Specific Languages, pg. 374).
This is especially in true in PHP where you cannot deduce the return type from the API signature alone.

Also, just because Method Chaining is a key technique in creating DSLs, drawing the conclusion that
you should always return `$this` is invalid. You are not always creating a DSL. And keep in mind that
each method supporting Method Chaining is potentially more error prone. A typo here and a forgotten
return there happens to even the most seasoned developer. Since you have to add the returns manually,
your chances to make a mistake eventually are much higher than without chaining. A line not written is
a line without errors.

## Conclusion

When writing functions and methods, stick to tried and tested principles. CQS is such a principle. My
post has shown how to approach the issues Brandon raised without having to abandon it.

[SAV1]: http://www.brandonsavage.net/always-return-something/
[MEY1]: https://en.wikipedia.org/wiki/Command%E2%80%93query_separation
[FOW1]: http://martinfowler.com/bliki/CommandQuerySeparation.html
[BER1]: http://sebastian-bergmann.de/archives/881-Testing-Your-Privates.html
[FOW2]: http://martinfowler.com/bliki/FluentInterface.html
[WTF1]: http://www.osnews.com/story/19266/WTFs_m