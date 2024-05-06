MySql

Connection
At the command line, type the following command, replacing username with your username:
```js
$ mysql -u username -p
```

To dump/export a MySQL database, execute the following command:
```js
mysqldump -u username -p dbname > filename.sql
```

To restore/import a MySQL database, execute the following command
```js
$ mysql -u username -p dbname < filename.sql
$ mysql -u root -p i22-newsletter-system < now.sql
```
