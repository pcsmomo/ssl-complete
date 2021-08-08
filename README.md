# ssl-complete

SSL Complete Guide 2021: HTTP to HTTPS by Bogdan Stashchuk by Bogdan Stashchuk

SSL : Secure Sockets Layer

## details

<details open>
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

### 20. RSA Overview

Key length

- 1024
- 2048 (Default)
- 3072
- 4096

private key and public key have the same length

### 25. Using OpenSSL for RSA keys generation

```sh
openssl

# Generate without encryption
OpenSSL> genrsa
# Generating RSA private key, 2048 bit long modulus
# .+++
# ..................................+++
# e is 65537 (0x10001)
# -----BEGIN RSA PRIVATE KEY-----
# MIIEowIBAAKCAQEAu8YXs5gvZwU763KHRUFeqlwPy9kYCemmKWs3dOV78t9sr0oh
# ...
# X1IrZoHJ4fnfZ3WmvpyK84Rt7+lvdBuqUPm0f9aAa+QAWOdMmZjh
# -----END RSA PRIVATE KEY-----
```

```sh
# Encrypt with AES-256
OpenSSL> genrsa -aes256
# Generating RSA private key, 2048 bit long modulus
# .....................................+++
# .............................................+++
# e is 65537 (0x10001)
# Enter pass phrase:
# Verifying - Enter pass phrase:
# -----BEGIN RSA PRIVATE KEY-----
# Proc-Type: 4,ENCRYPTED
# DEK-Info: AES-256-CBC,A1C663E683A49971C8A0C74FBD0BCF7B
#
# rvFOhjonpUReerrHK21PIyHThb762DtXMfWtx1FixJTYWjvZNcfhefcdli+25L+9
# ...
# 6f0YS3Dhj4HlYfxB2L7dMKwX97mxdWZhj+HgZhF3dngvriO0amlGHLu+7kfGSLFI
# -----END RSA PRIVATE KEY-----
```

```sh
# Encrypt with DES3
OpenSSL> genrsa -des3
# Generating RSA private key, 2048 bit long modulus
# ......................................................................+++
# ...............+++
# e is 65537 (0x10001)
# Enter pass phrase:
# Verifying - Enter pass phrase:
# -----BEGIN RSA PRIVATE KEY-----
# Proc-Type: 4,ENCRYPTED
# DEK-Info: DES-EDE3-CBC,5988E5B918179DC7
# -----END RSA PRIVATE KEY-----
```

```sh
# Save rsa to the file, private.pem
OpenSSL> genrsa -aes256 -out private.pem
# Generating RSA private key, 2048 bit long modulus
# .................+++
# .............................................................................................+++
# e is 65537 (0x10001)
# Enter pass phrase for private.pem:
# Verifying - Enter pass phrase for private.pem:
```

```sh
# The public key is encoded in the private key.
# Extract the public key from private.pem out to public.pem
OpenSSL> rsa -in private.pem -outform PEM -pubout -out public.pem
# Generating RSA private key, 2048 bit long modulus
# .................+++
# .............................................................................................+++
# e is 65537 (0x10001)
# Enter pass phrase for private.pem:
# Verifying - Enter pass phrase for private.pem:
```

```sh
# Generate RSA key length 4096
genrsa 4096
```

### 29. Root CA and root certificates in the OS

keychain access > System Roots > All certificated shipped on MacOS

### 30. How Chain of Trust is built

1. Root CA (Certificate Authority) : Selt-signed certificate
2. Intermediate CA : Signed by Root CA
3. End user : Signed by Intermediate CA

Signature : SHA hash with RSA Encryption

### 31. Verifying chain of certificates

1. Start with End user
   1. Check current date and time fall within the certificate validity interval
   2. Varification of the signature
      - Issuer Info in End user = Owner Info in Intermediate CA
2. Intermedicate CA
   1. Varification of the signature
      - Issuer Info in Intermediate CA = Owner Info in Root CA
3. Root CA
   1. Varification of the signature
      - Owner Info in Root CA within OS' keychain access

### 32. Verifying SSL certificate and certificates chain

[Geocerts SSL : SSL Checker](https://www.geocerts.com/ssl-checker)

Google Search : verify ssl certificate \
There are many websites where verify ssl certificates

</details>
