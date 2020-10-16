# azure cache for redis

My team found some problems with the initial implementation of redis cache in azure as a shared service, so the decision was made to continue with the individual application resource grouping. 
The pattern can been seen in the graphic from apim.

![redis](https://s3-us-west-1.amazonaws.com/donfouts.io/apim.png)

redis caches are deployed with terraform when justification for use is provided
redis caches are initally provisioned as small as possible - until useage metrics can be gathered to justify increasing capibilities or feature sets of the redis SKU's. 

[terraform modules](tfmodules.md)