# WDIAS K8s Setup

- https://github.com/kubernetes/ingress-nginx/blob/master/docs/deploy/index.md#docker-for-mac
- `wdias helm_install wdias-init`
- NGINX Prerequisites - https://kubernetes.github.io/ingress-nginx/examples/PREREQUISITES/
- Follow instructions here to genrate CA Key and Certificates
  - Better to use `rsa:4096`, instead of `rsa:2048`
  - Add subdomain support with `'*.wdias.com/CN=wdias.com'`
```sh
# Generate the CA Key and Certificate
$ openssl req -x509 -sha256 -newkey rsa:2048 -keyout ca.key -out ca.crt -days 356 -nodes -subj '/CN=Fern Cert Authority'

# Generate the Server Key, and Certificate and Sign with the CA Certificate
$ openssl req -new -newkey rsa:2048 -keyout server.key -out server.csr -nodes -subj '/CN=*.wdias.com'
$ openssl x509 -req -sha256 -days 365 -in server.csr -CA ca.crt -CAkey ca.key -set_serial 01 -out server.crt

# Generate the Client Key, and Certificate and Sign with the CA Certificate
$ openssl req -new -newkey rsa:2048 -keyout client.key -out client.csr -nodes -subj '/CN=Fern'
$ openssl x509 -req -sha256 -days 365 -in client.csr -CA ca.crt -CAkey ca.key -set_serial 02 -out client.crt
```
- [Create secrets manually](https://kubernetes.io/docs/concepts/configuration/secret/#creating-a-secret-manually) or [create secrets via kubectl](https://kubernetes.github.io/ingress-nginx/examples/auth/client-certs/#creating-certificate-secrets)
  - `kubectl create secret generic ca-secret --from-file=tls.crt=server.crt --from-file=tls.key=server.key --from-file=ca.crt=ca.crt
  - Create screts yaml with `cat server.crt | base64 && cat server.key | base64`

`openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout ${KEY_FILE} -out ${CERT_FILE} -subj "/CN=${HOST}/O=${HOST}"`
`kubectl create secret tls ${CERT_NAME} --key ${KEY_FILE} --cert ${CERT_FILE}`