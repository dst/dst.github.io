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

Then there was the keynote which was very interesting. Juergen Hoeller talked about
"12 Years of Spring: An Open Source Journey".
It was a very interesting story about the history of Spring which began from Rod Johnson
writing a book "Expert One-on-One J2EE Design and Development" in October 2002.
![Book Expert One-on-One J2EE Design and Development](/assets/book-j2ee-design-and-dev.jpg)

# Wikipedia contribution
While I was writing this blog post, I found a mistake in the article about Spring Framework
on [Wikipedia][spring-wiki]. It said that
"The first version was written by Rod Johnson, who released the framework with the publication
of his book "Expert One-on-One J2EE Development without EJB" in October 2002".
![Book Expert One-on-One J2EE Development without EJB](/assets/book-j2ee-dev-without-ejb.jpg)
 
According to Juergen Hoeller's [slides][juergen-slides] it is not true.
"Expert One-on-One J2EE Development without EJB" was a follow-up book, which was published
in 2004 and was  based on Spring Framework 1.0.
"Expert One-on-One J2EE Design and Development" was written first. I decided to change this fragment
to the following:
"The first version was written by Rod Johnson, who released the framework with the publication
of his book Expert One-on-One J2EE Design and Development in October 2002".
Here you can find a record of my [activity][wiki-change]. I think that it is worth to mention
that it was my first contribution to Wikipedia.

# Interesting story
There was also an interesting story about the cover of "Professional Java Development with the Spring Framework"
book. The authors asked a random photographer during some conference to take them a picture for a book cover.
Here is the result:

![Book Professional Java Development with the Spring Framework](/assets/book-java-dev-with-sf.jpg)

# Best talks
At the end of the conference the organisers announced three best talks:

1. Building Microservices with Spring Cloud and Netflix OSS
2. Building “Bootiful” Applications with Spring Boot 
3. Modern Java Component Design with Spring 4.2

I'm not sure how they chose these talks, but probably they counted somehow the number of attendees on each talk.
I didn't like the talk which won. Maybe because I had heard about Spring Cloud and Netflix OSS before and I use
them at work so I expected to see something more. Maybe I just made a wrong choice. If I would go to a talk about
the Java basics, I would be probably bored as well. Nevertheless, there was one interesting thing, which I has
learnt during this talk. Namely, a colon can separate a key and a value in a properties file. In fact, several
formats are possible, including:

* key=value
* key = value
* key:value
* key value.

I haven't seen the talk number 3 because I decided to see
"Inside an Spring Event Sourced CQRS application – or why Microservices can actually work" and it was a perfect
choice, I wasn't disappointed at all. I haven't also attended the talk number 2 because I have already seen it
in Warsaw during WJUG meeting, which was almost a year ago.

If I could award the best talks, choosing among the ones which I saw, I would choose:

* JHipster, the leading application generator for Spring Boot + AngularJS
* Inside an Spring Event Sourced CQRS application – or why Microservices can actually work

I was really impressed when listening to these talks.

# Funny moments
I liked the "Spring Batch for Large Enterprises Operations" talk. It was interesting from a technical point of view.
But I also really enjoyed how the speaker pronounced a word "feature". He called it "fi-ejtur" (Polish) :)

I liked also the talk "Micro-Services ¿Grails or Spring Boot?" given by Fátima. She was probably the only
woman among the speakers. She made an interesting comparison between Grails and Spring Boot. But I also
enjoyed it when Fátima wanted to announce a section in her talk about Spock. Unfortunately instead of
"My favorite section" she said "my favorite sex..." long break "...tion" :)

One remark to the Fátima's presentation. She gave an example of injecting property in Groovy:

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

I didn't found any agenda in my pack. There were only described talks given by Pivotal. I wish I also had
a map with the rooms. The auditorium was the main room, but it was not easy to find other rooms
at the first time. One needed to go outside the building to find them. Inside the auditorium there were perfect
conditions to listen talks. Plenty of space, good air-conditioning and sound system. On the other hand, the
other two rooms were too small and probably without air-conditioning (or at least I couldn't feel it).
It was very hard to breathe when many people arrived at such a small room. Room no. 3 was the worst. It
was definitely too small. Moreover, there was low visibility due to the columns inside the room.

I don't drink coffee often, maybe 1-2 times per month. But I like drinking coffee during conferences
due to a long, big mental effort. You know, you need to be focused all the time to gather as much knowledge
as possible from the conference. Unfortunately coffee was available only during 2 coffee breaks per day and
it was served by waiters. As an effect, there were very long queues.

I liked bags with food. It was really tasty.

At the end of the conference a few gifts were given to drawn people. My colleague Rafał has won
one of five Intellij licences. Congratulations to him.

# Summary
And summary as a [video][video].

[springio2015]:     http://www.springio.net
[spring-wiki]:      http://en.wikipedia.org/wiki/Spring_Framework
[juergen-slides]:   http://www.springio.net/wp-content/uploads/2014/11/spring-open-source-journey-juergen-hoeller.pdf
[wiki-change]:      https://en.wikipedia.org/w/index.php?title=Spring_Framework&type=revision&diff=664488102&oldid=663551612
[video]:            https://www.youtube.com/watch?v=XWKgi_XqkSg