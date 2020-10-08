{
   "date": "2020-09-17",
   "title": "Generar certificados locales para desarrollo",
   "slug": "generar-certificados-local",
   "weight": 10,
   "image": "local-cert.jpg",
   "authors": ["jdct"],
   "branches": [ "tech" ],
   "tags": [ "dev", "ssl", "cert" ]
}

## 1) Instalación y configuración 
* linux: 
`cp /usr/lib/ssl/openssl.cnf prefix.cnf` (copiar fichero de configuración)
* macos: `cp /System/Library/OpenSSL/openssl.cnf prefix.cnf` (copiar fichero de configuración)
* editar fichero:

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

* Descomentar la línea `req_extensions = v3_req`

## 2) Generar los ficheros de la Autoridad de Certificación (CA)

```sh
jdct@muultipla ~ $ openssl genrsa -aes256 -out ca.key.pem 2048

jdct@muultipla ~ $ openssl req -new -x509 -extensions v3_ca -days 3650 -key ca.key.pem -sha256 -out ca.pem -config prefix.cnf

jdct@muultipla ~ $ openssl x509 -in ca.pem -text -noout
```

## 3) Generar ficheros del servidor

```sh
jdct@muultipla ~ $ openssl genrsa -out server.key.pem 2048

jdct@muultipla ~ $ openssl req -extensions v3_req -sha256 -new -key server.key.pem -out server.csr -config prefix.cnf

jdct@muultipla ~ $ openssl x509 -req -extensions v3_req -days 3650 -sha256 -in server.csr -CA ca.pem -CAkey ca.key.pem -CAcreateserial -out server.crt -extfile prefix.cnf

jdct@muultipla ~ $ openssl x509 -in server.crt -text -noout
```
 
El certificado del servidor es `server.crt` and la clave privada del servidor `server.key.pem`
