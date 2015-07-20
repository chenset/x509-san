# frntn/x509-san

Generate a valid, self-signed, x509v3 certificate for multiple URLs / IPs

## Generate

The following command will generate (and overwrite if they already exists) two files:
 - pkcs#8 private key : `frntn-x509-san.key`
 - x509v3 certificate : `frntn-x509-san.crt`

```bash
curl -sSL https://raw.githubusercontent.com/frntn/x509-san/master/gencert.sh | CRT_CN="client.com" CRT_SAN="DNS.1:www.client.com,DNS.2:admin.client.com,IP.1:192.168.1.10,IP.2:10.0.0.234" bash
```

**=> Change the `CRT_CN` and `CRT_SAN` values to fit your needs**

## Check

You can check the certificate content by using the following standard `x509` command :

```bash
openssl x509 -in frntn-x509-san.crt -noout -text
```

## Secure the private key

The generated private key is passwordless by default. 

You can secure/unsecure using standard `pkcs8` commands :

```bash
# secure
openssl pkcs8 -in frntn-x509-san.key -topk8 -v2 des3 -out frntn-x509-san.secure.key

 unsecure
openssl pkcs8 -in frntn-x509-san.secure.key -topk8 -nocrypt -out frntn-x509-san.key
```
