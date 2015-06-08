---
layout: post
title:  "Spring I/O 2015 Barcelona review"
categories: conference
tags: conference review spring barcelona wikipedia
---

I attended Spring I/O conference in Barcelona on 29th and 30th April.

It was the first time when this conference took place in Barcelona and was fully in English.
The previous editions were in Madrid and talks were given in English and Spanish.
There were about 350 attendees from 20 countries.

# Let's begin
The conference started with a nice, comic, dancing performance. It was really funny.

Then there was a keynote which was very interesting. Juergen Hoeller talked about
"12 Years of Spring: An Open Source Journey".
It was a very interesting story about Spring history which began from writing a book 
"Expert One-on-One J2EE Design and Development" by Rod Johnson in October 2002.
![Book Expert One-on-One J2EE Design and Development](/assets/book-j2ee-design-and-dev.jpg)

# Wikipedia contribution
While I was writing this blog post, I found a mistake in an article about Spring Framework
on [Wikipedia][spring-wiki]. There was written that
"The first version was written by Rod Johnson, who released the framework with the publication
of his book "Expert One-on-One J2EE Development without EJB" in October 2002".
![Book Expert One-on-One J2EE Development without EJB](/assets/book-j2ee-dev-without-ejb.jpg)
 
According to Juergen Hoeller's [slides][juergen-slides] it is not true.
"Expert One-on-One J2EE Development without EJB" was the follow-up book, which was published
in 2004 and was  based on Spring Framework 1.0.
"Expert One-on-One J2EE Design and Development" was written first. I decided to change this fragment
to the following:
"The first version was written by Rod Johnson, who released the framework with the publication
of his book Expert One-on-One J2EE Design and Development in October 2002".
Here you can find a record of my [activity][wiki-change]. It was my first contribution to Wikipedia.

# Interesting story
There was also an interesting story about a cover of "Professional Java Development with the Spring Framework"
book. Authors asked a random photograph during some conference to take them a picture for a book cover.
Here is the result:

![Book Professional Java Development with the Spring Framework](/assets/book-java-dev-with-sf.jpg)

# Best talks
At the end of conference the organisers announced three best talks:

1. Building Microservices with Spring Cloud and Netflix OSS
2. Building “Bootiful” Applications with Spring Boot 
3. Modern Java Component Design with Spring 4.2

I'm not sure how they choose these talks, but probably they counted somehow the number of attendees on each talk.
I didn't like the talk which won. Maybe because I had heard about Spring Cloud and Netflix OSS before and I use
them at work so I expected to see something more. I haven't seen 3. because I decided to see 
"Inside an Spring Event Sourced CQRS application – or why Microservices can actually work" and it was a perfect
choice, I wasn't disappointed. I haven't also attended 2. because I have seen it already in Warsaw during WJUG meeting
almost 1 year ago.

If I could award the best talks, which I saw, I would choose:

* JHipster, the leading application generator for Spring Boot + AngularJS
* Inside an Spring Event Sourced CQRS application – or why Microservices can actually work

I was really impressed when listening these talks.

# Funny moments
I liked "Spring Batch for Large Enterprises Operations" talk. It was interesting from a technical point of view.
But I also really enjoyed how a speaker pronounced a world "feature". He called it "fi-ejtur" (Polish) :)

I liked also a talk "Micro-Services ¿Grails or Spring Boot?" given by Fátima. She was probably the only
woman within the speakers. She made interesting comparison between Grails and Spring Boot. But I also
enjoyed when Fátima wanted to announce a section in her talk about Spock. Unfortunately instead of
"My favorite section" she said "my favorite sex..." long break "...tion" :)

One remark to Fátima presentation. She gave an example of injecting property in Groovy:

{% highlight Groovy %} 
@Value("\${propertyKey}")
{% endhighlight %}

I recommend to use the following form:

{% highlight Groovy %} 
@Value('${propertyKey}')
{% endhighlight %}

It is nicer, isn't it?

# Organisation
Now it is time for less technical stuff.

I didn't found an agenda in my pack. There were only described talks given by Pivotal. I wish I had
also a map with rooms. The auditorium was a main room, but it was not easy to find other rooms
at first time. One needed to go outside the building to find them. Inside auditorium were perfect
conditions to watch talks. Plenty of space, good air-condition and sound system. On the other hand,
other 2 rooms were too small and probably without air-condition (or at least I couldn't feel it).
It was very hard to brief when many people arrived to such small room. Room 3 was the worst. It
was definitely too small. There was also a low visibility due to columns inside the room.

I don't drink coffee often, maybe 1-2 times per month. But I like drinking coffee during conferences.
Unfortunately coffee was available only during 2 coffee breaks per day and it was served by waiters.
As an effect there were long queues.

I liked begs with food. It was tasty.

At the end of conference a few gifts were given to drown people. My colleague Rafał has won
one of five Intellij licences. Congratulations for him.

# Summary
And summary as a [video][video].

[springio2015]:     http://www.springio.net
[spring-wiki]:      http://en.wikipedia.org/wiki/Spring_Framework
[juergen-slides]:   http://www.springio.net/wp-content/uploads/2014/11/spring-open-source-journey-juergen-hoeller.pdf
[wiki-change]:      https://en.wikipedia.org/w/index.php?title=Spring_Framework&type=revision&diff=664488102&oldid=663551612
[video]:            https://www.youtube.com/watch?v=XWKgi_XqkSg