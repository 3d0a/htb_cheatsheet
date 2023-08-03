## basic nmap command
```bash
$ sudo nmap -sS -A -sV -Pn -p- --max-rate 5000 10.10.11.101

-sS (TCP SYN scan)
    SYN scan is the default and most popular scan option for good reasons. It can be performed quickly, scanning thousands of ports per second on a fast network not hampered by restrictive firewalls. It is also relatively unobtrusive and stealthy since it never completes TCP connections. SYN scan works against any compliant TCP stack rather than depending on idiosyncrasies of specific platforms as Nmap s FIN/NULL/Xmas, Maimon and idlescans do. It also allows clear, reliable differentiation between the open, closed, and filtered states.
This technique is often referred to as half-open scanning, because you dont open a full TCP connection. You send a SYN packet, as if you are going to open a real connection and then wait for a response. A SYN/ACKindicates the port is listening (open), while a RST (reset) is indicative of a non-listener. If no response is received after several retransmissions, the port is marked as filtered. The port is also marked filtered if an ICMP unreachable error (type 3, code 0, 1, 2, 3, 9, 10, or 13) is received. The port is also considered open if a SYN packet (without the ACK flag) is received in response. This can be due to an extremely rare TCP feature known as a simultaneous open or split handshake connection (see https://nmap.org/misc/split-handshake.pdf).

 -A option enables version detection among other things

-sV (Version detection)
    Enables version detection, as discussed above. Alternatively, you can use -A, which enables version detection among other things.

-PN (No ping) .
    This option skips the Nmap discovery stage altogether. Normally, Nmap uses this stage to determine
    active machines for heavier scanning. By default, Nmap only performs heavy probing such as port
    scans, version detection, or OS detection against hosts that are found to be up. Disabling host
    discovery with **-PN** causes Nmap to attempt the requested scanning functions against every target IP
    address specified. So if a class B sized target address space (/16) is specified on the command line,
    all 65,536 IP addresses are scanned. Proper host discovery is skipped as with the list scan, but
    instead of stopping and printing the target list, Nmap continues to perform requested functions as if
    each target IP is active. To skip ping scan and port scan, while still allowing NSE to run, use the
    two options  -PN  -sP together.
```

