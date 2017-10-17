# code

* [Bash](#bash)



## BASH

### MySQL

Import a database from a gzip SQL dump file (*.sql.gz)

```bash
gzip -dc < [DATABASE].sql.gz | mysql -u [USER] -p [DATABASE]
```

Export a database into a gzip SQL dump file

```bash
mysqldump -u [USER] -p [DATABASE] | gzip > [DATABASE].sql.gz 
```
