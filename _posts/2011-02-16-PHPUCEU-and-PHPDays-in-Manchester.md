---
layout: post
title: PHPUCEU and PHPDays in Manchester
---
I had the pleasure to attend the first [PHP Unconference Europe][1] and the [PHP Days in Manchester][2]. I knew there would be a couple of people I wanted to meet in person. Also, I've never been to Manchester before. So I decided I had to go. Happy I did, because I had a great time.

###Warm-Up

Before the actual conference, about 25 people met in a pub for the warm-up party. I was introduced to what the British consider beer (I'd rather call it Mock Beer or Beer Doubles) and quickly got into smalltalk with the other conference attendees. Since the Conf would start at 9am the next day, I left at about 11pm to get some sleep.

###Day 1

The PHP Unconference in Manchester is the first spin-off of Hamburg's PHP Unconference. So it was no suprise that a good quarter to half of the 100 attendees were german. Judith Andresen kicked off the conference with a short speech before she explained how the Session voting works: you got four votes per day, which you can use to vote for any available Sessions. The Sessions with the most votes wins. There is two Sessions in parallel.

The first talk I attended was [Lorna "lornajane" Mitchell][17]'s **"Speaking Tips for Developers"**, which I liked very much. Lorna gave a highly enthusiastic talk with lots of useful advice for anyone who ever wants (or has) to speak in front of an audience.

I heard **"Dealing with Errors"** by James (last name?) then. I didnt agree on all the suggestions on how Error Handling should be used in PHP, but all in all, the Session was a good round-up of the various error handling mechanisms.

After that I saw [Volker Dusch][18]'s talk [**"Clean Code - Stop wasting my time"**][19]. The talk mainly focused on superfluous commenting in source code, doc blocks and commit messages. Again, quite interesting and also quite entertaining due to Volker's ranting presentation style.

&gt; It's not so much about the talks than about the coffee breaks - Judith Andresen

Along the lines of that quote I skipped the next session to meet Mark Baker of PHPExcel then. I only knew Mark from StackOverflow so far and was happy to finally meet him in person. Was a pleasure.

The last session of the day was Arne Blankert's talk **"PHPDox &ndash; an alternative to PHPDocumentor"**. PHPDox aims to finally supersede the aged PHPDocumentor tool. At the time of the conference, phpdox was nearing completion and looked quite promising already. It's available on github.

After that it was socializing again. The conference venue, Pitcher and Piano, is a bar chain so we didnt have to relocate for the evening. The second floor was reserved for us. I spent quality time with good talking and a couple of free drinks sponsored by the conf organisers before heading back to the hotel at about 11pm again.

###Day 2

When we arrived on the second day, they were still cleaning the room. So there was some delay before the voting and the sessions could start.

I attended [**"Building a successful development team"**][7] held by Stefan Priebsch and Judith Andresen. This talk was an open discussion about the topic. Although there was some good points mentioned what makes a good team and what is hampering it, I felt the discussion was too superficial. But interesting nonetheless.

After that I saw the completely PHP-unrelated talk **"HTML5 and Friends"** by Patrick Lauke, Web Evangelist at Opera. This was a very thorough, professional and lengthy talk and Patrick had to continue it long into the lunch break to finish it. It couldn't lessen my bias towards HTML5 though, as I don't believe in "bling".

&gt; HTML5 is HTML4 with added bling - Patrick H. Lauke

Then I heard **"Automated Release Procedures for the Web / DB Versioning and Deployment"**. This was an open discussion again and I didn't get too much out of it for myself. I like to leave a Session with at least one "I have to try that at home" thought.

The final session was **"Setting up Jenkins CI for PHP Projects"** held by Sebastian Bergmann and Volker Dusch (again). They introduced their [PHP Template for Jenkins][16] and ran through setting up the Continuous Integration Server for usage with PHP QA Tools, like phpunit, pdepend, phpmd and so on. Very useful talk.

After that the organisers held a short closing speech and were (rightfully) applauded by the remaining attendees.

###Venue

Originally, another venue was considered. But because there wasn't enough tickets sold when the venue was finalised, the choice was made for the Pitcher and Piano. So, next year, buy your tickets early and give the organizers some more financial room for planning.

Like already mentioned, Pitcher and Piano is a bar chain. Doing a conference in a bar works, as long as there is no other visitors. Unfortunately, the bar would allow other visitors into the bar though. Naturally, there noise level rose the later the day. This was somewhat annoying when attending talks upstairs, because music and talking from the main bar would disturb the speakers. Apart from that, the venue worked suprisingly well for me.

###Catering

Let's admit it: the PHPUnconference in Hamburg spoiled me. You get breakfast, lunch, cake (not a lie) and unlimited coffee, tea and softdrinks for free. All very tasty and easily on par with the catering at a commerical conference, like IPC. If there was no talks at all, I'd still attend for the food alone.

I had expected a similar pampering in Manchester. I didn't book breakfast at my hotel and I didn't bring any drinks. Both mistakes, because there wasn't any breakfast and no drinks during the day, except for coffee, tea and lemonade. All of these were made from tap water, which I wasn't the only one who felt tasted odd, [quoting][6]:

&gt; Wondering if they use canal water for the tea and coffee #phpuceu - antz29

Because of that I bought all my drinks at the bar instead (until we got our vouchers for the party).

The lunch on both days was solid. So was the dinner on the first day. I remember there was lasagna, chili, curry and assorted salads and side dishes. Vegetarians had their options, too. Some attendees told me they felt the food tasted rather bland. I felt it was okay (and there was salt and pepper available anyways). So, nothing to complain about here.

###PHP Days

As part of their sponsoring, [thePHPcc][8] aka [Sebastian Bergmann][9], [Stefan Priesch][10] and [Arne Blankerts][11] offered a two day training after the two days conference. All training fees would go directly to the Unconf, so they actually held the training for free. Because I had already attended both [PHPSummit's][13] held by thePHPcc last year and found them very valuable, I was eager to participate in this training.

The PHP Days were held at the Manchester Conference Center with just eight attendees (five of them german). All of us already knew a fair share about PHP, so discussions were at an enjoyable intermediate to expert level. It's also quite fun to see thePHPcc lecture together, as one of them will usually always play [Devil's Advocate][14]. Plus, there will a good portion of [geek humor][15] involved.

Since we could decide where we wanted this training to be headed, we decided to build a [joind.in clone][12] (we didn't finish it though). So we discussed the problem domain while thePHPcc would write the code and the UnitTests for us. As the code evolved and domain knowledge got better, we would apply needed refactorings.

Inbetween there was lunch, tea, coffee and cookies.

On the second day, thePHPcc showed us how to create a minimal MVC framework around our new Domain classes. We also talked about how to use the Dependency Injection Principle to avoid tight coupling in our classes. And we talked about how to properly divide functionality into framework, application and domain classes to get the responsibilities right. This was very insightful, even for seasoned developers. The last two hours of the training, we talked about how to deploy our application.

### Conclusion

Despite a few shortcomings, I really enjoyed PHP Unconference Manchester. It was a great event with great people and good talks. I am looking forward to attend next year.

The PHP Days training was fantastic and I can happily recommend it to any seasoned developer. Looking forward to attend this next year again as well (if it's offered).

In short: thanks to everyone who made these four days possible and awesome.


[1]: http://www.phpuceu.org/phpuceu-2011 "Official Website of the PHPUnconference EU"
[2]: http://www.phpuceu.org/2010/05/01/php-days-in-manchester "PHP Days Manchester"
[3]: http://www.phpuceu.org/contact/organizers "Organisers of of the PHPUnconference EU"
[4]: http://joind.in/event/phpuceu "PHPUnconference EU at Joind.in"
[5]: https://search.twitter.com/search?q=%23phpuceu "Hashtag #phpuceu on Twitter"
[6]: https://twitter.com/antz29/status/38943134884970496
[7]: http://www.slideshare.net/janosch007/20110218-janosch007-teambulildingkey "Session Slides"
[8]: http://thephp.cc "Website of thePHPcc"
[9]: http://sebastian-bergmann.de "Website of Sebastian Bergmann"
[10]: http://priebsch.de/about "Website of Stefan Priebsch"
[11]: https://twitter.com/arneblankerts "Arne Blankerts on Twitter"
[12]: https://github.com/thePHPcc/SplitOut "Joind.in clone on GitHub"
[13]: http://php-summit.de/ "Website of the PHPSummit series of trainings (german)"
[14]: https://secure.wikimedia.org/wikipedia/en/wiki/Devil%27s_advocate "Wikipedia on Devil's Advocate"
[15]: https://secure.wikimedia.org/wikipedia/en/wiki/Geek_humor "Wikipedia on Geek Humor"
[16]: http://jenkins-php.org/
[17]: http://www.lornajane.net/pages/about.html
[18]: http://joind.in/talk/view/2723 "Volker Dusch as joind.in"
[19]: http://www.slideshare.net/Edorian/php-unconference-europa-clean-code-stop-wasting-my-time "Session Slides"