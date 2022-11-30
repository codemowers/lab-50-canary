# Canary deployment

In this example Traefik v2.0 is configured using Traefik's custom resource
`IngressRoute` to send 75% of inbound HTTP requests to a production deployment and
remaining 25% to a canary deployment

Note that because `external-dns` is unaware of `IngressRoute` CRD,
it doesn't know how to add the CNAME record for the endpoint and
therefore `external-dns` custom resource `DNSEndpoint` is used to set up DNS.

To test run:

```
while [ 1 ]; do curl https://canary-laurivosandi.codemowers.ee; done
```

The output should more or less correspond to:

```
hello production
hello production
hello production
hello canary
hello production
hello production
hello production
hello canary
hello production
hello production
hello production
hello canary
``` 
