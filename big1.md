## Summary

![inter-subscription-map](https://stdsoinventory0001.blob.core.windows.net/mdwikiimages/inter-subscription-map.png)

## 3 subscriptions 1 tenant

The 10k foot view is architected to have 3 subscriptions (Research and Development, Non Production, and Production) each with seperate VPN tunnels to the Corporate datacenter, all three are initally set to 3gig but there is capacity to increase production up to 10 gig if needed in the future. Resources will be group logicaly by application and environment to allow for security measures to deny inter-environment traffic. 

## Research and Development
[subscription details](rnd1.md)
## Non Production
[subscription details](nonprod1.md)
## Production
[subscription details](prod1.md)