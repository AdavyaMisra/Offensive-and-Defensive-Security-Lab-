Experiment 4: Firewall and IDS Setup Using pfSense and Snort
Aim
To configure pfSense as a firewall and Snort as an IDS in a VMware lab, then generate and inspect network traffic with Nmap.

Requirements and topology
VMware Workstation/Player, pfSense, Kali Linux, and Metasploitable
pfSense WAN connected to NAT (VMnet8)
pfSense LAN, Kali, and Metasploitable connected to private VMnet1
Device/interface	Address	Network / role
pfSense WAN	DHCP	NAT (VMnet8)
pfSense LAN (em1)	192.168.1.1/24	VMnet1 gateway
Kali Linux	192.168.1.101/24	VMnet1 scanner
Metasploitable	192.168.1.100/24	VMnet1 test target
Procedure
Connect the VMs to the networks shown above. Configure the pfSense LAN as 192.168.1.1/24, Kali as 192.168.1.101/24, and Metasploitable as 192.168.1.100/24. Use pfSense as the LAN gateway.

In Firewall → Rules → LAN, allow the required services: DNS on TCP/UDP 53, HTTP on TCP 80, and HTTPS on TCP 443. Scope rules to the lab hosts and place them before a block rule for other unnecessary traffic. Review existing rules and their order before applying changes.

Install Snort from System → Package Manager → Available Packages.

Under Services → Snort → Snort Interfaces, add the LAN interface (em1) for monitoring and apply the configuration.

Enable and update the GPLv2 Community Rules. Enable the relevant rules for the LAN interface and apply the settings.

From Kali, generate traffic to Metasploitable with Nmap:

nmap -sV 192.168.1.100
Check Services → Snort → Alerts and compare alert timestamps with the scan. If no alert appears, check that Snort is running, the LAN interface is enabled, and the rules are active. A packet capture can confirm that traffic reached the interface, but does not itself confirm a Snort alert.

Result
The experiment was completed using the stated VMware topology and IP addresses. The lab covered pfSense LAN firewall rules, Snort installation and LAN monitoring, GPLv2 Community Rules, Nmap traffic generation, and alert review. The setup provided practice using a firewall and IDS in an isolated virtual lab.
