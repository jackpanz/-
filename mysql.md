# mysql 導出數據庫
```mysql
mysqldump --default-character-set=utf8mb4 -h127.0.0.1 -P3306 -uroot -proot --hex-blob --databases db1 db2 db3 -r D:\database_backup\all.sql
```

# mysql 導入數據庫
```mysql
mysql -uroot -proot -h127.0.0.1 -P3306 <D:\database_backup\all.sql
```
