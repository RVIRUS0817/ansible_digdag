# ansible_digdag

![スクリーンショット 2020-12-09 20 28 32](https://user-images.githubusercontent.com/5633085/101624459-49d50980-3a5d-11eb-874f-780ea593e1b0.jpg)


## Environment

- Amazon linux2
- RDS(PostgreSQL)
- digdag
- embulk

## dry-run

```
$ ansible-playbook -i hosts prd.yml -C
```

## run

```
$ ansible-playbook -i hosts prd.yml 
```

## Settiong server.properties.tmp

```
sudo su -
cd /etc/digdag
cp server.properties.tmp server.properties
vim server.properties
systemctl restart digdag
```
