Create playbook file `spark_yarn.yml`
```yaml
---

- name: Install hadoop on server
  hosts: hadoop
  roles:
    - spark_yarn
```

Execute it:
```shell
ansible-playbook spark_yarn.yml
```

Or execute separated
```shell
ansible-playbook spark_yarn.yml --tags packages
ansible-playbook spark_yarn.yml --tags config
```

Passwordless: Copy public key from master server to worker servers
```sehll
ssh-copy-id remote_username@server_ip_address
```

Passwordless: Copy public key from master server to yourself
```sehll
cp id_rsa.pub authorized_keys
chmod 0600 authorized_keys
```

Setup first time os master server
```shell
hdfs namenode -format
start-dfs.sh
start-yarn.sh
hdfs dfs -mkdir /spark-logs
hdfs dfs -mkdir -p /user/spark/share/lib
hdfs dfs -put /opt/spark/jars/* /user/spark/share/lib
start-history-server.sh
```