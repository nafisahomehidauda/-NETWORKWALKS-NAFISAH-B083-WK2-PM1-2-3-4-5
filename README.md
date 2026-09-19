# 🛡️ Week 2 - Footprinting, Reconnaissance and Network Scanning


# PM1- FOOTPRINTING & NETWORK SCANNING

## Overview
_______________________________
This covers footprinting the networkwalks.com domain using multiple Kali Linux tools and scanning my own local network with Zenmap . One module covers the footprinting phase and the other covers the scanning phase, so together they show how an attacker moves from gathering public information to mapping live hosts on a network. All commands were run in Kali Linux (footprinting) and on a Windows PC with Zenmap installed (scanning). 
---
🎯 # Objectives
____________________________________
Run WHOIS enumeration on the target domain

Fingerprint the web stack with WhatWeb

Confirm DNS resolution with nslookup

Inspect HTTP response headers with curl

Detect the presence of a WAF with wafw00f

Enumerate DNS records in depth with dnsrecon

Save output to file for later reference
_______________________________
🪜 # Tasks
----
### 1. WHOIS Lookup
   
 whois networkwalks.com

whois reveals the registrar, registration and expiry dates, and name servers. Here the name 
servers point to HostGator, so an attacker instantly learns the hosting provider. Registration dates 
and abuse contacts help with social engineering and planning.

    ### whatweb fingerprinting 
    
   whatweb networkwalks.com
   whatweb exposes the exact software and versions. An attacker looks these versions up in vulnerability databases to find known 
exploits. It also leaks the server IP and an email address.

 ### 3. DNS Resolution check
 
 nslookup turns a domain name into its real IP addresses Knowing the IP lets an 
attacker scan the server directly, look up other sites on the same IP, and map the target's 
infrastructure
   
   nslookup networkwalks.com

   Name:   networkwalks.com

   Address: 192.232.216.135
   
 ### 4. HTTP Header Inspection
   
HTTP headers leak the web server, caching stack and hidden endpoints Attackers read headers to fingerprint the stack and find entry points 
without even loading the full page.

curl -I https://networkwalks.com

### 5. WAF Detection

wafw00f tells an attacker if a firewall is watching. Here the site sits behind ModSecurity
(SpiderLabs). Knowing a WAF is present shapes the whole attack: naive attempts will be blocked 
or logged, so the attacker must adapt or try to bypass it.

wafw00f networkwalks.com

### 6. Deep DNS Enumeration

dnsrecon maps the target's entire DNS footprint: mail servers, DNS software version (Bind 
9.16.23), SPF policy and cPanel service records. Each record is a potential foothold and helps an 
attacker understand the email and hosting setup.

dnsrecon -d networkwalks.com
__________________

# PM3 - 






