# cisco-router-auditing
A small list of security controls that can be used to audit configuration on Cisco routers manually.   

## Passwords
Confirm that we do not use type7 for password encryption - Use type5 or type8  
Set min length using 'security password min-length 8'  (User – 8, Admin – 12, Service - 15)  
Remove type7 manually - Cisco's allow the same password to be added with both type 7 and type5  

## Management
Confirm SSH v2.0 or higher is being used rather than telnet  
Confirm that SSH Timeout has been configured  
Authentication retries – no. of retries before login     
Configure SSH on VTYs - 'transport input ssh' , Note that 'login local' on VTY will skip AAA  

## Logging
Set the appropriate time zone   
Set logging and debug with local time    
Log level information needs to be set appropriately    
Increase local log buffer size    
Are configuration changes being logged?  

## VTY ACL's
Set VTY IP access list permit with whitelisted IP subnets    
Apply outbound access list   
If OOB NW is used, use 'vty in vrf-also' for mgmt VRF    

## SNMP
Use SNMPv3    
Set SNMP groups (for read and write, different areas of the MIB) with users with different privileges   
Add access-list with IP whitelists for SNMPv3 access   

## Secure NTP  
Secure against amplification attacks    
Set NTP authentication key with type 5 md5    

## SCP
Enable SCP instead of TFTP or FTP  
Cisco dev can also act as SCP server, can be configured with AAA   

## IOS Hardening
Disable unused services  
Disable Interface IP Options - Proxy-ARP, IP Redirects and IP Unreachables  
Routing update auth (OSPF auth) needs to be used with MD5 to prevent route poisoning  

## Control Plane 
Prevent DDoS attacks with CoPP (Control Plane Policing)  
Policy Map should be applied for Control Plane - Access-list can be created to allow/deny icmp.tcp.udp and a policy map created to block this access-list  

## STP (Spanning Tree Protocol)
STPs BPDU should not be seen by end-user devices connected to edge port. In which case BPDU guards must be used (Bridge port data unit) (port shutdown)   
Root guard can be configured in a similar way to block the VLAN (blocking state)   
Loop guard can also be used    

## CAM Table overload 
Port security needs to be configured to allow only a limited number of mac addresses to be connected on the port (especially edge ports).    
Generally only one MAC address allowed per port. Automatically disables port if more devices are connected   
