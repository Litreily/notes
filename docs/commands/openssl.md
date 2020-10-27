# openssl

> OpenSSL is a robust, commercial-grade, and full-featured toolkit for the Transport Layer Security (TLS) and Secure Sockets Layer (SSL) protocols. It is also a general-purpose cryptography library.

## usage

openssl 是一个工具集，包含支持TLS，SSL协议的工具

```bash
$ openssl -h
openssl:Error: '-h' is an invalid command.

Standard commands
asn1parse      ca             ciphers        cms            crl
crl2pkcs7      dgst           dh             dhparam        dsa
dsaparam       ec             ecparam        enc            engine
errstr         gendh          gendsa         genpkey        genrsa
nseq           ocsp           passwd         pkcs12         pkcs7
pkcs8          pkey           pkeyparam      pkeyutl        prime
rand           req            rsa            rsautl         s_client
s_server       s_time         sess_id        smime          speed
spkac          srp            ts             verify         version
x509

Message Digest commands (see the `dgst` command for more details)
md4            md5            rmd160         sha            sha1

Cipher commands (see the `enc` command for more details)
aes-128-cbc    aes-128-ecb    aes-192-cbc    aes-192-ecb    aes-256-cbc
aes-256-ecb    base64         bf             bf-cbc         bf-cfb
bf-ecb         bf-ofb         cast           cast-cbc       cast5-cbc
cast5-cfb      cast5-ecb      cast5-ofb      des            des-cbc
des-cfb        des-ecb        des-ede        des-ede-cbc    des-ede-cfb
des-ede-ofb    des-ede3       des-ede3-cbc   des-ede3-cfb   des-ede3-ofb
des-ofb        des3           desx           rc2            rc2-40-cbc
rc2-64-cbc     rc2-cbc        rc2-cfb        rc2-ecb        rc2-ofb
rc4            rc4-40         seed           seed-cbc       seed-cfb
seed-ecb       seed-ofb       zlib
```

## openssl s_client

`s_client`, `s_server` 主要用来测试openssl握手的套件是否可用，是否能正常完成密钥协商，以`s_client`为例。

```bash
openssl s_client -connect serverip:port
openssl s_client -connect serverip:port -CApath /etc/ssl/certs/
```

正常情况下

```bash
$ openssl s_client -connect 52.48.74.182:443
CONNECTED(00000003)
depth=4 C = US, O = "Starfield Technologies, Inc.", OU = Starfield Class 2 Certification Authority
verify return:1
depth=3 C = US, ST = Arizona, L = Scottsdale, O = "Starfield Technologies, Inc.", CN = Starfield Services Root Certificate Authority - G2
verify return:1
depth=2 C = US, O = Amazon, CN = Amazon Root CA 1
verify return:1
depth=1 C = US, O = Amazon, OU = Server CA 1B, CN = Amazon
verify return:1
depth=0 CN = devicelocation.ngxcld.com
verify return:1
---
Certificate chain
 0 s:/CN=devicelocation.ngxcld.com
   i:/C=US/O=Amazon/OU=Server CA 1B/CN=Amazon
 1 s:/C=US/O=Amazon/OU=Server CA 1B/CN=Amazon
   i:/C=US/O=Amazon/CN=Amazon Root CA 1
 2 s:/C=US/O=Amazon/CN=Amazon Root CA 1
   i:/C=US/ST=Arizona/L=Scottsdale/O=Starfield Technologies, Inc./CN=Starfield Services Root Certificate Authority - G2
 3 s:/C=US/ST=Arizona/L=Scottsdale/O=Starfield Technologies, Inc./CN=Starfield Services Root Certificate Authority - G2
   i:/C=US/O=Starfield Technologies, Inc./OU=Starfield Class 2 Certification Authority
---
Server certificate
-----BEGIN CERTIFICATE-----
MIIFezCCBGOgAwIBAgIQD2G5WRjlpBXraGmoG0C50TANBgkqhkiG9w0BAQsFADBG
MQswCQYDVQQGEwJVUzEPMA0GA1UEChMGQW1hem9uMRUwEwYDVQQLEwxTZXJ2ZXIg
Q0EgMUIxDzANBgNVBAMTBkFtYXpvbjAeFw0yMDA4MjgwMDAwMDBaFw0yMTA5Mjcx
MjAwMDBaMCQxIjAgBgNVBAMTGWRldmljZWxvY2F0aW9uLm5neGNsZC5jb20wggEi
MA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCZw+BtpGv+SopXdXVjxvRJb1It
3MqlCXyFp+lRxuM9ySLT0IFCMqhBadzJCIB32VZP4ixQ0WjqGDjwcXVau2ka0SDN
e+xjhYzc6FKzgRmIy016sBQiadasadAZbbcJeRTNrhjD0PqjCE7DbKmQWx8SEoY0
Nm1fnq/TPwBIKqo1vdS2e6CiXcfH5LTBLLE4Ryw9aloWDQ2nud/x8lRMlY+0Gird
X1abENX9++gpoS/TUQ2uXxbFKDPb/Moi/3hirivQiVi1R9CjEYYcmlSr+XctUjk/
VgzqwgUukC15YABvfxCjZRHyNQ85SJ2vDtDhxMfQfhZHqcUozkQPqw28SUVhAgMB
AAGjggKFMIICgTAfBgNVHSMEGDAWgBRZpGYGUqB7lZI8o5QHJ5Z0W/k90DAdBgNV
HQ4EFgQUtbIEC2lD6lx/E0fmPY/OICyl9HQwJAYDVR0RBB0wG4IZZGV2aWNlbG9j
YXRpb24ubmd4Y2xkLmNvbTAOBgNVHQ8BAf8EBAMCBaAwHQYDVR0lBBYwFAYIKwYB
BQUHAwEGCCsGAQUFBwMCMDsGA1UdHwQ0MDIwMKAuoCyGKmh0dHA6Ly9jcmwuc2Nh
MWIuYW1hem9udHJ1c3QuY29tL3NjYTFiLmNybDAgBgNVHSAEGTAXMAsGCWCGSAGG
/WwBAjAIBgZngQwBAgEwdQYIKwYBBQUHAQEEaTBnMC0GCCsGAQUFBzABhiFodHRw
Oi8vb2NzcC5zY2ExYi5hbWF6b250cnVzdC5jb20wNgYIKwYBBQUHMAKGKmh0dHA6
Ly9jcnQuc2NhMWIuYW1hem9udHJ1c3QuY29tL3NjYTFiLmNydDAMBgNVHRMBAf8E
AjAAMIIBBAYKKwYBBAHWeQIEAgSB9QSB8gDwAHYA9lyUL9F3MCIUVBgIMJRWjuNN
Exkzv98MLyALzE7xZOMAAAF0Moj6QwAABAMARzBFAiArdrj+FzgNhO3UOShNAThI
dUxRgP21OgRiZCsOv3UZDwIhAJFyF0BC4kYsJqJFkc+n/ZMmmVrrAG4WPIfGqwq/
nqc+AHYAXNxDkv7mq0VEsV6a1FbmEDf71fpH3KFzlLJe5vbHDsoAAAF0Moj6PQAA
BAMARzBFAiEA+twofyIX7Z2fSqY3OJsHzw2c39o3oBVkwuthnGmsIegCIHNCLMBY
lrkWX0V9j+7Pi+NHe57Bj2+IgWqlw/CHeM5OMA0GCSqGSIb3DQEBCwUAA4IBAQAf
2CtL8DliTB9Inf1+ZKTg6JjCebH4iH61gSfqxJZyDgW+7umFQguL+hEpdDUd6tcq
Uj9ibAxtcdOLSbIjJKwC1cN+gcgSHYbPBD2mQU4U7wPhfFSZRDBoFBH4n13OkgT+
f2tO/byQ7uchJvnezVhjYdJwZoBpPi6IXpzqE5A6IH9AJz0iQJLUyyC1b8fQNiFQ
5j65t5FrLqf9LU82hrDrPLjEvR9v6BAumlH/0FmaIbXPwZm6kMXmTqRoPzX0+R5W
M8bUGEDnkWMwzj+1eW64hpu8Fwsq17SAeITVclj2ZNjz2LaNyuLbdKkMatnLq1M6
2sq4dgrQ1Jx90PGLzAbi
-----END CERTIFICATE-----
subject=/CN=devicelocation.ngxcld.com
issuer=/C=US/O=Amazon/OU=Server CA 1B/CN=Amazon
---
No client certificate CA names sent
Peer signing digest: SHA512
Server Temp Key: ECDH, P-256, 256 bits
---
SSL handshake has read 5506 bytes and written 400 bytes
---
New, TLSv1/SSLv3, Cipher is ECDHE-RSA-AES128-GCM-SHA256
Server public key is 2048 bit
Secure Renegotiation IS supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
SSL-Session:
    Protocol  : TLSv1.2
    Cipher    : ECDHE-RSA-AES128-GCM-SHA256
    Session-ID: EFA5500D91F4403CA0D2003B98F790B238F68D34E4A9D1F7CB6E382B1C762588
    Session-ID-ctx:
    Master-Key: 8CEE4FCFC53AA6CB66F915D5C0911D28F59D30477EEDDA1E2A5E6C0DEE3FE24F8CC7918EF85717D34BC675F83F1BB892
    Key-Arg   : None
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 43200 (seconds)
    TLS session ticket:
    0000 - c3 33 dc 6e 4b 4c 35 4f-3a 84 49 5d 7f 4a 12 30   .3.nKL5O:.I].J.0
    0010 - cb be 29 f6 6c 04 78 61-19 48 9a ba e8 b8 21 31   ..).l.xa.H....!1
    0020 - 56 52 ab d0 16 eb 56 6f-b6 8c 00 42 f6 14 cd 49   VR....Vo...B...I
    0030 - b4 a1 09 5b 0e ea 11 1c-0c 85 61 4d 9b b3 75 49   ...[......aM..uI
    0040 - 80 d5 ab da c8 2d 07 4c-c0 dc 9a dc 9c 4d 66 87   .....-.L.....Mf.
    0050 - b3 8c 72 f4 c3 75 9a cf-76 46 75 35 81 54 48 ad   ..r..u..vFu5.TH.
    0060 - 71 16 db 55 12 61 fe da-87 1a bc eb 43 83 2d 75   q..U.a......C.-u
    0070 - 6a 6d 97 4a de 09 e1 b2-5c 18 2e af ac a0 a1 7a   jm.J....\......z
    0080 - b8 e9 3f 83 65 5e 3e da-db 4f 1d fd 94 b6 66 e1   ..?.e^>..O....f.
    0090 - 74 73 3b 09 93 83 2f 23-7f 13 98 8c 63 3b 13 6b   ts;.../#....c;.k
    00a0 - 03 07 0f d2 b2 66 37 df-92 e7 c9 c1 7b da 26 67   .....f7.....{.&g

    Start Time: 1600248002
    Timeout   : 300 (sec)
    Verify return code: 0 (ok)
---
```

可以看到正常情况下，verify return code是0，代表一切正常。

异常情况下，如果证书认证失败，会返回`verify error`，比如下面的高亮部分，提示证书无效。这种情况出现的原因是当前时间不在server提供的证书有效期范围内，有可能是本地时间未更新，或者server端证书配置有误。

```bash hl_lines="12"
$ openssl s_client -connect 52.48.74.182:443
CONNECTED(00000003)
depth=4 C = US, O = "Starfield Technologies, Inc.", OU = Starfield Class 2 Certification Authority
verify return:1
depth=3 C = US, ST = Arizona, L = Scottsdale, O = "Starfield Technologies, Inc.", CN = Starfield Services Root Certificate Authority - G2
verify return:1
depth=2 C = US, O = Amazon, CN = Amazon Root CA 1
verify return:1
depth=1 C = US, O = Amazon, OU = Server CA 1B, CN = Amazon
verify return:1
depth=0 CN = devicelocation.ngxcld.com
verify error:num=9:certificate is not yet valid
notBefore=Aug 28 00:00:00 2020 GMT
verify return:1
depth=0 CN = devicelocation.ngxcld.com
notBefore=Aug 28 00:00:00 2020 GMT
verify return:1
---
Certificate chain
 0 s:/CN=devicelocation.ngxcld.com
   i:/C=US/O=Amazon/OU=Server CA 1B/CN=Amazon
 1 s:/C=US/O=Amazon/OU=Server CA 1B/CN=Amazon
   i:/C=US/O=Amazon/CN=Amazon Root CA 1
 2 s:/C=US/O=Amazon/CN=Amazon Root CA 1
   i:/C=US/ST=Arizona/L=Scottsdale/O=Starfield Technologies, Inc./CN=Starfield Services Root Certificate Authority - G2
 3 s:/C=US/ST=Arizona/L=Scottsdale/O=Starfield Technologies, Inc./CN=Starfield Services Root Certificate Authority - G2
   i:/C=US/O=Starfield Technologies, Inc./OU=Starfield Class 2 Certification Authority
---
Server certificate
-----BEGIN CERTIFICATE-----
MIIFezCCBGOgAwIBAgIQD2G5WRjlpBXraGmoG0C50TANBgkqhkiG9w0BAQsFADBG
MQswCQYDVQQGEwJVUzEPMA0GA1UEChMGQW1hem9uMRUwEwYDVQQLEwxTZXJ2ZXIg
Q0EgMUIxDzANBgNVBAMTBkFtYXpvbjAeFw0yMDA4MjgwMDAwMDBaFw0yMTA5Mjcx
MjAwMDBaMCQxIjAgBgNVBAMTGWRldmljZWxvY2F0aW9uLm5neGNsZC5jb20wggEi
MA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCZw+BtpGv+SopXdXVjxvRJb1It
3MqlCXyFp+lRxuM9ySLT0IFCMqhBadzJCIB32VZP4ixQ0WjqGDjwcXVau2ka0SDN
e+xjhYzc6FKzgRmIy016sBQiadasadAZbbcJeRTNrhjD0PqjCE7DbKmQWx8SEoY0
Nm1fnq/TPwBIKqo1vdS2e6CiXcfH5LTBLLE4Ryw9aloWDQ2nud/x8lRMlY+0Gird
X1abENX9++gpoS/TUQ2uXxbFKDPb/Moi/3hirivQiVi1R9CjEYYcmlSr+XctUjk/
VgzqwgUukC15YABvfxCjZRHyNQ85SJ2vDtDhxMfQfhZHqcUozkQPqw28SUVhAgMB
AAGjggKFMIICgTAfBgNVHSMEGDAWgBRZpGYGUqB7lZI8o5QHJ5Z0W/k90DAdBgNV
HQ4EFgQUtbIEC2lD6lx/E0fmPY/OICyl9HQwJAYDVR0RBB0wG4IZZGV2aWNlbG9j
YXRpb24ubmd4Y2xkLmNvbTAOBgNVHQ8BAf8EBAMCBaAwHQYDVR0lBBYwFAYIKwYB
BQUHAwEGCCsGAQUFBwMCMDsGA1UdHwQ0MDIwMKAuoCyGKmh0dHA6Ly9jcmwuc2Nh
MWIuYW1hem9udHJ1c3QuY29tL3NjYTFiLmNybDAgBgNVHSAEGTAXMAsGCWCGSAGG
/WwBAjAIBgZngQwBAgEwdQYIKwYBBQUHAQEEaTBnMC0GCCsGAQUFBzABhiFodHRw
Oi8vb2NzcC5zY2ExYi5hbWF6b250cnVzdC5jb20wNgYIKwYBBQUHMAKGKmh0dHA6
Ly9jcnQuc2NhMWIuYW1hem9udHJ1c3QuY29tL3NjYTFiLmNydDAMBgNVHRMBAf8E
AjAAMIIBBAYKKwYBBAHWeQIEAgSB9QSB8gDwAHYA9lyUL9F3MCIUVBgIMJRWjuNN
Exkzv98MLyALzE7xZOMAAAF0Moj6QwAABAMARzBFAiArdrj+FzgNhO3UOShNAThI
dUxRgP21OgRiZCsOv3UZDwIhAJFyF0BC4kYsJqJFkc+n/ZMmmVrrAG4WPIfGqwq/
nqc+AHYAXNxDkv7mq0VEsV6a1FbmEDf71fpH3KFzlLJe5vbHDsoAAAF0Moj6PQAA
BAMARzBFAiEA+twofyIX7Z2fSqY3OJsHzw2c39o3oBVkwuthnGmsIegCIHNCLMBY
lrkWX0V9j+7Pi+NHe57Bj2+IgWqlw/CHeM5OMA0GCSqGSIb3DQEBCwUAA4IBAQAf
2CtL8DliTB9Inf1+ZKTg6JjCebH4iH61gSfqxJZyDgW+7umFQguL+hEpdDUd6tcq
Uj9ibAxtcdOLSbIjJKwC1cN+gcgSHYbPBD2mQU4U7wPhfFSZRDBoFBH4n13OkgT+
f2tO/byQ7uchJvnezVhjYdJwZoBpPi6IXpzqE5A6IH9AJz0iQJLUyyC1b8fQNiFQ
5j65t5FrLqf9LU82hrDrPLjEvR9v6BAumlH/0FmaIbXPwZm6kMXmTqRoPzX0+R5W
M8bUGEDnkWMwzj+1eW64hpu8Fwsq17SAeITVclj2ZNjz2LaNyuLbdKkMatnLq1M6
2sq4dgrQ1Jx90PGLzAbi
-----END CERTIFICATE-----
subject=/CN=devicelocation.ngxcld.com
issuer=/C=US/O=Amazon/OU=Server CA 1B/CN=Amazon
---
No client certificate CA names sent
Peer signing digest: SHA512
Server Temp Key: ECDH, P-256, 256 bits
---
SSL handshake has read 5506 bytes and written 400 bytes
---
New, TLSv1/SSLv3, Cipher is ECDHE-RSA-AES128-GCM-SHA256
Server public key is 2048 bit
Secure Renegotiation IS supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
SSL-Session:
    Protocol  : TLSv1.2
    Cipher    : ECDHE-RSA-AES128-GCM-SHA256
    Session-ID: 979E3C71B293EDF1923989B706B0B315A638046A30DA9E6B77C8889DF94BC613
    Session-ID-ctx:
    Master-Key: 24F7FD66C5A195765C62FE5B8D5304F94F3006A1A2993B7C3FB5B1D9162A9E5BFD6CADC984458153E32F012AD30A3F7A
    Key-Arg   : None
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 43200 (seconds)
    TLS session ticket:
    0000 - c3 33 dc 6e 4b 4c 35 4f-3a 84 49 5d 7f 4a 12 30   .3.nKL5O:.I].J.0
    0010 - be c3 28 c9 3a fd 73 6a-c7 65 65 b0 a7 69 a1 ca   ..(.:.sj.ee..i..
    0020 - f8 89 1d 62 75 3d 46 7d-92 62 01 f6 8b fa 40 c7   ...bu=F}.b....@.
    0030 - ef de 3b 35 50 ab 0c 45-79 ce 97 2f 13 9e 0c 10   ..;5P..Ey../....
    0040 - 4c d2 2a 4e 85 fc 8f b1-4c c9 98 1a 0d 39 a9 26   L.*N....L....9.&
    0050 - e3 c3 18 16 fc ad b9 9a-ba 5d f7 b1 db 70 ab 30   .........]...p.0
    0060 - 04 b3 9a 2f 66 97 74 e6-74 c9 04 59 3b 18 df 67   .../f.t.t..Y;..g
    0070 - a3 17 03 52 c8 c9 b9 8c-1f 11 01 8e cf bc 17 22   ...R..........."
    0080 - e7 7d 40 ad 53 c6 04 83-d2 80 24 28 3f cb f8 c6   .}@.S.....$(?...
    0090 - c4 1c 2f 42 15 7b a3 13-c7 4f 8f 62 18 71 0f 2a   ../B.{...O.b.q.*
    00a0 - 90 8b 8b d9 64 b8 1e 0d-cf df 62 cc fc 95 d0 ce   ....d.....b.....

    Start Time: 1598327363
    Timeout   : 300 (sec)
    Verify return code: 9 (certificate is not yet valid)
---
```
