# Scenario
1-# Using system DNS
dig example.com 
# Using 8.8.8.8
dig @8.8.8.8 example.com
2-  Using curl (best for HTTP/HTTPS)
# For HTTP (port 80)
curl -I http://example.com
# For HTTPS (port 443)
curl -I https://example.com
Using telnet
# HTTP
telnet example.com 80
# HTTPS
telnet example.com 443
Using nc (netcat) (better than telnet)
# HTTP
nc -zv example.com 80
# HTTPS
nc -zv example.com 443
 Using ss or netstat (to check local services, not remote)
ss example (modern tool):
ss -tuln | grep ':80\|:443'
netstat example (older tool):
netstat -tuln | grep ':80\|:443'
3-DNS-Level Issues
 Incorrect DNS records	internal.example.com points to the wrong IP address.
DNS cache poisoning or stale cache	Local resolver or system is caching outdated/wrong DNS data.
 DNS server unreachable	Client cannot reach DNS server listed in /etc/resolv.conf..
 Typos or wrong domain suffix	Misconfiguration (e.g., querying internal.exmaple.com instead of example.com).
 Firewall blocking DNS queries	UDP port 53 traffic blocked or dropped somewhere.
 Network-Level Issues
IP routing problems	Route to the server IP is missing or incorrect (especially in internal/private networks).
 Firewall blocking traffic	Firewall rules (network or host-based) block port 80/443 or ICMP (ping) traffic.
 NAT or IP address translation issues	If network address translation is wrong, packets never reach the correct destination.
 Proxy misconfiguration	Some internal services need an HTTP proxy, and direct access without proxy will fail.
Service/Application-Level Issues
 Web service only listening on localhost (127.0.0.1)	The service is running but not bound to the correct interface (0.0.0.0).
 Web service bound to wrong port	Service might be running on a non-standard port (not 80 or 443).
 Application-layer error (HTTP 5xx)	Service is up but broken internally, e.g., 503 Service Unavailable.
4- Confirm:
dig internal.example.com
Fix: Update the DNS record on your DNS server
If using bind:
sudo vim /etc/bind/db.example.com
# Correct the A record for internal.example.com
sudo systemctl reload bind9
IP routing problems
Confirm: Trace route to the server.
traceroute internal.example.com
Fix: Fix the route (usually a router configuration change).
Temporarily add route on Linux:
sudo ip route add <server_ip> via <gateway_ip>
 IP-based filtering on web server
Confirm: Review web server configs.
Fix: Allow your IP address in server configuration.
Example (nginx allow-listing):
allow your.ip.address.here;
deny all;
