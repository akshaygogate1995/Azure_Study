# Azure_Study

## Azure Vnet

RFC 1918

IP address classes A, B, C, D, and E are part of the classful network architecture of IPv4, which was used to categorize IP addresses in different ranges based on the size of the network they were intended for:

Class A: Designed for very large networks, such as multinational corporations. The first octet starts with a 0, allowing for 128 networks (1.0.0.0 to 127.255.255.255), but only 126 are usable because 0.0.0.0 is reserved and 127.0.0.0 is used for loopback addresses1.

Class B: Intended for medium-sized networks, like universities or large businesses. The first octet starts with 10, ranging from 128.0.0.0 to 191.255.255.255, allowing for 16,384 networks1.

Class C: Used for small networks, such as small businesses or residential networks. The first octet starts with 110, covering the range 192.0.0.0 to 223.255.255.255, and supports 2,097,152 networks1.

Class D: Reserved for multicast groups and not used for standard network addresses. The first octet starts with 1110, ranging from 224.0.0.0 to 239.255.255.2551.

Class E: Reserved for experimental purposes, such as research and development. The first octet starts with 1111, spanning from 240.0.0.0 to 255.255.255.2551.

The reason why the ranges 172 and 192 are part of the private IP address space as defined in RFC 1918 is historical. When the Internet was in its early stages, the need for private IP addresses that could be used within organizations without being routed on the public Internet became apparent. The ranges 172.16.0.0 to 172.31.255.255 and 192.168.0.0 to 192.168.255.255 were chosen to be part of the private address space because they were sufficient to cover the needs of most organizations for internal addressing and were part of the Class B and Class C address ranges, respectively2. These addresses are non-routable on the public Internet, meaning they are not used outside of private networks, which helps to conserve the global pool of routable IP addresses. The 10.0.0.0 to 10.255.255.255 range was also designated for the same purpose and is part of the Class A address range2.

The selection of these specific ranges was likely due to their position within the overall IPv4 address space and their suitability for the scale of networks they were intended to serve. The 172 and 192 ranges fit well within the Class B and C structures, providing a good balance between the number of networks and the number of hosts within those networks.

To connect your on-premise network to Azure network you need VPN gateway or express route. Public IP is for connection with Internet.

Best Static IP scenarios -

1. DNS Name resolution - where a change in IP address would require updating host records.
   
2. Also good for IP address-based security models, which requires apps or services to have a static IP address.
   
3. SSL certificates are always linked to an IP address.
   
4. Firewall rules that allow or deny traffic based on IP address ranges.
   
5. Rule-based virtual machines such as domain controllers and DNS servers.
   
6. Best practice is dynamic assignment goes to a different subnet and static assignment goes to a different subnet.

IMP - Private IP address are assigned to Virtual Machines, Internal Load Balancer and Application Gateway and it supports both dynamic and static allocation. By default - Dynamic allocation is used in Azure Internally.

IMP - Public IP address are assigned to Virtual Machines, Internet facing Load Balancers, VPN Gateways and Application Gateways.You can use dynamic assignment of each of those but static assignment are not allowed on VPN Gateways and Application Gateways.

Few Commands -

1. Get-AzNetworkInterface   ---> Will list all network Cards (Get-AzNetworkInterface | select Name)

IMP - Service Endpoints are used to connect your virtual machines to platform as a service-based services in Azure.

Why use a service Endpoint?

1. Improved security for your azure service resources. Vnet's private address space can be overlapping, and so it cannot be used to uniquely identify traffic originating from your VNET. Service Endpoint provides the ability to secure Azure service resources to your virtual network by extending VNET identity to the service. Once service endpoints are enabled in your vnet, you can secure azure service resources to your vnet by adding a vnet rule to the resources.

2. Optimal routing.

3. Internal traffic routing.

4. Simple to setup.

 
