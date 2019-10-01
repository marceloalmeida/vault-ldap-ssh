Vault LDAP SSH POC
============

```
export VAULT_ADDR='http://192.168.33.22:8200'
export VAULT_TOKEN='mysecrettoken'
```

```bash
vault login -method=ldap username=homer password=password
vault login -method=ldap username=ned password=password
vault login -method=ldap username=ralph password=password
```

```bash
vault write -field=signed_key ssh-client-signer/sign/simpson valid_principals=admins public_key=@$HOME/.ssh/id_ed25519.pub | tee $HOME/.ssh/id_ed25519-cert.pub
vault write -field=signed_key ssh-client-signer/sign/flanders valid_principals=developers public_key=@$HOME/.ssh/id_ed25519.pub | tee $HOME/.ssh/id_ed25519-cert.pub
```

```bash
ssh-keygen -Lf $HOME/.ssh/id_ed25519-cert.pub
```

```bash
ssh 192.168.33.23 -l admins -i ~/.ssh/id_ed25519 -i ~/.ssh/id_ed25519-cert.pub
ssh 192.168.33.23 -l developers -i ~/.ssh/id_ed25519 -i ~/.ssh/id_ed25519-cert.pub
```

# Sources
* https://hub.docker.com/r/nshou/elasticsearch-kibana/
* https://banzaicloud.com/blog/vault-dynamic-ssh/
* https://abridge2devnull.com/posts/2018/05/leveraging-hashicorp-vaults-ssh-secrets-engine/
* https://www.katacoda.com/hashicorp/scenarios/vault-policies
* https://github.com/hashicorp/vault/blob/master/website/source/docs/concepts/policies.html.md
* https://github.com/errygg/hashiconf-2018/blob/master/scripts/roles/zombies.json

# @ToDo
* Create index pattern on Kibana
* Wait/Retry CA creation on Vault
