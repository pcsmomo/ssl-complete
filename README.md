# ssl-complete

SSL Complete Guide 2021: HTTP to HTTPS by Bogdan Stashchuk by Bogdan Stashchuk

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

</details>
