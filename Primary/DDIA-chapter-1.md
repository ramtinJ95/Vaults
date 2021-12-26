# Foundations of data systems
Three main concern that are important in most software systems
- Reliability
- Scalability
- Maintainability

### Reliability
Expectations that are common are:
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

In an online system we measure the response time - that is, the time between a client sending a request and receiving a response.(Side note: The response time is what the client sees, besides the actual time to process the request (the **service time**) in includes network delays and queuing delays. Latency is the duration that a request is waiting to be handled - during which it is latent, awaiting service.) We need too think about response time not as a single number but rather as a distribution of values that you ca measure. As such average response time tells us not much and thus it is much better to use percentiles. Using percentiles we can use the median, p50, instead of the average response time. Also high percentiles of response times, **tail latencies**, are important because they directly affect users experience of the service. 

Queuing is a major part of response time since a server can only do a small amount of work in parallel and so it only takes a few slow requests to hold up the processing for following requests, aka **head-of-line blocking**. Due to this effect it is important to measure response time on the client side.

When testing and generating load, the generating client has to keep sending requests independently of the response time. Because if the client waits the queues will be shorter then they would have been.

**Scaling up**: vertical scaling, moving to a more powerful machine
**Scaling out**: horizontal scaling, distributing the load across multiple smaller machines. 

### Percentiles in practice
High percentiles become especially important in backend services that are called multiple times as part of serving a single end-user request. Even if you make the calls in parallel, the end-user request still needs to wait for the slowest of the parallel calls to complete. Even if only a small percentage of backend calls are slow, the chance of getting a slow call increases if an end-user requests requires multiple backend calls, and so a higher proportion of end-users requests end up being slow (an effect known as **tail latency amplification**)

If you want to add response time percentiles to the monitoring dashboards for your services, you need to efficiently calculate them on an ongoing basis. For example, you may want to keep a rolling window of response times of requests in the last 10 minutes. Every minute, you calculate the median and various percentiles over the values in that window and plot those metrics on a graph.

The naive implementation is to keep a list of response times for all requests within the time window and to sort that list every minute. If that is too inefficient for you, there are algos that can calculate good approximations of percentiles at minimal CPU and memory cost, such as forward decay, t-digest our HdrHistogram. Beware that averaging percentiles, e.g to reduce the time resolution or to combine data from several machines, is mathematically meaningless - the right way of aggregating response time data is to add the histograms. 


Scaling up: vertical scaling, moving to a more powerful machine
Scaling out: horizontal scaling, distributing the load across multiple smaller machines. 

### Maintainability
- Operability (dev ops team) make it easy for ops to run system smoothly
- Simplicity, make it easy for new devs to understand the system
- Evolvability, make it easy for engineers to make changes to the system in the future, adapting it for unanticipated use cases as requirements change.

---
Status: Done
tags: [[030 Software Development]] - [[Designing Data Intensive Applications by Martin Kleppmann]]
date:2021-12-26
