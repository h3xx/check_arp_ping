Nagios `check_arp_ping` plugin
==============================

This is basically the same thing as `check_ping`, except uses the ARP table to
"ping-by-MAC-address."

How it works is it'll scan your network using nmap(1) to refresh the ARP cache,
then send a ping to every IP address matching the MAC address you give it until
it finds one that responds.

Installation
------------

Log into your Nagios install and run this as root:

    curl -Ls https://github.com/h3xx/check_arp_ping/raw/main/check_arp_ping > /usr/local/nagios/libexec/check_arp_ping
    chmod +x /usr/local/nagios/libexec/check_arp_ping

Usage
-----

    check_arp_ping [OPTIONS] MAC_ADDR

Options
-------

    --help                  Show this help message.
    -n, --network NET       Use NET as the network IP range or netmask to scan to
                              populate ARP table. Example forms accepted:
                              - 192.168.0.0/24
                              - 192.168.0.[100-200]
                              - 192.168.*.*
                            (Default: 192.168.0.0/24)
    -d, --dont-scan         Don't scan the network at all, rely solely on the ARP
                              cache.
    -l, --lazy              Only scan the network if the MAC address isn't in the
                              ARP cache. Could lead to discrepancies.
    -w <wrta>,<wpl>%        -+
    -c <crta>,<cpl>%         | These options get passed to check_ping.
    [-p packets]             |
    [-t timeout]            -+

Example configuration in Nagios
-------------------------------

    $USER1$/check_arp_ping -n 192.168.23.0/24 -w $ARG1$,$ARG2$ -c $ARG3$,$ARG4$ -p 5 ab:cd:ef:ff:ff:ff

    - ARG1=3000.0
    - ARG2=80%
    - ARG3=5000.0
    - ARG4=100%
