# ssl-complete

SSL Complete Guide 2021: HTTP to HTTPS by Bogdan Stashchuk by Bogdan Stashchuk

SSL : Secure Sockets Layer

## details

<details>
  <summary>Click to Contract/Expend</summary>

### 7. Analyzing traffic using Wireshark

[install Wireshark](https://www.wireshark.org/)

Wireshark is a free and open-source packet analyzer.\
It is used for network troubleshooting, analysis, software and communications protocol development.

```sh
nslookup www.intagram.com

# Server:		192.168.8.1
# Address:	192.168.8.1#53

# Non-authoritative answer:
# www.intagram.com	canonical name = star.c10r.facebook.com.
# Name:	star.c10r.facebook.com
# Address: 157.240.8.18
```

But when I look up from chrome devtool, the IP is different.\
Chrome Devtool > Network > Doc > www.instagram.com > Headers \
\> Remote Address : 157.240.8.174:443

**Filtering on Wireshark**\
`ip.addr == 157.240.8.174`

### 8. TCP/IP stack by example

1. Click one of the packets
   1. Layer1 > TCP (Transmission Control Protocol)
      - Source Port : 61934 (Randomly chosen on my local)
      - Destination Port : 443
      - Flags: 0x002 (SYN) -> Flags: 0x012 (SYN, ACK) -> Flags: 0x010 (ACK)
   2. Layer2 > IP (Internet Protocal Version 4) : It has IP information
      - Source Address: 192.168.8.113
      - Destination Address: 157.240.8.174
   3. Ethernet II () : Hardware; my macaddress to destination router/network device
   4. Data (Frame 75) : Actual data

### 10. Analyzing HTTPS and TLS using Wireshark

TLS : Transport Layer Security

- TLSv1.2 Record Layer: Application Data Protocol: http-over-tls

</details>
