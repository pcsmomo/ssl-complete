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

### 13. Symmetric Key Encryption Algorithms

AES (Advanced Encryption Standard) : Symmetric
RSA (Rivest–Shamir–Adleman) : Asymmetric

DES, 3DES : Obsolete

### 14. Hashing Overview

Bashing Algorithms : One way, cannot decrypt from hashed result

- MD5 (message-digest) : 128 bit
- SHA (Secure Hash Algorithm)
  - SHA-1 : 160 bit
  - SHA-256 : 256 bit
  - SHA-512 : 512 bit
- HMAC (keyed-hash message authentication code) : Can be used with MD5 and SHA

### 15. MD5 hashing algorithm

```sh
# MD5 : 126 bit = 4 bit(16, hexadecimal) * 32 characters
touch file.txt
md5 file.txt
# MD5 (file.txt) = d41d8cd98f00b204e9800998ecf8427e

# Add "Hello world" in the file.txt
open file.txt
md5 file.txt
# MD5 (file.txt) = 3e25960a79dbc69b674cd4ec67a72c62

# Hashed result is totally differents
```

[MD5 Hash Generator](https://passwordsgenerator.net/md5-hash-generator/)

Generate Hash with text "Hello world" \
-> 3e25960a79dbc69b674cd4ec67a72c62 (Exactly same)

> It generated based on content

### 16. SHA hashing algorithm and HMAC overview

```sh
# SHA-1 Hash: 160 bit
# 4 bit(16, hexadecimal) * 40 characters
# "Hello world"
shasum file.txt
7b502c3a1f48c8609ae212cdfb639dee39673f5e  file.txt

# SHA-256 : 256 bit
# 4 bit(16, hexadecimal) * 64 characters
# "Hello world"
shasum -a 256 file.txt
64ec88ca00b268e5ba1a35678a1b5316d212f4f366b2477232534a8aeca37f3c  file.txt

# SHA-512 : 512 bit
# 4 bit(16, hexadecimal) * 128 characters
# "Hello world"
shasum -a 512 file.txt
b7f783baed8297f0db917462184ff4f08e69c2d5e5f79a942600f9725f58ce1f29c18139bf80b06c0fff2bdd34738452ecf40c488c22a7e3d80cdf6f9c1c0d47  file.txt

# SHA-512 : 512 bit
# 4 bit(16, hexadecimal) * 128 characters
# "H" -> "h", "hello world"
open file.txt
shasum -a 512 file.txt
309ecc489c12d6eb4cc40f50c902f2b4d0ed77ee511a7c7a9bcd3ca86d4cd86f989dd35bc5ff499670da34255b45b0cfd830e81f605dcf7dc5542e93ae9cd76f  file.txt
```

</details>
