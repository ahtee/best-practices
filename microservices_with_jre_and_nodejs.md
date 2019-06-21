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

### Considerations for moving to Microservices :thinking:

Consider the following important aspects before you move to microservices:

- Flexibility for the development platform :sweat_smile:

Microservices offer flexibility to choose the correct tool for the job; the idea is that each microservice can be backed by a different technology. A microservice can use different languagesl this enables you to choose the preferred technology for a particular problem rather than following the standard.

- Design by functionality and responsibilities :art:

Microservices offer separation of components and responsibilitiesL each microservice is responsible for a determinate topic. You may apply new features or improvements in specific parts of the system and also avoid mistakes or damage a part of the system that is working. This approach can be used for isolating older functionality; new functionality can be added to the monolith system by adding a microservice.

- Easily rewrite complete services :writing_hand:

Usually a microservice is a small services that are resy to rewrite, maintain, and change. Microservices provide a strong encapsulation model and a safe way to refactor and rewrite.

- Flexibility for changes :dancer:

With microservices, you can defer decision and have flexibility in the growth of your architecture as your understanding od the system and domain increases. You can defer difficult decisions until they are absolutely required. The only function that a service provides is a thin domain-aware wrapping over a data store, but the most important function to get correct is the **interface with which your other services interact**.

- Driving business value :car:

Business owners will be able to see the benefit of microservices because they want their teams to be able to respond rapidly to new customer and market needs. As we know today, the monolithic application approach slows down our response and we have to be extremely careful not to break parts of the application which may be dependent on any or all other parts.

Microservices are more aligned to business because they allow for frequent and faster delivery times than monolithic services. Microservices also allow business owners to get feedback quickly and adjust their investments accordingly.

  Other benefits are as follows: 💁‍♀️
  - Smaller focused teams enabling the business owners to easily manage resources more effectively, like moving more resources from low-impact areas to high-impact areas.
  - Scaling an individual microservice for removing bottlenecks enables a smoother user experience.
  - Identifying and eliminating duplicate services reduces development costs.

- Flexibility regarding scalability

With microservices, different parts of the system can be scaled. Each microservice is responsible for specific functionality, which results in more flexible scalability.

- Security zoning 👷

Security architects insist on a layered approach to building a system to avoid risk of having important code running on web-facing servers. Microservices can provide zoning that is analagous to the traditional layered approach. Business logic and critical data storage can be separated from the services that provide HTML rendering, for example. Communication between individual microservices can be firewalled, encrypted and secured in other ways.

### Decomposing the monilith application into microservices 🏗️🚧



### Refactoring ♻️

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
