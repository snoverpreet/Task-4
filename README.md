# Task-4
 
 **Setup and Use a Firewall on Windows/Linux**
 
In windows to open the firewall tool 
start+run > wf.msc this opens up the windows defender firewall where we can see inbound rules

LINUX (UFW) = 
**1) Install / enable UFW**
sudo apt update 
sudo apt install ufw

**2) Check Current Status**
sudo ufw status

**3) Important: allow SSH before enabling firewall (if remote)**
sudo ufw allow 22/tcp

sudo ufw status

**4) Add a rule to block inbound traffic on port 23 (Telnet)**

sudo ufw deny proto tcp from any to any port 23 comment 'Block Telnet - Test'

**5) Enable UFW (if not enabled)**
sudo ufw enable

**6) Test the rule** 
Created a listener on port 23 
sudo nc -l -p 23 > using ncat 

# Then from the same or another machine:
telnet <ip> 23

Interpretation:
> If blocked, telnet will hang or nc -vz reports connection refused / timed out depending on reject/drop.

> If allowed, you’ll connect to the listener and see any banner you printed.

**7) Remove the test block rule** 
sudo ufw delete deny proto tcp from any to any port 23

sudo ufw status numbered

**8) Export rules for deliverable (config files)**
UFW rule files are text and you can copy them:

/etc/ufw/user.rules (IPv4 rules)

/etc/ufw/user6.rules (IPv6 rules)
Use sudo cp /etc/ufw/user.rules ~/firewall_user.rules and include in deliverables

**How firewalls filter traffic?** 

A firewall sits between networks or on a host and looks at each packet or connection request. It compares packet attributes — source IP, destination IP, protocol (TCP/UDP), and port — against an ordered set of rules (allow/deny). If a packet matches a rule, the firewall takes that rule’s action (allow or block). Many modern firewalls are stateful, meaning they track connection states (new, established) so return traffic for allowed connections can pass automatically. Windows uses the Windows Filtering Platform to enforce rules at OS level; UFW is a friendly front-end to Linux’s netfilter/iptables/nftables packet filtering.
 
 
