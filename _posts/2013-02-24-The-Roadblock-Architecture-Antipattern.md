---

layout: post
title: Roadblock Architecture
tags: [anti-patterns]

---

The following describes something that I have experienced a number of times, either on the job or in software,
(especially in frameworks) and which I think is worth coining an AntiPattern for.

- *AntiPattern Name:* Roadblock Architecture
- *Also Known As:* Obstacle Odyssey
- *Most Frequent Scale:* Application
- *Refactored Solution Name:* Refactoring of Responsibilities
- *Refactored Solution Type:* Software
- *Root Causes:* Miscommunication, Overengineering
- *Unbalanced Forces:* Management of Functionality, Performance, Complexity
- *Anecdotal Evidence:* "So to echo something, I just need to change these ten files?"

## Background

[A roadblock is a temporary installation set up to control or block traffic along a road.][WIKI-RB]
When you encounter a roadblock, you need to find another way to continue to your destination.
This takes time, especially if you do not know the area you are driving in and don't have a 
navigation system to lead you around that obstacle.

Roadblocks in code can be helpful if they detour the developer in a way that is benefiting the
overall system architecture, e.g. instead of taking a direct route, it forces a developer to
adhere to a certain way of doing things. In the Antipattern, these guiding characteristics are amiss.

## General Form

In a Roadblock Architecture, each change to the application is ridiculously difficult or 
unintuitive to achieve. The architecture forces you to take detour after detour to reach 
a certain goal. In poorly architected systems, this is often accompanied by leading you
through parts and layers of the application that should not be part of the route. If you 
have to run the gauntlet, you are likely facing a Roadblock Architecture.

Roadblock Architecture is different from a [Big Ball of Mud][WIKI-BBOM] in that it has a
perceivable architecture and often even sane software metrics, e.g. little code duplication,
high Code Coverage, no globals, etc. A Roadblock Architecture might even look sane and reasonable
when it is explained to you by the person who devised. It is only that when you start to work
with it that you realize it is suffering from unnecessary complexity.

## Symptoms And Consequences

Changing or adding features is more expensive in terms of time and effort than it needs to be.
To achieve a certain functionality you have to touch or create a multitude of files. Developers
new to a project will not come to speed because the flow of messages through the system is non-obvious.
This can be especially frustrating for experienced developers who are aware that the architecture
is not supporting but hindering progress.

## Typical Causes

Typical causes are [Over-Engineering][WIKI-OE], bi-directional dependencies between software layers and
lack of documentation of how messages flow through the application or where things need to be configured.
This can also be a team smell when knowledge about the application is limited to certain people.
It can also occur when there is large experience gap between the lead architect(s) and the implementing
developers: the initial concept of the Roadblock might have made sense, but because it's intention was not
well understood by other developers caused it to become an obstacle instead of a helpful artifact.
If there is no such experience gap Roadblock Architecture can also be caused by [Lead Architect(s) living
in an Ivory Tower][IT].

## Known Exceptions

Roadblocks used sparingly or in a sane fashion. It's when there is too many roadblocks that it becomes a problem.

## Variations

[Pasta Code (in particular Lasagna or Ravioli)][PASTA], [Architecture by Implication][ABI], [Poltergeists][PG].
A Roadblock Architecture is likely to contain one or more of these problems.

## Refactored Solution

A solution to Roadblock Architecture is to remove superfluous Roadblocks obviously. That means refactoring
complexity to a level that the code gets simpler and comprehensible (cf. [KISS][WIKI-KISS] and [YAGNI][WIKI-YAGNI]). If there is any
bi-directional dependencies between software they need to be changed to [uni-directional, facing inwards][Martin-CA].
If there is isolated functionality, it should be checked whether it can be [moved onto the objects using them instead][WIKI-IE].

Since Roadblock Architecture is likely to contain one or more of the aforementioned variations, any refactorings
applying to them might apply to Roadblock Architecture, too.

Parts that cannot be reasonably refactored this way need to be documented and stored at a location easily available
to the developers. Pair Programming with new developers might also help to get them to speed. However, the latter
is curing symptoms only. It is not addressing the root cause.


[WIKI-RB]: https://en.wikipedia.org/wiki/Roadblock
[WIKI-OE]: https://en.wikipedia.org/wiki/Overengineering
[PASTA]: http://c2.com/cgi/wiki?PastaCode
[ABI]: http://sourcemaking.com/antipatterns/architecture-by-implication
[IT]: http://stevenimmons.org/2012/02/the-ivory-tower-anti-pattern/
[PG]: http://sourcemaking.com/antipatterns/poltergeists
[Martin-CA]: http://blog.8thlight.com/uncle-bob/2012/08/13/the-clean-architecture.html
[WIKI-IE]: https://en.wikipedia.org/wiki/GRASP_%28object-oriented_design%29#Information_Expert
[WIKI-KISS]: https://en.wikipedia.org/wiki/KISS_principle
[WIKI-YAGNI]: https://en.wikipedia.org/wiki/YAGNI
[WIKI-BBOM]: https://en.wikipedia.org/wiki/Big_ball_of_mud
[WIKI-PL]: https://en.wikipedia.org/wiki/Pattern_language