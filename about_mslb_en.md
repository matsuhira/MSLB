# About MSLB
## What is MSLB
MSLB is an abbreviation for Multi-Stage Transparent Server Load Balancing, which is a protocol-independent load balancing technology.<br>

One of the existing well-known load balancing technologies is a method realized by rewriting the destination address of an IP packet.<br>
NAT and NAPT are well-known technologies for rewriting the address of the IP header, but it is well known that these technologies have the problem of dealing with applications that carry the IP address in the data section. increase. Load balancing technology, which rewrites the destination address, has similar issues. Since NAT rewrites the source address, the target to be rewritten is different, but it is the same in that the IP address is rewritten.<br>

MSLB aims to eliminate such application dependencies and achieve general-purpose load balancing. Of course, it supports IPv4 / IPv6 with the same mechanism.<br>

## How MSLB works
MSLB solves the above problems by processing them in multiple stages.<br>

In the first stage, the destination address is translated as before. In MSLB, the final stage is provided, and the rewritten destination address is rewritten to the address before rewriting. The packet is then passed to the server, which is exactly the same packet that the first stage received. As a result, there is no inconsistency between the IP address information in the IP header and the IP address information contained in the data part. Neither the client nor the server can see the existence of the load balancer.<br>

## MSLB configuration
With the existing load balancing technology, it is necessary to rewrite the source address for the returned IP packet. As a result, all IP packets destined for the server and all returning packets must pass through this load balancer, and the performance of this load balancer becomes a performance bottleneck.<br>

MSLB can realize the first stage processing with one arm. With such a configuration, the reply from the server to the client does not need to pass through the first stage device. As a result, performance bottlenecks are alleviated.<br>
