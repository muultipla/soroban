{
   "date": "2020-05-01",
   "title": "Generating a trusted CA and server",
   "weight": 10,
   "image": "local-cert.jpg",
   "authors": [ "jdct" ],
   "branches": [ "tech" ],
   "tags": [ "dev", "ssl", "cert" ]
}

## 1) Setup & Configuration 
* linux: `cp /usr/lib/ssl/openssl.cnf prefix.cnf` (copy config file)
* macos: `cp /System/Library/OpenSSL/openssl.cnf prefix.cnf` (copy config file)
* edit file:

```ini
[ v3_ca ]
subjectKeyIdentifier=hash
authorityKeyIdentifier=keyid:always,issuer
basicConstraints = critical, CA:TRUE, pathlen:3
keyUsage = critical, cRLSign, keyCertSign
nsCertType = sslCA, emailCA

(...)

[ v3_req ]
basicConstraints = CA:FALSE
keyUsage = nonRepudiation, digitalSignature, keyEncipherment
subjectAltName = @alt_names

(...)

[ alt_names ]
DNS.1 = localhost
IP.1 = 127.0.0.1
```

* Uncomment next line 

```ini 
req_extensions = v3_req
```

## 2) Create CA files

```sh
jdct@muultipla ~ $ openssl genrsa -aes256 -out ca.key.pem 2048

jdct@muultipla ~ $ openssl req -new -x509 -extensions v3_ca -days 3650 -key ca.key.pem -sha256 -out ca.pem -config prefix.cnf

jdct@muultipla ~ $ openssl x509 -in ca.pem -text -noout
```

## 3) Create server files

```sh
jdct@muultipla ~ $ openssl genrsa -out server.key.pem 2048

jdct@muultipla ~ $ openssl req -extensions v3_req -sha256 -new -key server.key.pem -out server.csr -config prefix.cnf

jdct@muultipla ~ $ openssl x509 -req -extensions v3_req -days 3650 -sha256 -in server.csr -CA ca.pem -CAkey ca.key.pem -CAcreateserial -out server.crt -extfile prefix.cnf

jdct@muultipla ~ $ openssl x509 -in server.crt -text -noout
```
 
The server certificate is `server.crt` and the server private key is `server.key.pem`
