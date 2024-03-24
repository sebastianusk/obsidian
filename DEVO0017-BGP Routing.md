Broadcast Gateway Protocol is a way for routers to communicate with each other. Instead of each other needing to list out manually where the other IP addresses are, they just broadcast the routes that they own.

1. Practically, on each BGP, they have ASN, if you want private, use 64512 to 65535
2. After that list the BGP address that you want to be broadcasted
3. You can also set its weight
4. Then on the other end, just list out the IP address and it's BGP number (you can also add auth password for it)
5. The BGP protocol will automatically add the routing that's given by other BGP routers then considering its weight, will get the best route possible