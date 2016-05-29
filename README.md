# Domain Driven Design Based Enterprise Application Framework

An Enterprise Application Framework based on different Patterns, Principles and Practices of Domain Driven Design.Although not all tactical and strategic Patterns, Principles and Practices of DDD are in place but the most important ones(the ones that are used almost in any Enterprise app) are in place.Will try to connect most of the dots in future with time.This being a Framework, any application specific stuff is not there and will never be there in the Core code.

This framework is also helpful in scenarios wherein one needs to interact with different Integration technologies using different .NET based access technologies(can be DBs, SOAP or RESTFUL Web Services or MQs or File Sysstem or an LDAP or any other imaginable data source).Another possible scenario can be in a CQRS environment wherein the commands are processed in an RDBMS like SQL Server whereas the queries are executed to fetch data from NOSQL DBs.

Implementation Overview-> 
Here the CommandRepository(for persisting data) and QueryableRepository(for querying data) are in-memory representation of some external source - mainly DBs(but can be extended to Web Services or MQ interactions as well or any other imaginable data source for that matter).
The CommandRepository class needs instances of concrete implementation of BaseUnitOfWork and ICommand which can be injected using some DI Framework like Unity.

UnitOfWork (inherits and overrides BaseUnitOfWork members) - De-couples the logic to do atomic transactions across Dbs(can be extended to use Web Services/MQs or some other data source as well to be part of the Transaction) using different DB access technologies(again can be extended to use Web Service/MQs or any other data source) .

ICommand & IQuery- Provides contracts to deal with different DB technologies viz. ADO.NET,Enterprise Library or ORMs like Entity FrameWork Code First etc and different DBs(current implementation supports mainly SQL Server - but as mentioned eralier also, can be extended to support other DB types as well).

Pending Tasks ->

• Will use SQL Express for integration testing of Transaction Management.SQL CE and SQL Lite seems to have lot of issues in this respect (alongwith not supporting DateTimeOffset). Don't want to spend much time on SQL CE/Lite just for testing purpose.

• Testing BulkOperations using SQL Express Edition.

• Testing of Fluent APIs and Asynchronous Operations.

• Redesign Caching stuffs to support in-memory caching or some scalable option like Windows AppFabric or Redis(a scalable NOSQL option). Ideally, should be designed in a pluggable way to support any cool Caching mechanism coming in future as well.Also should use some AOP or attribute(annotation) based approach to apply Caching or invalidating the Cache else it becomes very hectic to apply these cross cutting concerns everywhere within a large application.

• Fixing or suppressing the Warnings generated by MS Code Analysis Tool (currently, Code Analysis Settings is set to "Microsoft Basic Design Guidelines")

• Also need to Run the Code Metrics to check everything is as per standards

References(not that everything mentioned below is referred to build this framework, but atleast some bits of each of these awesome resources mentioned below have been referred or will be referred) -   
1) [Patterns, Principles and Practices of Domain Driven Design](http://www.wrox.com/WileyCDA/WroxTitle/Patterns-Principles-and-Practices-of-Domain-Driven-Design.productCd-1118714709.html)  
2) [Implementing Domain Driven Design](https://vaughnvernon.co/?page_id=168)  
3) [CQRS Journey](https://msdn.microsoft.com/en-us/library/jj554200.aspx)  
4) [Javascript Domain Driven Design](https://www.packtpub.com/web-development/javascript-domain-driven-design)  
5) [Coding for Domain Driven Design](https://msdn.microsoft.com/en-us/magazine/dn342868.aspx)  
6) [Domain Driven Design Wiki](https://en.wikipedia.org/wiki/Domain-driven_design)  
7) Some good open source DDD apps- [I](http://stackoverflow.com/questions/152120/are-there-any-open-source-projects-using-ddd-domain-driven-design) and [II](http://stackoverflow.com/questions/540130/good-domain-driven-design-samples)  
8) [HTTP: The Definitive Guide](shop.oreilly.com/product/9781565925090.do) and [Restful Web Services](https://www.crummy.com/writing/RESTful-Web-Services/html/)  
9) [Restful Web APIs](http://shop.oreilly.com/product/0636920028468.do) and [Rest in Practice](http://shop.oreilly.com/product/9780596805838.do)  
10) [Almost Anything and Everything about ASP.NET Web API](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api)(including [ASP.NET WEB API 2: HTTP MESSAGE LIFECYLE](http://www.asp.net/media/4071077/aspnet-web-api-poster.pdf))    
11) [Designing Evolvable Web APIs with ASP.NET](http://chimera.labs.oreilly.com/books/1234000001708)  
12) [24 Deadly Sins of Software Security](http://www.amazon.in/Deadly-Sins-Software-Security-Programming/dp/0071626751), [Federated Identity](https://en.wikipedia.org/wiki/Federated_identity),[Guide to Claims based Identity and Access Control](https://msdn.microsoft.com/en-us/library/ff423674.aspx) and [An Updated Look At Choosing Between OAuth2 and SAML](https://www.mutuallyhuman.com/blog/2015/07/17/an-updated-look-at-choosing-between-oauth2-and-saml/)  
13) [Single Page Web Applications](https://www.manning.com/books/single-page-web-applications)  
14) [Telerik Academy's ShowcaseSystem(having a quite good SPA sample using Angular.js)](https://github.com/TelerikAcademy/ShowcaseSystem)  


P.S. -> Planning to have a port of this codebase in Node.js(Javascript). Node.js is becoming very popular for Web/Mobile development being very good at handling I/O intensive work rather than Compute Intensive work(& I/O intensive work is what most of the Web/Mobile Apps deal with). On the contrary C,C++,Java,C#,F# etc like primitive server side languages(although F# is not that primitive) are more suitable for Compute Intensive work(e.g. some Engineering/Science application, Workflows having Complex Business Computational logic or even a Web/Mobile app being very computational). Anyways, Node.js(javascript) seems to be now mainstream for Enterprise Apps(atleast Enterprise Web Apps) and that's why I feel a Node.js(Javascript) port of this codebase should be there.But that's not going to happen soon since the conversion process itself is going to take some time. Agreed that there are converters(from C# to JS) available as suggested [here](http://stackoverflow.com/questions/16434389/javascript-and-c-sharp-cross-compiling-and-conversion) but doubt the performance and coding standards of such generated code.Might go via the lengthy learning curve(i.e. revising some JS stuffs and also learning some new stuffs) or via the converter approach or a mix and match of both the approaches but all these is going to happen after I satisfactorily finish off this current .NET code base which itself has quite a few pending items. A very good read on Node.js and .NET comparison is available [here](http://www.haneycodes.net/to-node-js-or-not-to-node-js/). As suggested in the comparison article, it's not very difficult to implement Event Loop in C# - just do a google search for "C# + Event Loop" and you will get quite a few good options.

And if you want to have insane performance then try out the LMAX
way ([Disruptor in the Java Servlet and handling multiple events](http://stackoverflow.com/questions/18375147/using-disruptor-in-the-java-servlet-and-handling-multiple-events), [Log4j-2 Performance close to insane](https://www.grobmeier.de/log4j-2-performance-close-to-insane-20072013.html), [Disruptor-NET](http://elekslabs.com/2013/01/disruptor-net.html)). Probably I am going to become insane too soon and try out building a self hosted OWIN Katana Server based on OWINMiddleware and the LMAX Disruptor pattern, within this application itself. Also want to check, to what level of insanity it goes to, if the highly scalable "Event Driven Rest" approach (one of the best options for integrating Bounded Contexts) is added alongwith the LMAX insanity.
