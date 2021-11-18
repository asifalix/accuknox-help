```sh
kubectl run -i --rm --tty percona-client --image=percona:8.0 --restart=Never -- bash -il
```

```sh
mysql -h service name  -u[user] -p[password]
```

```sh
show databases;
```

![Alt](../images/mysql-verify.png)