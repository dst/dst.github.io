---
layout: post
title:  "Why you shouldn't use a dollar sign in your passwords"
categories: misc
tags: bash open-source micro-infra-spring
---
Recently I have had a very interesting problem at work. I started my new microservice which uses encrypted,
git-based properties and I noticed the following exception in logs:

{% highlight text %}
2015-04-28 01:06:09.290+0200 | ERROR |  | main | o.s.b.SpringApplication | Application startup failed
java.lang.IllegalArgumentException: Unable to initialize due to invalid secret key
	at org.springframework.security.crypto.encrypt.CipherUtils.initCipher(CipherUtils.java:110) ~[spring-security-crypto-3.2.6.RELEASE.jar:3.2.6.RELEASE]
	at org.springframework.security.crypto.encrypt.AesBytesEncryptor.decrypt(AesBytesEncryptor.java:74) ~[spring-security-crypto-3.2.6.RELEASE.jar:3.2.6.RELEASE]
	at org.springframework.security.crypto.encrypt.HexEncodingTextEncryptor.decrypt(HexEncodingTextEncryptor.java:40) ~[spring-security-crypto-3.2.6.RELEASE.jar:3.2.6.RELEASE]
	at com.ofg.infrastructure.property.FileSystemLocator.decrypt(FileSystemLocator.java:95) ~[micro-infra-spring-config-0.8.17.jar:na]
	at com.ofg.infrastructure.property.FileSystemLocator.decryptIfEncrypted(FileSystemLocator.java:87) ~[micro-infra-spring-config-0.8.17.jar:na]
	at com.ofg.infrastructure.property.FileSystemLocator.decrypt(FileSystemLocator.java:80) ~[micro-infra-spring-config-0.8.17.jar:na]
	at com.ofg.infrastructure.property.FileSystemLocator.toPropertySource(FileSystemLocator.java:67) ~[micro-infra-spring-config-0.8.17.jar:na]
	at com.ofg.infrastructure.property.FileSystemLocator.locate(FileSystemLocator.java:41) ~[micro-infra-spring-config-0.8.17.jar:na]
	at org.springframework.cloud.bootstrap.config.PropertySourceBootstrapConfiguration.initialize(PropertySourceBootstrapConfiguration.java:81) ~[spring-cloud-config-client-1.0.0.RELEASE.jar:1.0.0.RELEASE]
	at org.springframework.boot.SpringApplication.applyInitializers(SpringApplication.java:567) ~[spring-boot-1.2.2.RELEASE.jar:1.2.2.RELEASE]
	at org.springframework.boot.SpringApplication.run(SpringApplication.java:303) ~[spring-boot-1.2.2.RELEASE.jar:1.2.2.RELEASE]
	at org.springframework.boot.SpringApplication$run.call(Unknown Source) [spring-boot-1.2.2.RELEASE.jar:1.2.2.RELEASE]
	at org.codehaus.groovy.runtime.callsite.CallSiteArray.defaultCall(CallSiteArray.java:45) [groovy-all-2.4.1.jar:2.4.1]
	at org.codehaus.groovy.runtime.callsite.AbstractCallSite.call(AbstractCallSite.java:110) [groovy-all-2.4.1.jar:2.4.1]
	at org.codehaus.groovy.runtime.callsite.AbstractCallSite.call(AbstractCallSite.java:122) [groovy-all-2.4.1.jar:2.4.1]
	at com.ofg.releasenotes.Application.main(Application.groovy:21) [main/:na]
{% endhighlight %}

As you can see above, I use a module config from [micro-infra-spring][micro-infra-spring-github] library.
I am a coauthor of this module and I can honestly tell you that git-based properties are great.
You can find more details about this mechanism on [wiki][micro-infra-spring-config-wiki].

But let's come back to our exception. When I entered a debugger, I noticed that my password was
encoded as "abcdhimBHefgh}xyz" instead of "abcd$-efgh$2}xyz" (passwords are simplified for the
purpose of this article).

I thought: "What the hell?" The prefix and suffix of password were ok, but the medium part was incorrect.

I used a Ruby script, which is a part of micro-infra-spring, to encrypt the password:

{% highlight bash %}
$ ruby aes.rb -e "abcd$-efgh$2}xyz" "SUPER secret and hard master password"
"{cipher}212ea4f1c5c58894884f51697f078c98ab37d4555f3b24c234c1b3b319d281c617aebb7d4b09f9f036255da99e302c9e"
{% endhighlight %}

and then to decrypt it:

{% highlight bash %} 
$ ruby aes.rb -d "212ea4f1c5c58894884f51697f078c98ab37d4555f3b24c234c1b3b319d281c617aebb7d4b09f9f036255da99e302c9e"  "SUPER secret and hard master password"
abcdhimBHefgh}xyz
{% endhighlight %}

Btw. You should remove these commands from your Bash history, if you use real passwords.

The password was the same as in a debugger. At this moment I knew that there was something wrong with
the script aes.rb or the way it was called. 

If you look very closely at the difference between these two passwords, you can find two things:

* $- was changed into himBH
* $2 was changed into an empty string

At this moment you can recall that you can put variables in Bash string (like in Groovy language):

{% highlight bash %}
$ name="Darek"; echo "Hello $name"
Hello Darek
{% endhighlight %}

Do you get it? You should solve at least one puzzle now. There is no $2 variable, so it is translated
into an empty string.

Ok, if you have some experience with Bash, you should probably know variables like:

* $1, $2, $3 - positional parameters
* $# - number of parameters
* $@ - array representation of parameters
* $0 - name of the shell or shell script

But have you ever heard of $- variable? Let's check: 
{% highlight bash %}
$ echo $-
himBH
{% endhighlight %}

If you are smarter than me, you can try to google "himBH", otherwise when searching for "$-" you
can be out of luck. Fortunately, there is a [SymbolHound][symbol-hound] search engine that
can do it pretty well.

$- is a variable which keeps shell flags. It was tricky, wasn't it?

To fix the issue, you can escape all dollars:

{% highlight bash %} 
$ ruby aes.rb -e "abcd\$-efgh\$2}xyz" "SUPER secret and hard master password"
"{cipher}212ea4f1c5c58894884f51697f078c9894db95ba3085da15a018d267ffae3d54d91f3ae9f794317705c260d9bd891149"

$ ruby aes.rb -d 212ea4f1c5c58894884f51697f078c9894db95ba3085da15a018d267ffae3d54d91f3ae9f794317705c260d9bd891149  "SUPER secret and hard master password"
abcd$-efgh$2}xyz
{% endhighlight %}

or use a single quotation mark:
{% highlight bash %} 
$ ruby aes.rb -e 'abcd$-efgh$2}xyz' "SUPER secret and hard master password"
"{cipher}212ea4f1c5c58894884f51697f078c9894db95ba3085da15a018d267ffae3d54d91f3ae9f794317705c260d9bd891149"

$ ruby aes.rb -d 212ea4f1c5c58894884f51697f078c9894db95ba3085da15a018d267ffae3d54d91f3ae9f794317705c260d9bd891149  "SUPER secret and hard master password"
abcd$-efgh$2}xyz
{% endhighlight %}
 
Double quotes allow expansion of variables within the quotes, and single quotes don’t.

I decided to use a single quotation mark and changed examples in [documentation][micro-infra-spring-config-wiki]

The conclusion is simple: "Don't use a dollar sign in your application passwords" or be very careful
and use a single quotation mark when encrypting it.

[micro-infra-spring-github]:   https://github.com/4finance/micro-infra-spring
[micro-infra-spring-config-wiki]: https://github.com/4finance/micro-infra-spring/wiki/Centralized-configuration-management
[symbol-hound]: http://symbolhound.com