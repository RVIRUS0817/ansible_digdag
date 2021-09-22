# ansible_digdag

![スクリーンショット 2020-12-09 20 28 32](https://user-images.githubusercontent.com/5633085/101624459-49d50980-3a5d-11eb-874f-780ea593e1b0.jpg)


## Environment

- Amazon linux2
- RDS(PostgreSQL 12)
- Java v1.8.0_265
- Digdag v0.9.42
- Embulk v0.9.23

## dry-run

```
$ ansible-playbook -i hosts prd.yml -C
```

## run

```
$ ansible-playbook -i hosts prd.yml 
```

## Make DB

```
$ psql -h digdag.xxxxxxxx.xxxxxxx.rds.amazonaws.com -U root -d digdag_db
 
CREATE ROLE digdag WITH PASSWORD 'xxxxxxxx' NOSUPERUSER NOCREATEDB NOCREATEROLE LOGIN;
GRANT digdag TO root;
CREATE DATABASE digdag_db WITH OWNER digdag;
    
$ psql -h digdag.xxxxxxxx.xxxxxxx.rds.amazonaws.com -U digdag -d digdag_db

CREATE EXTENSION IF NOT EXISTS "uuid-ossp";
```

## Settiong server.properties.tmp

- digdag.secret-encryption-key
```
echo -n '16_bytes_phrase!' | openssl base64
```

```
$ sudo su -
# chown -R hoge:hoge /var/log/digdag
# cd /etc/digdag
# cp server.properties.tmp server.properties
# vim server.properties
# digdag server --config server.properties
# systemctl restart digdag
```

## Setting digdag secrets

```
digdag secrets --local --set gcp.credential=/opt/digdag/key.json
digdag secrets --project hoge --set gcp.credential=@/opt/digdag/key.json
```
