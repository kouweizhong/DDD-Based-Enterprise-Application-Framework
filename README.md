# Domain Driven Design Based Enterprise Application Framework

An opinionated Enterprise Application Framework based on different Patterns, Principles and Practices of Domain Driven Design.Although not all tactical and strategic Patterns, Principles and Practices of DDD are in place but the most important ones(the ones that are used almost in any Enterprise app) are in place.Will try to connect most of the dots in future with time.This being a Framework, any application specific stuff is not there and will never be there in the Core code.

This framework is also helpful in scenarios wherein one needs to interact with different Integration technologies using different .NET based access technologies(can be DBs, SOAP or RESTFUL Web Services or MQs or File Sysstem or an LDAP or any other imaginable data source).Another possible scenario can be in a CQRS(Command Query Responsibility Seggregation) environment wherein the commands are processed in an RDBMS like SQL Server whereas the queries are executed to fetch data from NOSQL DBs.Also, once this framework is completed and if someone uses this framework, atleast for the development of a SPA based Web Application or Website or a Mobile Web application, ideally he/or she should need to work only on Domain Modelling(i.e. mainly Domain,Domain Services and Application Services) and UI stuffs(there might be some requirement for extending some extensibility points which are already provided out of the box or creating new extensibility points all-together or some other configuration stuff changes required like DI container specific stuffs or ORM configurations if RDBMS is used etc).That doesn't mean that all these can be applied only for Web apps or Websites or Mobile Web Application only but in-fact, parts of this framework can be applied to Business Process Management and Integration projects as well.

But please don't use this framework for some simple domain.DDD is more about domain modelling for complex domains using concepts of Entities,Value Objects, Aggregates etc and separating out your Business functionalities from your technical functionalities. Although this framework provides(or will provide) most of the technical functionalities(out of the box, including the source code) used in an Enterprise app and some base level classes for dealing with Entities,Value Objects, Aggregates etc but it's not necessary that one is going to need every bit of it. So use this framework(or may be just parts of the framework) deligently after analyzing the requirements for your app meticulously.

Implementation Overview-> 
Here the CommandRepository(for persisting data) and QueryableRepository(for querying data) are in-memory representation of some external source - mainly DBs(but can be extended to Web Services or MQ interactions as well or any other imaginable data source for that matter).
The CommandRepository class needs instances of concrete implementation of BaseUnitOfWork and ICommand which can be injected using some DI Framework like Unity.

UnitOfWork (inherits and overrides BaseUnitOfWork members) - De-couples the logic to do atomic transactions across Dbs(can be extended to use Web Services/MQs or some other data source as well to be part of the Transaction) using different DB access technologies(again can be extended to use Web Service/MQs or any other data source) .

ICommand & IQuery- Provides contracts to deal with different DB technologies viz. ADO.NET,Enterprise Library or ORMs like Entity FrameWork Code First etc and different DBs(current implementation supports mainly SQL Server - but as mentioned eralier also, can be extended to support other DB types as well).

Pending Tasks ->

• Incorporation of some tactical DDD stuffs(mainly the common framework elements)

• Trying exploring and incorporating Dapper(a Micro-ORM - Micro ORMs may not provide you some functionalities like UnitOfWork out of the box like that of an ORM but performance wise they are way better compared to ORMs), Event Stores and Grid Based Storage.

• Incorporation of some Restful stuffs(again the core framework elements), including one of the major strategic DDD pattern -   
  "Event Driven Rest" which is one of the best Integration options based on pure HTTP and optimal for scenarios where Eventual Consistency rather than Transaction Consistency should be the way to go.     
  N.B. -> One can refer the paper - [Your Coffe Shop Doesn't use 2 phase commit](http://www.enterpriseintegrationpatterns.com/docs/IEEE_Software_Design_2PC.pdf)(written by the Integration genius - Gregor Hohpe, author of the Integration Bible viz. [Enterprise Integration Patterns](http://www.enterpriseintegrationpatterns.com/)) to see how apps can be implemented without using Transactional Consistency.

• Will use SQL Express for integration testing of Transaction Management.SQL CE and SQL Lite seems to have lot of issues in this respect (alongwith not supporting DateTimeOffset). Don't want to spend much time on SQL CE/Lite just for testing purpose.

• Testing BulkOperations using SQL Express Edition.

• Testing of Fluent APIs and Asynchronous Operations.

• Redesign Caching stuffs to support in-memory caching or some scalable option like Windows AppFabric or Redis(a scalable NOSQL
  option). Ideally, should be designed in a pluggable way to support any cool Caching mechanism coming in future as well.Also should use some AOP or attribute(annotation) based approach to apply Caching or invalidating the Cache else it becomes very hectic to apply these cross cutting concerns everywhere within a large application.

• Fixing or suppressing the Warnings generated by MS Code Analysis Tool (currently, Code Analysis Settings is set to "Microsoft
  Basic Design Guidelines")

• Also need to Run the Code Metrics to check everything is as per standards

References(not that everything mentioned below is referred to build this framework, but atleast some bits of each of these awesome resources mentioned below have been referred or will be referred) -   
1) [Patterns, Principles and Practices of Domain Driven Design](http://www.wrox.com/WileyCDA/WroxTitle/Patterns-Principles-and-Practices-of-Domain-Driven-Design.productCd-1118714709.html)  
2) [Implementing Domain Driven Design](https://vaughnvernon.co/?page_id=168)  
3) [CQRS Journey](https://msdn.microsoft.com/en-us/library/jj554200.aspx)  
4) [Javascript Domain Driven Design](https://www.packtpub.com/web-development/javascript-domain-driven-design)  
5) [Coding for Domain Driven Design](https://msdn.microsoft.com/en-us/magazine/dn342868.aspx)  
6) [Domain Driven Design Wiki](https://en.wikipedia.org/wiki/Domain-driven_design)  
7) Some good open source DDD apps- [I](http://stackoverflow.com/questions/152120/are-there-any-open-source-projects-using-ddd-domain-driven-design) and [II](http://stackoverflow.com/questions/540130/good-domain-driven-design-samples)  
8) [HTTP: The Definitive Guide](shop.oreilly.com/product/9781565925090.do) and [Restful Web Services Cookbook](http://shop.oreilly.com/product/9780596801694.do)  
9) [Restful Web APIs](http://shop.oreilly.com/product/0636920028468.do) and [Rest in Practice](http://shop.oreilly.com/product/9780596805838.do)  
10) [Almost Anything and Everything about ASP.NET Web API](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api)(including [ASP.NET WEB API 2: HTTP MESSAGE LIFECYLE](http://www.asp.net/media/4071077/aspnet-web-api-poster.pdf))    
11) [Designing Evolvable Web APIs with ASP.NET](http://chimera.labs.oreilly.com/books/1234000001708)       
12) Some good Hypermedia Resources(needed for Event Driven Rest) - [The value proposition of Hypermedia](https://lostechies.com/jimmybogard/2014/09/23/the-value-proposition-of-hypermedia/), [Level Up your Web API with Hypermedia](https://channel9.msdn.com/Events/TechEd/NewZealand/2013/DEV305), [Generating Hypermedia links in ASP.NET Web API](http://benfoster.io/blog/generating-hypermedia-links-in-aspnet-web-api) and [Building Hypermedia Web APIs with ASP.NET Web API](https://msdn.microsoft.com/en-us/magazine/jj883957.aspx)    
13) [24 Deadly Sins of Software Security](http://www.amazon.in/Deadly-Sins-Software-Security-Programming/dp/0071626751), [Federated Identity](https://en.wikipedia.org/wiki/Federated_identity),[Guide to Claims based Identity and Access Control](https://msdn.microsoft.com/en-us/library/ff423674.aspx) and [An Updated Look At Choosing Between OAuth2 and SAML](https://www.mutuallyhuman.com/blog/2015/07/17/an-updated-look-at-choosing-between-oauth2-and-saml/)  
14) [Single Page Web Applications](https://www.manning.com/books/single-page-web-applications)  
15) [Telerik Academy's ShowcaseSystem(having a quite good SPA sample using Angular.js)](https://github.com/TelerikAcademy/ShowcaseSystem)  

Other Good Resources – Most of the references mentioned above are really good(especially for developing this Application Framework) but the resources mentioned  below can hopefully make you a better Coder/Designer/Architect/Systems Programmer –>     

1) Coding -> Some good resources in .NET space are [C# 6.0 in a Nutshell]( http://www.albahari.com/nutshell/about.aspx), [C# in Depth]( http://csharpindepth.com/), [CLR Via C#](http://www.wintellect.com/devcenter/jeffreyr/what-s-new-in-clr-via-c-4th-edition-as-compared-to-the-3rd-edition), [.NET 4.0 Generics Beginner’s Guide]( https://www.packtpub.com/application-development/net-40-generics-beginner%E2%80%99s-guide), [MetaProgramming in .NET]( https://www.manning.com/books/metaprogramming-in-dot-net), [Pro DLR in .NET 4.0](http://www.apress.com/9781430230663), [Concurrency in C# Cookbook]( http://shop.oreilly.com/product/0636920030171.do),[Learn Roslyn Now Series]( https://joshvarty.wordpress.com/learn-roslyn-now/) and [Domain Specific Language in .NET] (http://udooz.pressbooks.com/). Although not a .NET resource(rather a Java resource), an awesome DSL(Domain Specific Language) resource is [Language Implementation Patterns](https://pragprog.com/book/tpdsl/language-implementation-patterns). A  coder/programmer/developer can opt for peeking into other languages/paradigms as well (via which one can use some unique aspect of some programming language into his/her favorite programming language to develop something cool or can become a Polyglot Programmer) and for that, one can refer [Pragmatic Bookshelf’s 7 in 7 series] (https://pragprog.com/categories/7in7). A programming language which is in quite hype nowadays is Node.js and for that, one can refer - [You don’t know JS Series]( https://github.com/getify/You-Dont-Know-JS ),[Stoyan Stefanov's JS Books](http://www.amazon.com/Stoyan-Stefanov/e/B002BLXYIG),[
Nicholas C. Zakas' JS Books](http://www.amazon.com/Nicholas-C.-Zakas/e/B001IGUTOC), [Learning Javascript Design Patterns](https://addyosmani.com/resources/essentialjsdesignpatterns/book/), [Node.js Resources]( http://davidherron.com/book/2015-09-14/books-and-videos-so-you-can-easily-learn-nodejs-programming ),[Node.js Architecture slides from Slideshare](http://www.slideshare.net/search/slideshow?searchfrom=header&q=node.js+architect), [JS material available at MDN]( https://developer.mozilla.org/en-US/docs/Web/JavaScript) and [Other JS resources]( http://blog.reybango.com/2010/12/15/what-to-read-to-get-up-to-speed-in-javascript/)(by the way, one can refer Addy Osmani's, Stoyan Stefanov's and Nicholas Zakas' blogs as well for some intriguing stuffs). Although the Javascript world have been moving towards Object Orientation(ES6 and ES7) but the irony is that the traditional Object Oriented languages like Java,C# have been moving more towards the functional side and for functional approaches, one can refer(mainly JS and .NET based language resources) - [Functional Programming in C#](http://www.wrox.com/WileyCDA/WroxTitle/Functional-Programming-in-C-Classic-Programming-Techniques-for-Modern-Projects.productCd-0470744588.html), [LINQ and Functional Programming via C#](http://weblogs.asp.net/dixin/linq-via-csharp), [Learning F#](http://fsharp.org/learn.html), [Functional Javascript](http://shop.oreilly.com/product/0636920028857.do) and [Functional Programming in Javascript](https://www.packtpub.com/web-development/functional-programming-javascript). And for Unit Testing, [The Art of Unit Testing]( http://artofunittesting.com/) seems to be the best resource.

2) Design, Architecture and DevOps – Some good resources in general for this space are [Patterns Literature]( https://insightsdelight.wordpress.com/2011/10/12/patterns-literature/), [RDBMS Data Modelling]( http://www.agiledata.org/essays/dataModeling101.html), [NOSQL Data Modelling](https://highlyscalable.wordpress.com/2012/03/01/nosql-data-modeling-techniques/), [O’Reilly’s Beautiful X Series]( http://product.hubspot.com/bid/24069/O-Reilly-s-Beautiful-X-Series), [The Architecture of Open Source Applications]( http://aosabook.org/en/index.html), [Application Architecture Posts by Martin Fowler]( http://martinfowler.com/tags/application%20architecture.html), [Application Integration Posts by Martin Fowler]( http://martinfowler.com/tags/application%20integration.html), [Enterprise Architecture Posts by Martin Fowler]( http://martinfowler.com/tags/enterprise%20architecture.html), [Practical SOA For the Solution Architect]( https://www.youtube.com/watch?v=1KXKppaOgtY), [Almost anything and everything on SOA from Manning](https://www.manning.com/catalog#section-58), [Microservices Architecture]( http://microservices.io/), [O’Reilly’s Software Architecture Series]( http://www.oreilly.com/software-architecture-video-training-series.html), [Architectural Styles and Patterns]( https://en.wikipedia.org/wiki/Architectural_pattern) (including [Hexagonal Architecture]( https://www.infoq.com/news/2014/10/exploring-hexagonal-architecture), [Onion Architecture]( http://blog.thedigitalgroup.com/chetanv/2015/07/06/understanding-onion-architecture/) and [Microkernel Architecture]( http://viralpatel.net/blogs/microkernel-architecture-pattern-apply-software-systems/ )), [Multi Layered Architectures in .NET](http://www.mono.hr/Pdf/Muilt-Layered%20Architectures%20in%20.Net-Web.pdf), [Are you a Software Architect](https://www.infoq.com/articles/brown-are-you-a-software-architect), [How to Interview a Software Architect](https://www.youtube.com/watch?v=t2Ti-pZGy8I) and [DevOps in Practice] (https://pragprog.com/book/d-devops/devops-in-practice). Some good resources in this space from the Software Engineering perspective are [Architecting High Performing, Scalable and Available Enterprise Web Applications]( http://www.amazon.in/Architecting-Performing-Available-Enterprise-Applications/dp/0128022582/ref=la_B00OTWHRRO_1_1?s=books&ie=UTF8&qid=1441731036&sr=1-1 ), [Just Enough Software Architecture]( http://www.amazon.in/Just-Enough-Software-Architecture-Risk-Driven/dp/0984618104)(some  [recommended texts]( http://georgefairbanks.com/software-architecture/book-recommendations/ ) by this author), [Software Architecture for Developers]( https://leanpub.com/software-architecture-for-developers), [DevOps : A Software Architect’s Perspective ]( http://ssrg.nicta.com.au/projects/devops_book/), [Architecture Principles : The cornerstones of Enterprise Architecture] (http://www.amazon.com/Architecture-Principles-Cornerstones-Enterprise-Engineering/dp/3642202780/ref=sr_1_78?s=books&ie=UTF8&qid=1308252595&sr=1-78 ) and [Other Software Architecture Resources]( https://www.linkedin.com/pulse/10-must-read-books-software-architects-ganesh-samarthyam ).Again from the Systems Programming and Distributed Computing perspective, some good resources are like [Distributed Computing for Fun and Profit]( http://book.mixu.net/distsys/ebook.html), [High Scalability All Time Favorites]( http://highscalability.com/all-time-favorites/), [High Scalability Real Life Architectures]( http://highscalability.com/blog/category/example), [All Things Distributed]( http://www.allthingsdistributed.com/)(Amazon CTO’s blog), [Mechanical Sympathy]( http://mechanical-sympathy.blogspot.in/ )(blog of one of the brainchild behind the superb [LMAX Architecture]( http://martinfowler.com/articles/lmax.html)), [Operating System Support for Warehouse Scale Computing]( https://www.cl.cam.ac.uk/~ms705/pub/thesis-submitted.pdf) and [The Not so Small list of almost all Distributed Computing Resources]( https://www.quora.com/What-are-some-good-resources-for-learning-about-distributed-computing-Why). And last but not the least, from a Cloud Computing perspective, some good resources are like [Cloud Computing Patterns](http://www.cloudcomputingpatterns.org/), [Cloud Patterns](http://www.cloudpatterns.org/), [MS Azure Cloud Development resources from Patterns and Practices](https://msdn.microsoft.com/en-us/library/ff898430.aspx), [MS Azure Solutions](https://azure.microsoft.com/en-in/), [MS Azure Certifications](https://buildazure.com/2015/12/09/microsoft-azure-certification-where-to-start/), [AWS Architecture Centre](https://aws.amazon.com/architecture/?nc1=f_cc), [AWS Security Centre](https://aws.amazon.com/security/?nc1=f_cc), [AWS Solutions](https://aws.amazon.com/solutions/) and [AWS Certifications](https://aws.amazon.com/certification/).

*** Also,one can refer [Udacity Courses](https://www.udacity.com/courses/all)(alongwith [Downloads](https://www.udacity.com/wiki/downloads)), [Coursera Courses](https://www.coursera.org/courses?_facet_changed_=true&domains=computer-science&languages=en&query=free+courses&start=60) and [eDX courses](https://www.edx.org/course) for overall breadth and depth of Computer Science and Engineering.

N.B. -> It’s not that I have read/viewed everything mentioned above but yes, I have read/viewed a few of them (partially or completely) and many are yet to be even started(for reading) but all the resources mentioned above are some of the best resources(as per my interaction with some beautiful minds and my own exploration). Also, something not mentioned in the above list doesn't mean that it's not good - only that I am not aware of(or not my preference). Believe me or not this is a jotted down version of a much bigger list which is a nightmare. But even if someone reads just one resource, don’t just mug it up but rather try some PoCs, the DIY(Do it Yourself) way. May be start with something small (e.g. small PoCs) and then ultimately come up with some big and innovative idea and start building the same. I have no idea whether this project is "big and innovative" or not but some geeky interviewers do ask you whether you have developed something "big and innovative" end to end on your own, which could have acted as some bit of thrust for this project initiative but that’s not the reason behind building this framework (and anyways this might be big but no-where near to any real innovation).They say “Necessity is the mother of Invention” but for some people “Laziness is the mother of Necessity”  and I am a very lazy guy, atleast in doing the same stuffs again and again (especially developing the same technical functionalities again and again) and that’s the main reason behind this initiative (to provide the most important technical functionalities used in almost any Enterprise app, out of the box, including the source code along-with providing some basic tactical and strategic DDD stuffs).     

P.S. -> Planning to have a port of this codebase in Node.js(Javascript). Node.js is becoming very popular for Web/Mobile development being very good at handling I/O intensive work rather than Compute Intensive work(& I/O intensive work is what most of the Web/Mobile Apps deal with). On the contrary C,C++,Java,C#,F# etc like primitive server side languages(although F# is not that primitive) are more suitable for Compute Intensive work(e.g. some Engineering/Science application, Workflows having Complex Business Computational logic or even a Web/Mobile app being very computational). Anyways, Node.js(javascript) seems to be now mainstream for Enterprise Apps(atleast Enterprise Web Apps) and that's why I feel a Node.js(Javascript) port of this codebase should be there.But that's not going to happen soon since the conversion process itself is going to take some time. Agreed that there are converters(from C# to JS) available as suggested [here](http://stackoverflow.com/questions/16434389/javascript-and-c-sharp-cross-compiling-and-conversion) but doubt the performance and coding standards of such generated code.Might go via the lengthy learning curve(i.e. revising some JS stuffs and also learning some new stuffs) or via the converter approach or a mix and match of both the approaches but all these is going to happen after I satisfactorily finish off this current .NET code base which itself has quite a few pending items. A very good read on Node.js and .NET comparison is available [here](http://www.haneycodes.net/to-node-js-or-not-to-node-js/). As suggested in the comparison article, it's not very difficult to implement Event Loop in C# - just do a google search for "C# + Event Loop" and you will get quite a few good options.

And if you want to have insane performance then try out the LMAX
way ([Disruptor in the Java Servlet and handling multiple events](http://stackoverflow.com/questions/18375147/using-disruptor-in-the-java-servlet-and-handling-multiple-events), [Log4j-2 Performance close to insane](https://www.grobmeier.de/log4j-2-performance-close-to-insane-20072013.html), [Disruptor-NET](http://elekslabs.com/2013/01/disruptor-net.html)). Probably I am going to become insane soon and try out building a self hosted OWIN Katana Server based on OWINMiddleware and the LMAX Disruptor pattern, within this application itself. Also want to check, to what level of insanity it goes to, if the highly scalable "Event Driven Rest" approach (one of the best options for integrating Bounded Contexts) is added alongwith the LMAX insanity.
