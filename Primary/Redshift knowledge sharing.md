+ Go through a quick overview of redshift architecture. https://www.youtube.com/watch?v=13iIj34nkQE&ab_channel=AWSEvents good example of how sort keys work etc.
	+ memory blocks
	+ Zone maps
	+ Data sorting
	+ Data distribution co-locate large tables using diststyle key using high cardinality column (with many unique values). For sort key low cardinality column is best.
+ WLM redshift using transient clusters called concurrency scaling for speeding up usage feeling of DS's. SQA, short query accelaration.
+ Query monitoris rules. 
+ concurrency scaling seems to be quite important. 
+ Materialized views, compute once query many times.
+ important that i explain why joining two tables which have the same dist key gives good performance. 

+ https://www.youtube.com/watch?v=jRuE7tdZisU&ab_channel=AurobindoSaha really good. 


### Solution to our problems that pop up in my head
+ We could do a brute force fix and just set diststyle all to spread out the data we have to each compute node, that would speed up query speed significantly. 