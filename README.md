# letsencrypt-to-vault

## Description
Let's encrypt to Hashicorp Vault

Renew or get Let's Encrypt certificates and send it to Hashicorp Vault

## Usage
  letsencrypt-to-vault command [-flags] [sitesnames]

  Some flags can be set by env vars.
  Var names for this flags are in parens in flags description below
### Flags
      -a, --vaul-addr Address of vault server (VAULT_ADDR)
      -f, --certbot-flags Options that are passed to certbot. Overrides default (CERTBOT_FLAGS)
      -h, --help Show help
      -p, --vault-cert-path Path where certs will be stored (VAULT_CERT_PATH)
      -t, --vault-token Vault token (VAULT_TOKEN)

Default value for certbot-flags is: ```--webroot --webroot-path /webroot-dir --agree-tos --renew-by-default```.

### Docker

This dockerfile contains exposed volume */webroot-dir* for webroot plugin.
This means, that you can use it to share it to your **containerized proxy** by volumes_from.
If it's not containerized, just use ```-v``` flag to share it in place that you need(/usr/share/nginx/webroot for example).

Example:
```
docker run -ti -v /my/path/for-webroot:/webroot-dir ket4yii/letsencrypt-to-vault renew -t something-uuidgenerated -p secret/my/certs/certs -a http://vault.addr:8200
```
