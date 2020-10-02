# VPNs and Firewalls

## VPN 

Each subscription has its own vpn back to the on-prem cisco firepower 

![inter-subscription-net](https://stdsoinventory0001.blob.core.windows.net/mdwikiimages/inter-subscription-net.png)


## internal control
North south traffic is controlled with several firewalls:  azure vnet peering, azure vpn / connections / the ash owned Perimeter firewall the ASA or Firepower (as we make the transition to the Firepower) and VMware NSX firewall that controls traffic in the datacenter.

![resource grouping](https://stdsoinventory0001.blob.core.windows.net/mdwikiimages/environmentfirewall.png)

