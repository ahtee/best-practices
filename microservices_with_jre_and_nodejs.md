# Microservices - JRE and Nodejs

Source from the [IBM Redbooks](http://www.redbooks.ibm.com/redbooks/pdfs/sg248358.pdf)

## Identifying candidates with the Monolith 🕵️🙋‍♀️

### Identifying Candidates 🔍

Candidates may be in the following situations:

- You are unable to deploy your application fast enough to meet requirements because of difficulty maintaining, modifying and becoming productive quickly, resulting in long cycles of time-to-market to roll out ner services. You are unable to build, test, and deploy your application in a timely manner.
- You are unbale to apply a single deployment. Usually it is necessary to invilve other modules or components to build, test, and deploy, even for small changes or enhancements. There is no separation of modules and components inside the same package of `.ear` or `.war` files.
- Only a single choice of technology exists and you cannot take advantage of new technologies, libraries, or techniques that are being adopted by other enterprises. Your current technology stack does not support the functionality you need. You want to generate documentation automatically from your code but the current technology used in your system or platform does not offer these features.

- Your large systems have the following characteristics:
  - High amount of data in memory :chart_with_upwards_trend: ❌
  - High-use CPU operations :chart_with_upwards_trend: ❌
  - Unable to scale a portion of the application; usually the entire application must be scaled. :chart_with_upwards_trend: ❌
  - Cannot be easily updated and maintained 🙅‍♂️ ❌
  - Code dependencies are difficult to manage :sob: ❌

## Considerations for moving to Microservices :thinking:

Consider the following important aspects before you move to microservices:

### Flexibility for the development platform :sweat_smile:

Microservices offer flexibility to choose the correct tool for the job; the idea is that each microservice can be backed by a different technology. A microservice can use different languagesl this enables you to choose the preferred technology for a particular problem rather than following the standard.

### Design by functionality and responsibilities :art:

Microservices offer separation of components and responsibilitiesL each microservice is responsible for a determinate topic. You may apply new features or improvements in specific parts of the system and also avoid mistakes or damage a part of the system that is working. This approach can be used for isolating older functionality; new functionality can be added to the monolith system by adding a microservice.

### Easily rewrite complete services :writing_hand:

Usually a microservice is a small services that are resy to rewrite, maintain, and change. Microservices provide a strong encapsulation model and a safe way to refactor and rewrite.

### Flexibility for changes :dancer:

With microservices, you can defer decision and have flexibility in the growth of your architecture as your understanding od the system and domain increases. You can defer difficult decisions until they are absolutely required. The only function that a service provides is a thin domain-aware wrapping over a data store, but the most important function to get correct is the **interface with which your other services interact**.

### Driving business value :car:

Business owners will be able to see the benefit of microservices because they want their teams to be able to respond rapidly to new customer and market needs. As we know today, the monolithic application approach slows down our response and we have to be extremely careful not to break parts of the application which may be dependent on any or all other parts.

Microservices are more aligned to business because they allow for frequent and faster delivery times than monolithic services. Microservices also allow business owners to get feedback quickly and adjust their investments accordingly.

  Other benefits are as follows: 💁‍♀️
  - Smaller focused teams enabling the business owners to easily manage resources more effectively, like moving more resources from low-impact areas to high-impact areas.
  - Scaling an individual microservice for removing bottlenecks enables a smoother user experience.
  - Identifying and eliminating duplicate services reduces development costs.

### Flexibility regarding scalability

With microservices, different parts of the system can be scaled. Each microservice is responsible for specific functionality, which results in more flexible scalability.

### Security zoning 👷:key: ✅

Security architects insist on a layered approach to building a system to avoid risk of having important code running on web-facing servers. Microservices can provide zoning that is analagous to the traditional layered approach. Business logic and critical data storage can be separated from the services that provide HTML rendering, for example. Communication between individual microservices can be firewalled, encrypted and secured in other ways.

## Decomposing the monilith application into microservices 🏗️🚧

### Choosing the Implementation Stack :point_right: :books:

Because microservices systems consist of individual services running as separate
processes, the expectation is that any competent technology that is capable of supporting
communication or messaging protocols works. The communications protocols might be, for
example, HTTP and REST. You must consider several aspects, though, when choosing the implementation stack:

### Synchronous versus Asynchronous 🛑⤴️vs 🔂

Classic stacks, such as Java Platform Enterprise Edition (Java EE), work by _synchronous
blocking_ on network requests. As a result, they must run in separate threads to be able to
handle multiple concurrent requests.

Asynchronous stacks, such Java Message Server (Java EE JMS) handle requests using
an event loop that is often single-threaded, yet can process many more requests when
handling them requires downstream input and output (I/O) operations.

### I/O versus processor (CPU) bound 📨 vs ⚡️

Solutions such as Node.js work well for microservices that predominantly deal with I/O
operations. Node.js provides for waiting for I/O requests to complete without holding up
entire threads. However, because the execution of the request is performed in the event
loop, complex computations adversely affect the ability of the dispatcher to handle other
requests. If a microservice is performing long-running operations, doing one of the
following actions is preferred:

1. Offload long-running operations to a set of workers that are written in a stack that is
best suited for CPU-intensive work (for example, Java, Go, or C).
2. Implement the entire service in a stack capable of multithreading.

### Memory 💭 and CPU ⚡️ requirements

Microservices are always expressed in plural because you run several of them, not only
one. Each microservice is further scaled by running multiple instances of it. There are
many processes to handle, and memory and CPU requirements are an important
consideration when assessing the cost of operation of the entire system. Traditional Java
EE stacks are less suitable for microservices from this point of view because they are
optimized for running a single application container, not a multitude of containers.
However, Java EE stacks, such as IBM WebSphere Liberty, mitigate this problem. Again,
stacks such as Node.js and Go are a go-to technology because they are more lightweight
and require less memory and CPU power per instance.

## Sizing Microservices 👨‍🍳

The following techniques can be used alone or in combination:

### Number of files 🔢

You can gauge the size of a microservice in a system by the number of files it consists of.
This is imprecise, but at some point you might want to break up a microservice that is
physically too large. Large services are difficult to work with, difficult to deploy, and take
longer to start and stop. However, be careful not to make them too small. When
microservices are too small, frequently referred to nanoservices as an anti-pattern, the
resource cost of deploying and operating such a service overshadows its utility. 

### Too many responsibilities 😱

A service that is responsible simultaneously for different subjects might need to be split up
because usually it is difficult to test, maintain, and deploy. Even if all of the responsibilities
are of the same type (for example, REST endpoints), there might be too many
responsibilities for a single service to handle.

### Service type 👨‍🔧

A good rule is that a microservice does only one thing, for example, one of the following
tasks:

1. Handle authentication
2. Serve several REST endpoints
3. Serve several web pages

Normally, you do not want to mix these same responsibilities. Although this might
seem the same as the "too many responsibilities" technique, when in fact it is not. It deals with the
quality, not the quantity, of the responsibilities. An anti-pattern might be a service that
serves web pages and also provides REST end-points, or serves as a worker.

### Bounded context separation ⛓

The name comes from a design pattern proposed by [Martin Fowler](http://martinfowler.com/bliki/BoundedContext.html). 
It represents parts of the system that are relatively self-sufficient, so there are few links
to a server that can be turned into microservices. If a microservice needs to talk to 10 other
microservices to complete its task, that can be an indication that the division was made in
an incorrect place in the monolith.

### Team organization 🎳

Many microservices systems are organized around teams that are responsible for writing
the code. Therefore, microservice partition follows team lines to maximize team
independence.

One of the key reasons microservices are popular as an architectural and organizational
pattern is that they allow teams to plan, develop, and deploy features of a system in the
cloud without tight coordination. 

## Refactoring ♻️

Refactoring is a practice that modernizes the application and gains resources provided by
new structures and platforms. The migration of a monolithic application to microservices
follows the same path. Refactoring adds microservices to an application without changing the
purpose of the application.

Starting over with new runtimes and programming languages is costly, especially when much
of the code is developed in Java and still works. Refactoring using microservices is a more
cautious approach because you can keep the old system running and move the monolithic
application in parts to a more sustainable and current platform.

### Strategy ✍️🤔💡

Moving a monolith application to microservices can involve these strategies: 

#### Convert the whole monolith application to microservices 🎛

The construction of a new application based on microservices __from scratch__ can be the
best option. However, because this approach can involve too much change at one time, it
is risky and often ends in failure. 

#### Refactor gradually 👍

This strategy is based on refactoring the monolith application gradually by building parts of
the system as microservices running together with the monolith application. Over time the
amount of functionality provided by the monolith application shrinks until it is completely
migrated to microservices. This is considered a __careful strategy__. 

- Do not add new features in the monolithic application; this prevents it from getting
larger. For all new features, use independent microservices.
  -  Create microservices organized around business capability, where each microservice
is responsible for one topic.
    - A monolithic application usually consists of layers, such as presentation, business
rules, and data access. You can create a microservice for presentation and create
another microservice for business access data. The focus is always on functionality
and business.
      - Use Bounded Context, dividing a complex domain into
multiple bounded contexts and mapping out the relationships between them, where a
natural correlation between service and context boundaries exists

## How to refactor JavaEE into Microservices 👩‍🏫

Consider these important aspects when moving Java Platform and Java EE applications to
microservices:

### Repackaging the application :package: 

Use the following steps:

1. **Split up the EARs or WAR files** ⚛️

Instead of packaging all of your related web archives (WARs) in one EAR, split them
into independent WARs. This might involve some minor changes to code, or more likely
to static content, if you change application context roots to be separate.

2. **Apply the container-per-service pattern** 👉🎨

Next apply the container-per-service pattern and deploy each WAR in its own
application server, preferably in its own container (such as a Docker container). You can then scale containers independently.

3. **Build, deploy, and manage each WAR independently** 🚢🛳⛴
  
After they are split, you can manage each WAR independently through an automated
DevOps pipeline (such as Jenkins, AWS's CodePipeline or Azure's AzurePipelines). This is a step toward
gaining the advantages of continuous delivery.

### Refactoring the monolith code 🎒

After repackaging, where your deployment strategy is down to the level of independent
WARs, you can start looking for opportunities to refactor:

1. **Front-end** 🕸

For simple program servlets/JSPs that are usually front ends to database tables,
create a domain layer that you can represent as a RESTful service. Identifying your
domain objects by applying domain-driven design can help you identify your missing
domain services layer. After building, in the next phase you can refactor your existing
servlet/JSP application to use the new service or build a new interface using
JavaScript, HTML5, and CSS, or as a native mobile application.

2. **RESTful services** 😴
  
You might have existing services that are compatible, or can be made compatible, with
a microservices architecture. Start by untangling each REST or simple JMS service 
Chapter 3. Identifying candidates within the monolith 45
from the remainder of the WAR, and then deploy each service as its own WAR.

### Refactoring monolith data 🏎
 
The next step might be the most difficult problem in adopting microservices. That step is to create a
new data model for each microservice based on the current data model.

#### Here are the rules to follow: 👨‍🏫📏

#####  Isolated islands of data 🏝

Begin by looking at the database tables that your code uses. If the tables used are
either independent of all other tables or come in a small, isolated island of a few tables
joined by relationships, you can split those out from the rest of your data design. 

For defining which database to use, verify the types of queries that you want to use. If
most of the queries you use are simple queries on primary keys, a key-value database
or a document database might be the best option. However, if you do have complex
joins that vary widely (for example, the queries are unpredictable), staying with SQL
might be your best option.

##### Batch data updates 👨‍🍳

If you have only a few relationships and you decide to move your data into a NoSQL
database anyway, consider whether you only need to do a batch update into your
existing database. Often, when you consider the relationships between tables, the
relationships do not consider a time factor; they might not always need to be up to date.
A data dump and load approach that runs every few hours might be sufficient for many
cases.

##### Table denormalization 🍽

If you have more than a few relationships to other tables, you might be able to refactor
(or in database administrator terms, denormalize) your tables.
Often, the reason for using highly normalized schemas was to reduce duplication,
which saved space, because disk space was expensive. However, disk space is now
inexpensive. Instead, query time is now what you must optimize; denormalization is a
straightforward way to achieve that optimization.

## Enterprise data access patterns

- Distributed data management
- Data consistency
- Communication between microservices
- Integration with monolith application
  - Modifying the monolith application
- Which database to use
  - Relational or NoSQL
  
## Security and Governance

- Security in microservices
- Governance in microservices

## Performance

- Common problems
- Antipatterns to avoid
- Practices to improve performance

## DevOps and Automation

- Deployment automation
- Monitoring
- Performance
