# s3-ssl-certs
Ansible role to fetch SSL certificates and corresponding private keys (certificate bundles), which are stored in AWS S3 in single vault-encrypted YAML file, and deploy them on remote machines.

# Operation
Your host machine must have `boto` and `boto3` modules installed, for Ansible S3 module to work correctly.

# S3 stored YAML certificate bundle format
```yaml
---

cn: <common name>
timestamp: <unix timestamp>

private_key: |
  -----BEGIN RSA PRIVATE KEY-----
  <private key>
  -----END RSA PRIVATE KEY-----

certificate: |
  -----BEGIN CERTIFICATE-----
  <X.509 certificate>
  -----END CERTIFICATE-----

full_chain: |
  -----BEGIN CERTIFICATE-----
  <root CA>
  -----END CERTIFICATE-----
  -----BEGIN CERTIFICATE-----
  <intermediate CA>
  -----END CERTIFICATE-----

chain: |
  -----BEGIN CERTIFICATE-----
  <certificate chain>
  -----END CERTIFICATE-----

```
`cn`, `private_key` and `certificate` are mandatory. `timestamp`, `full-chain` and `chain` are optional. Order does not matter. Everything should be in ASCII PEM format. Mind spaces at beginning of new lines. `full_chain` will be stored in one file, order of certificates is up to you.

# Variables and configuration
`defaults/main.yml` is well documented. You probably want to override all values to satisfy your requirements.
