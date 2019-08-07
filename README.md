# Backup scripts for MySQL server on Linux

Performs nightly, weekly and quarterly backups of a MySQL database with the following retention policy:

 - Nightly dumps written every night, always overwriting the dump from one week ago
 - Weekly dumps written every Sunday, always overwriting the dump from four weeks ago
 - Quarterly dumps written every first March, June, September and December, always overwriting the dump from one year ago

Scripts are run via cronjobs. Here is a sample configuration of the crontab:

```
# m h  dom mon      dow   command
  0 2  *   *        1-6   /home/ubuntu/mysqlbackup/backup_nightly    > /home/ubuntu/mysqlbackup/nightly.log   2>&1
  0 2  *   *        0     /home/ubuntu/mysqlbackup/backup_weekly     > /home/ubuntu/mysqlbackup/weekly.log    2>&1
  0 22 1   3,6,9,12 *     /home/ubuntu/mysqlbackup/backup_quartlerly > /home/ubuntu/mysqlbackup/quarterly.log 2>&1
```

These scripts have not been tested extensively. Use at your own risk!
