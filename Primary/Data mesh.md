### Notes From The Book
+ Each domain becomes responsible for the data it is most familiar with. This is called the principle of domain ownership
+ Page 19 8th paragraf, excellent example of how we could extend the responsiblites of product teams
+ Domain data archtypes page 20-21, very important
+ Polysems are shared concepts across different domains, they point to the same entity with domain-specific attributes. Polysems represent shared core concepts in a business such as "artist", "listener" and "song". Following DDD(domain driven design) data mesh should allow different domains analytical data to model a polyseme according to the bounded context of their domain. However, it allows mapping a polyseme from one domain to another with global identication scheme.
+ In data mesh, a data pipeline is simply and internal implementation of the data domain and is handled internally within the domain. It's an implementation detail that must be abstracted from outside the domain.
+ Essentially the main idea of data mesh is to implement domain-driven bounded context modeling.
+ One thought I had while reading is that data product could also lead to greater collaboration betwen teams. Because you would have to think about how other teams will comsume your data, and how you will consume their data. Through this cross consumption maybe some use cases around features that help both teams becomes obvious.
+ One thought to go towards better discoverability of is to in looker have data under folders/schemas which have the names of produvt teams which are the domian which the data was generated in. Now if someone wants to know something about a domain they just look it up fast or contact that team for a quick walk through
+ To improve trust in our data we can have objective measures that remove uncertainty surrounding data aka SLO. A list of common such themes is on page 37.
+ openlineage a tool to trace data lineage. 
+ page 57. has a good list of tasks that a data product developer should focus on. Everything else should be taken care of by the platform. oage 59 5th paragraph gives some good examples of what the platform should do
+ I should investigate this "Bitemporal" idea, it seems quite useful. page 211 has a good explanation of it.
+ Maybe it is worth it to abandon the idea of having Redshift as our singe source of truth. Instead could be worth it to start thinking in slices of truth instead.
+ Page 239. has a set of attributes as an example of how to measure data quality. This is not about data a data product being good or bad. Rather its about what set of gurantees a data product can give.
+ page 241 exploring shape of the data without accessing individual records. For example through the use of the output port where we have funtions to investigate distriution of fields, value ranges, percentiles etc.
+ Every row of data in our system should be made immutable.
+ Read martin fowler "Microservice prerequisite"
+ When designing new systems of architectures it is good to have a fitness function in mind with which one can evaluate the progress and state of the system compared to where one wants it to be in an ideal state/stage
+ No centralised data architecture can coexist with data mesh, unless in transition