---
layout: post
title: Tech review - Java web frameworks (for CRUD apps)
---

## Java Enterprise

The first Java web framework was Java Enterprise (J2EE). This included a lot of stuff for distributed applications and didn't focus specifically on web applications. The web part was Java Servlets (the controller in MVC pattern) along with Java Server Pages (the view). 

Note that Java EE was and is only a specification of an API: there are multiple implementations available from different vendors. You've probably heard of Jboss, Tomcat, Jetty, etc. I guess Sun wanted to encourage competition while providing standardisation, so you could take your app and deploy to any EE-compatible server, but possibly because the standard was the lowest common denominator agreed by all the vendors it was pretty clunky. Everything had to be configured with XML files before coding could even begin, which programmers found painful.

Thus Java was only really used on the web by large organisations who could mandate their programmers had to use it to be compatible with their existing Java  EE applications. 

This allowed crappy but easy to use dynamic alternatives like Perl and PHP to flourish. 

## Grails

The game changer was the release of the Rails framework for Ruby. Ruby is a dynamic typed language like PHP, so it is far slower and less safe than Java. But unlike PHP it is well designed, pleasant to use and it encourages automated testing to overcome the lack of safety. Rails used Ruby's dynamism and a principal of 'convention over configuration' to make it very easy to create web applications, specifically CRUD applications. 

Rails single handedly made Ruby into a mainstream language and spawned a host of imitators in other languages (Django for Python, Yii for PHP). 

Java couldn't emulate Rails directly because it lacked dynamic typing, so several different things happened. The first was, I think, Grails, a clone of Rails using the Groovy language. Groovy runs on the JVM and looks pretty similar to Java but with more dynamism.  Grails is still popular today, although now it runs as a layer above the Spring framework.  I think it is a good choice.  although I'm not a fan of Groovy, you can write the majority of your app in Java. The only caveats are some parts will have to be Groovy, and since it runs on top of Spring it will never be faster and may be slower than Spring. 

## Spring

Which brings us to Spring. Not an easy thing to define! Spring began in the pre-Rails days as a dependency injection framework which was a reaction against the deficiencies of Java EE. As it grew it absorbed other popular frameworks, such as Hibernate ORM.  It's popularity caused Sun to adopt many of Spring's APIs into future versions of the Java Enterprise API. Conversely, nowadays Spring is able to interoperable with and incorporate many of the Enterprise APIs.  I think it bundles Jetty (?) inside itself too. So I'm not entirely clear on how to define the difference between them. Certainly you can do a Java Enterprise project and use different implementations other than those in Spring. If you do a Spring project then I think by definition your project is Java Enterprise because many parts of Spring implement Java Enterprise. And Spring is big. Many, many modules and sub modules make it difficult to generalise about. 

## Spring Roo

For a long time Spring was a competitor to Java Enterprise, not to Rails. The release of Rails did prompt Spring to attempt to drain their swamp of XML configuration files but Rails was still much more efficient at developing CRUD web applications.  A couple of Spring subprojects have attempted to change this. 

First was Spring Roo, which gets its dynamic magic from using AspectJ. This is good because you can stick to writing pure Java, while AspectJ quietly adds methods to your objects when you compile.  It does scaffolding and lots of auto generation. It's part of the larger Spring ecosystem which is reassuring. So it's a good alternative to Grails without using Groovy.  The only downside is that development and popular interest seem to have slowed to a crawl. 

## Spring Bootstrap

More recently they concentrated dev effort into a newer subproject, Spring Bootstrap. It provides a nice way of setting up a Spring project, making conventional 'opinionated' decisions for you.  However this is only necessary because Spring had grown into such a huge maze of different modules that no one knew which ones they should install to get started! It doesn't seem to do any scaffolding so CRUD apps are still slow to get started. I suppose  huge projects don't really care about scaffolding because the time saved is such a minimal part of their overall budgets and they don't need to iterate quickly anyway. But for me Bootstrap is still clunky compared to Rails. 

The current version of Grails is built on top of Spring Bootstrap. Spring Roo is still in (slow) development and the next version will use Bootstrap. So I don't really see Bootstrap as an alternative to these projects - it's a lower layer in the stack. If you want to work at the top level then you wouldn't use Bootstrap directly, despite it's name. 

## JHipster

Jhipster is another option for the layer-on-top-of-Spring-Bootstrap. It does even more configuration for you than Bootstrap so you can get started quickly, although it also gives you fewer options.  It does scaffolding, but not just view templates on the backend, it generates a JavaScript powered front end too, using Angular JS. 

## Play

If you want to stay outside the Java Enterprise / Spring ecosystem entirely then I don't blame you and there are many attempts at simpler Rails-like frameworks. 

The most popular is probably Play. While Grail's secret sauce was the Groovy language, Play chose another JVM language, Scala, to get the ease of configuration they required. This worked pretty well and Play become very popular. Scala made a good template DSL for the views and you could write the rest of your app in Java. 

Unfortunately the company that owned Scala was looking for a web framework too. They fell out with the developer of Scala's native web framework, Lift, and decided to buy out Play instead. They put a lot of money into marketing Play and its popularity increased, but they also took over the project and did exactly what they had done to Scala itself: over engineered it. When I tried to use it I found a beautiful system of thousands of parts working in harmony… Except some of the parts would regularly break, taking the system down, and not being a Scala experts I couldn't even tell which ones. 


## Ninja framework
 
Ninja seems like a version of Play that is actually used by in the real world and works. Still doest have scaffolding so is targeted at experienced developers. But it bundles an ORM, it has templates. I could happily use this for some projects.  But we are now firmly in the realm of community supported projects - you have to be happy go without the reassurance of large corporate backing. 

## Sparkjava
 
A very minimal framework. Doesn't have to download a load of jars like Grails and Play. Very easy to setup, very little to go wrong, but doesn't provide much. I think this would be good for someone who was already doing everything manually, e.g. PHP (without a framework). It doesn't have ORM. You can add ORM, but you can also just write SQL. It doesn't have HTML templates. You can easily add a template library, or you could just write HTML yourself. If you were doing a fully featured web app in Spark I feel you may as well use Ninja because you would end up adding all the stuff that Ninja bundles. 

There of course hundreds of other frameworks  I haven't mentioned, mostly small one man projects that that some people will love because they are so lightweight but personally make me feel like I'm having to reinvent the wheel. 

## Conclusion

Personally, what I want from an ideal Java web framework is: 

* Scaffolding to automatically generate CRUD apps
* sizeable community
* Enterprise level  backing
* reverse engineering of existing databases.

 I don't like Play.  Thus my recommendations are 
 
* Spring Roo (although stuck with old version because current version lacks DB reverse) and 
* Grails.

Jhipster is also very interesting if you want a fancy front end but don't want to learn whatever the latest hotness in JavaScript land is. 