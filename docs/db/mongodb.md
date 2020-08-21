# MongoDB

## install

``` sh
sudo apt update
sudo apt-get install -y mongodb
```

## check status

``` sh
$ sudo systemctl status mongodb
● mongodb.service - LSB: An object/document-oriented database
 Loaded: loaded (/etc/init.d/mongodb; generated)
 Active: active (running) since Mon 2019-01-21 07:55:49 CST; 13h ago
   Docs: man:systemd-sysv-generator(8)
Process: 850 ExecStart=/etc/init.d/mongodb start (code=exited, status=0/SUCCESS)
  Tasks: 26 (limit: 4915)
 CGroup: /system.slice/mongodb.service
         └─944 /usr/bin/mongod --config /etc/mongodb.conf

1月 21 07:55:45 litreily-pc systemd[1]: Starting LSB: An object/document-oriented database...
1月 21 07:55:45 litreily-pc mongodb[850]:  * Starting database mongodb
1月 21 07:55:49 litreily-pc mongodb[850]:    ...done.
1月 21 07:55:49 litreily-pc systemd[1]: Started LSB: An object/document-oriented database.
```

## mongoexport

``` sh
mongoexport -h localhost:27017 -d databaseName -c collectionName -f data.json
```

## mongoimport

``` sh
$ mongoimport -h localhost:27017 -d databaseName -c collectionName -f data.json
$ mongo
> use databaseName
> databaseName.collectionName.find().pretty()
```

## manager

- [Robo 3T](https://robomongo.org/)
