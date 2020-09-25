# azure cache for redis

my team found some problems with the inital impementation of redis cache in azure as a shared service, so the decision was made to continue with the individual application resource grouping. 
the pattern can been seen in the graphic from apim.

![redis](https://stdsoinventory0001.blob.core.windows.net/mdwikiimages/apim.png)

redis caches are deployed with terraform when justification for use is provided
redis caches are initally provisioned as small as possible - until useage metrics can be gathered to justify increasing capibilities or feature sets of the redis SKU's. 

[terraform modules](tfmodules.md)