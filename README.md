Nagios `check_arp_ping` plugin
==============================

This is basically the same thing as `check_ping`, except uses the ARP table to
"ping-by-MAC-address."

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
