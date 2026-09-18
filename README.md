# 🛡️ Week 2 - Footprinting & Network Scanning
## Table of content

- Engagement Brief

- Final report 

- Legal and ethical notice 

- Objective and scope 

- Arsenal- tools used

Activities performed 

PM1 # FOOTPRINTING & NETWORK SCANNING

## Overview
_______________________________
This covers footprinting the networkwalks.com domain using multiple Kali Linux tools and scanning my own local network with Zenmap . One module covers the footprinting phase and the other covers the scanning phase, so together they show how an attacker moves from gathering public information to mapping live hosts on a network. All commands were run in Kali Linux (footprinting) and on a Windows PC with Zenmap installed (scanning). Every step below includes the exact command used, the result I observed, and a short note on why the finding matters from an attacker's point of view.
--
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
🪜 # Tasks & Findings
-----
1. ### WHOIS Lookup
   
 whois networkwalks.com

   Domain Name: NETWORKWALKS.COM
   Registry Domain ID: 2452319255_DOMAIN_COM-VRSN
   Registrar WHOIS Server: whois.godaddy.com
   Registrar URL: http://www.godaddy.com
   Updated Date: 2025-11-12T10:08:43Z
   Creation Date: 2019-11-06T22:51:46Z
   Registry Expiry Date: 2027-11-06T22:51:46Z
   Registrar: GoDaddy.com, LLC
   Registrar IANA ID: 146
   Registrar Abuse Contact Email: abuse@godaddy.com
   Registrar Abuse Contact Phone: 480-624-2505
   Domain Status: clientDeleteProhibited https://icann.org/epp#clientDeleteProhibited
   Domain Status: clientRenewProhibited https://icann.org/epp#clientRenewProhibited
   Domain Status: clientTransferProhibited https://icann.org/epp#clientTransferProhibited
   Domain Status: clientUpdateProhibited https://icann.org/epp#clientUpdateProhibited
   Name Server: NS6135.HOSTGATOR.COM
   Name Server: NS6136.HOSTGATOR.COM
   DNSSEC: unsigned
   
2. ### WhatWeb Fingerprinting
   whatweb networkwalks.com
   
3. ### DNS Resolution check
   
   nslookup networkwalks.com
   
   Server:         8.8.8.8
   
   Address:        8.8.8.8#53

   Non-authoritative answer:

   Name:   networkwalks.com

   Address: 192.232.216.135

4. ### HTTP Header Inspection
   
curl -I https://networkwalks.com
HTTP/2 200 
permissions-policy: private-state-token-redemption=(self "https://www.google.com" "https://www.gstatic.com" "https://recaptcha.net" "https://challenges.cloudflare.com" "https://hcaptcha.com"), private-state-token-issuance=(self "https://www.google.com" "https://www.gstatic.com" "https://recaptcha.net" "https://challenges.cloudflare.com" "https://hcaptcha.com")
link: <https://networkwalks.com/wp-json/>; rel="https://api.w.org/", <https://networkwalks.com/wp-json/wp/v2/pages/53>; rel="alternate"; title="JSON"; type="application/json", <https://networkwalks.com/>; rel=shortlink
set-cookie: __wpdm_client=5865f3f3bc64e00b181f80f8de449cd4; path=/; domain=networkwalks.com; secure; HttpOnly
referrer-policy: no-referrer-when-downgrade
x-endurance-cache-level: 0
x-nginx-cache: WordPress
content-type: text/html; charset=UTF-8
date: Tue, 15 Sep 2026 11:52:33 GMT
server: Apache

5.### WAF Detection

wafw00f networkwalks.com

6. ###  Deep DNS Enumeration

dnsrecon -d networkwalks.com


2026-09-15T07:59:25.667024-0400 INFO Starting enumeration for domain: networkwalks.com

2026-09-15T07:59:25.667773-0400 INFO std: Performing General Enumeration against: networkwalks.com...

2026-09-15T07:59:27.167634-0400 ERROR No answer for DNSSEC query for networkwalks.com

2026-09-15T07:59:28.911819-0400 INFO     SOA ns6135.hostgator.com 50.87.144.87

2026-09-15T07:59:30.778349-0400 INFO     NS ns6135.hostgator.com 50.87.144.87

2026-09-15T07:59:31.785003-0400 INFO     Bind Version for 50.87.144.87 "9.16.23-RH"

2026-09-15T07:59:31.785674-0400 INFO     NS ns6136.hostgator.com 192.232.216.131

2026-09-15T07:59:32.820347-0400 INFO     Bind Version for 192.232.216.131 "9.16.23-RH"

2026-09-15T07:59:33.930787-0400 INFO     MX mail.networkwalks.com 192.232.216.135

2026-09-15T07:59:34.794759-0400 INFO     A networkwalks.com 192.232.216.135

2026-09-15T07:59:36.353510-0400 INFO     TXT networkwalks.com google-site-verification=rr04eRmqHoWY3XemnizDNVK4q75X-Ij-mjgEeg-UsYI

2026-09-15T07:59:36.354838-0400 INFO     TXT networkwalks.com v=spf1 +a +mx +ip4:50.87.144.87 +include:websitewelcome.com ~all

2026-09-15T07:59:37.426097-0400 INFO Enumerating SRV Records
__________________

## Tools Used
-----
whois (built-in)

WhatWeb

nslookup (built-in)

curl (built-in)

wafw00f

dnsrecon




