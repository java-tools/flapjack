### Why did I call the project **"[flapjack](http://dictionary.reference.com/browse/flapjack)"**? ###
When I thought about parsing a flat file I imagined a stack of pancakes on a plate.

### Why did I make the parsing and mapping to the model separate? ###
Well, that's the way I think it should be.  Also, it allows multiple developers to use the same record layouts, but use totally different domain models. Why should someone have to duplicate the record definitions?!  This leads to mistakes re-implementing the record layouts and it's also duplication.  Plus from my experience it's sometimes hard to get others to agree on the same domain model design.

### How to use Flapjack? ###
Checkout the [examples](Examples.md) on how to use flapjack.

### How to access Flapjack as a Maven dependency? ###
Checkout how to setup your pom to access the flapjack [repository](HowToUseMavenRepo.md)

### I see there is a new release of flapjack. What features or bug fixes are in the new release? ###
Checkout the **[release notes](ReleaseNotes.md)**.

### I have encounted a bug or I see a missing feature. What should I do? ###
Create an issue [here](http://code.google.com/p/flapjack/issues/list).

### How can I be notified of updates or new releases? ###
Checkout the project feeds [here](http://code.google.com/p/flapjack/feeds).
Follow us on [twitter](http://twitter.com/flapjackparser)

### How do I get access to the source code repository? ###
The source code is actually hosted on Git Hub [here](http://github.com/born2snipe/flapjack/tree/master).

### I have a question, but it is not answered here? ###
Post a question on the [Google Group](http://groups.google.com/group/flapjackparser).