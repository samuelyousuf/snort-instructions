# Instructions

## Install Snort on Linux

* For Debian-based Linux distributions, type `sudo apt install snort`.
* Enter your password and then wait for installation to complete.  
**Note:** For other operating systems, download Snort from [Downloads](https://www.snort.org/downloads). Make sure you choose the correct file for your operating sytem.

## Create a rules file and logs directory

You can create a file that contains custom rules that Snort will use when it performs scans.

* In the Kali terminal, type touch `fullstack.rules` and then press enter.
* Type `mkdir logs` to create a directory.
* Type `nano fullstack.rules` to open the file for editing.
* In the file, type your rule(s):
    * `alert icmp any any -> any any (msg: "NMAP ping sweep Scan"; dsize:0;sid:10000004; rev: 1;)`
    * `alert tcp any any -> any 22 (msg: "NMAP TCP Scan";sid:10000005; rev:2; )`
    * `alert tcp any any -> any 22 (msg:"Nmap XMAS Tree Scan"; flags:FPU; sid:1000006; rev:1; )`
* Save and close the file.

## Start scan

* Open Wireshark and start a scan on the Eth0 port.
* In the metasploitable VM terminal, run the command `sudo nmap -A <ip-address of Kali VM>`. Wait for the scan to complete.
* When the scan completes, go to Wireshark and stop the scan. Save the scan results into a .pcap file.
* In the Kali terminal, type `snort -k none -l ./logs/ -c ./fullstack.rules -r ./<.pcap file>`. The results display in the terminal.
