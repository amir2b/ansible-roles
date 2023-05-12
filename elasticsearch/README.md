## Setup

Install Elasticsearch and config it:

```bash
ansible-playbook run.yml --tags details
ansible-playbook run.yml

# ansible-playbook run.yml --tags new_server
# ansible-playbook run.yml --skip-tags new_server
```

Config backup by nfs service:

```bash
ansible-playbook run.yml --tags backup
```

Generate certs:

```bash
ansible-playbook run.yml --tags cert_generate --limit "elasticsearch[0]"
unzip files/certs.zip -d files/certs/

ansible-playbook run.yml --tags cert
```

Stop, start, restart:

```bash
ansible-playbook run.yml --tags stop
ansible-playbook run.yml --tags start
ansible-playbook run.yml --tags restart
```

Create auth mekanism:

```bash
ansible-playbook run.yml --tags auth --limit "elasticsearch[0]"
```

Upgrade

```bash
ansible-playbook upgrade.yml --tags details
# Disable elasticsearch allocation
ansible-playbook upgrade.yml --tags stop
ansible-playbook upgrade.yml --tags uninstall
ansible-playbook upgrade.yml
ansible-playbook upgrade.yml --tags upgrade
ansible-playbook upgrade.yml --tags backup
ansible-playbook upgrade.yml --tags cert
ansible-playbook upgrade.yml --tags restart
# Check elasticsearch nodes
# Enable elasticsearch allocation
```

## Curl

```bash
curl http://${USER}:${PASS}@${IP}:9200/_cat/nodes?v&pretty
curl http://${USER}:${PASS}@${IP}:9200/_cat/health?v&pretty

#curl -XPUT "http://${USER}:${PASS}@${IP}:9200/_cluster/settings" \
#    --header "Content-Type: application/json" \
#    --data '{ "persistent": { "cluster.routing.allocation.enable": null } }'
```

# Kibana

```bash
ansible-playbook kibana.yml --tags details
ansible-playbook kibana.yml

# ansible-playbook kibana.yml --tags new_server
# ansible-playbook kibana.yml --skip-tags new_server
```

Change kibana config:

> server.host

> elasticsearch.hosts

> elasticsearch.username

> elasticsearch.password
