# SSL Certs for Local Development

Having an SSL certificate for local development can have several benefits.
- Avoid browser console errors.
- Fetch fallback live media through correct protocol.
- Any requests to load assets from an HTTPS URL not getting blocked, etc.
- Match even closer to production environment to debug 1:1.

Suggestions:
- Save the cert where all other certs are stored. In VVV that would be `./certificates/localhost/`.
- Do not use the name `CA` for the certificate since VVV already has a `CA` named cert.

### Cert Generation
In a hurry? Generate cert using the following repo and it's instructions: https://github.com/dakshshah96/local-cert-generator

For a more in depth understanding, here is an article and the main commands to generate the cert:
https://www.freecodecamp.org/news/how-to-get-https-working-on-your-local-development-environment-in-5-minutes-7af615770eec/

```bash
openssl genrsa -des3 -out rootCA.key 2048
openssl req -x509 -new -nodes -key rootCA.key -sha256 -days 1024 -out dev.pem

openssl req -new -sha256 -nodes -out dev.csr -newkey rsa:2048 -keyout dev.key -config <( cat dev.csr.cnf )
openssl x509 -req -in dev.csr -CA dev.pem -CAkey rootCA.key -CAcreateserial -out dev.crt -days 3650 -sha256 -extfile openssl.conf
```

