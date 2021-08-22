# Setup

Create playbook file `spark_yarn.yml`
```yaml
- name: Install hadoop on server
  hosts: hadoop
  roles:
    - spark_yarn
```

Execute it:
```bash
ansible-playbook spark_yarn.yml

## or
# ansible-playbook spark_yarn.yml --tags packages
# ansible-playbook spark_yarn.yml --tags config
```

Passwordless:
```sehll
ansible-playbook spark_yarn.yml --tags=ssh_generate --limit=master_nodes[0]
ansible-playbook run.yml --tags=ssh
```

Setup first time on master server:
```bash
hdfs namenode -format
start-dfs.sh
start-yarn.sh
hdfs dfs -mkdir /spark-logs
hdfs dfs -mkdir -p /user/spark/share/lib
hdfs dfs -put /opt/spark/jars/* /user/spark/share/lib
start-history-server.sh
```

# Start and stop

```bash
start-dfs.sh
start-yarn.sh
start-history-server.sh

stop-history-server.sh
stop-yarn.sh
stop-dfs.sh
```
