# rsnap

Simple bash script to make a hard linked differential backup pulled from remote machines. There is solutions that does this with a lot more features as [rdiff-backup](https://rdiff-backup.net/) or [BackupPC](https://backuppc.github.io/backuppc/). But if you just need a simple solution running in cron, this may be your thing.

## Backup structure

Backups will be stored in destination directory with the structure below. A link `latest` will be created and point to the latest backup at after each run.

```
.
└── my.domain.com
    ├── 2021-03-06T17:22:38+00:00
    ├── 2021-03-06T17:23:07+00:00
    ├── 2021-03-06T17:23:11+00:00
    ├── 2021-03-06T17:23:27+00:00
    ├── 2021-03-06T17:23:35+00:00
    └── latest -> 2021-03-06T17:23:35+00:00
```

## How to use

```
rsnap creates rsync snapshots of one or more paths on a remote
location. Specify number of snapshots to keep and/or max age in days.

Snapshot name format: 2021-03-06T10:25:45+00:00. A link, latest, point to
the latest snapshot.

  -d DAYS           number of days to keep snapshots
  -i                ignore missing remote folder or server
  -n NUMBER         max number of snapshots to keep
  -p PATH           destination path, autocreated if missing
  -s SERVER         server to rsync from, user@server may be used
  -v LEVEL          verbosity level where 1=ERROR, 2=WARN, 3=INFO, 4=DEBUG

Snapshot one or more paths on the remote server.

Example: Make backup of my.domain.com:/var/backups and my.domain.com:/etc
to this servers /srv/backups. Keep 90 days of snapshots or max 30 snapshots.

  rsnap -n 30 -d 90 -p /srv/backups my.domain /var/backups /etc
```



<!---
vim: set spell spelllang=en:
-->
