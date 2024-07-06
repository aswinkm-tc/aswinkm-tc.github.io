+++
title = "Taking backup of MariaDB databases"
date = 2024-04-28T16:05:00+02:00
url = "post/maria-db-backup"
Tags = ["mariadb","backup"]
Categories = ["operations","databases"]
draft = true
thumbnail = "/images/mariadb-logo.jpeg"
+++
---
MariaDB is a popular open-source database management system and a drop-in replacement for MySQL.

Mariadb backups can be made using [mariadb-backup](https://mariadb.com/kb/en/mariabackup-overview/) utility.

## Alternatives
1. Using percona-xtrabackup but it's not supported on the newer versions of mariadb(no support on 10.3 and partial support on 10.1 & 10.2).
2. Using mysqldump to take backups of database but it doesn't provide information about the binlog name and log position

## Installation

```bash
apt-get install mariadb-backup
```
## Backing up and preparing data
```bash
mariabackup --backup --target-dir=/data/backup/
mariabackup --prepare --target-dir=/data/backup/
```

## Restoring data
```bash
mariabackup --copy-back --target-dir=/data/backup/
```

>Note: Incase you get an error about the restored data run the following command
```bash
mysql_upgrade
```

## Dumping all databases as backup
mysqldump is a good tool to dump entire database fast and efficiently.
### Without Compression
```bash
mysqldump --all-databases --routines > "/data/backup/$(date +"%y%m%d%H%M%S").sql"
```
### With Compression
```bash
mysqldump --all-databases --routines | gzip > "/data/backup/$(date +"%y%m%d%H%M%S").sql.gz"
```

## Restoring from backup
```bash
mysql < /data/backup/<timestamp>.sql
```

## Handling authentication
On databases with authentication it's good to use authentication files saved in $HOME directory <br> The file format is as follows:
```bash
#
# .my.cnf
#
[client]
user="username"
password="changeme"
```
