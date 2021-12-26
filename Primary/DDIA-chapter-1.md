# Foundations of data systems
Three main concern that are important in most software systems
- Reliability
- Scalability
- Maintainability

### Reliability
Expectations that are comman are:
- The application performs the function that the user expected.
- The application can tolerate the user making mistakes or using the software in unexpected ways.
- The applications performance is good enough for the required use case, under expected load and data volume. 
- The system prevents any unauthorized access and abuse.

So we can say that reliability is essentially that the systems keep working correctly even if something goes wrong. Human error is something to account for heavily.

### Scalability
If one wants to determine the scalability of a system there are two metrics that need to be measured first. We need to measure load and performance.

Load Description; The numbers that describe the system load are called **load parameters**. Depending on the application it can be:
- Requests per second to a web server
- Ratio of reads and writes to DB
- Hit rate on cache
- Number of concurrent users

A good term to be familiar with her is **fan-out** which describes the number of requests to other services that we need to make in order to serve one incoming request.

Performance Description; Two ways of looking at this:
- When you increase a load parameter and keep the system resources(CPU, memory, bandwidth, etc) unchanged, how is the system affected
- When increasing a load parameter how much do you need to increase resources to keep the performance of the system unchanged. 


---
Status: Done
tags: [[030 Software Development]] - [[Designing Data Intensive Applications by Martin Kleppmann]]
date:2021-12-26
