# PsQL - Postgres

Connection
At the command line, type the following command, replacing username with your username:
```js
$ psql -U <username>
```

Drop & create db
```js
DROP database dev;
CREATE database dev;
```

Export
```js
pg_dump -U username <database_name> > dbexport.pgsql
```

import
```js
psql -U username <database_name> < dbexport.pgsql
```
