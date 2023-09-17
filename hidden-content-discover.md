Subdomain Enumeration

It's method to increase surface of attack by discovering subdomains of website. More subdomains = Bigger attack surface.

1) SSL/TLS Transparency Logs

"The purpose of Certificate Transparency logs is to stop malicious and accidentally made certificates from being used."

We can use this logs to discover belonging subdomains to the domain.

https://crt.sh
https://ui.ctsearch.entrust.com/ui/ctsearchui

2) Google Dorks Script

-site:www.website.com  site:*.website.com

We are excluding main domain, and including all founded subdomains in Google Search Engine.

3) DNS Bruteforce

We can try to find hidden subdomains using dsnrecon tool. This tool provides automating DNS threads to specific domain with common subdomain names.

dnsrecon -t brt -d website.com

We also have Sublist3r Tool
download: https://github.com/aboul3la/Sublist3r

./sublist3r.py -d acmeitsupport.thm

4) Virtual Hosts

Subdomains can be hosted on private servers, and they are not accessible by web.
DNS record could be kept on :
- private DNS server
- recorded on the developer's machines 
usually: 
Linux: /etc/hosts file 
Windows: c:\windows\system32\drivers\etc\hosts

these files are mapping domain names to IP addresses
 
We can get to them using HOST header fuzzing, to domain/IP address we specified.

FFUF:

ffuf -w common-subdomains.txt -H "Host: FUZZ.domain.com" -u http://MACHINE_IP

-w common-subdomains.txt -> text file with common subdomain names
-H "Host: FUZZ.domain.com" -> Host Header with FUZZ variable loaded from "common-subdomains.txt" file and target domain
-u http://MACHINE_IP -> IP machine of target domain
