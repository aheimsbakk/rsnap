# rsnap

Simple bash script to make a hard linked differential backup pulled from remote machines. Only dependency on the remote is `rsync`. If you want compression and checksumming use `zfs` or `btrfs` file system on the target machine.

This script is intended for low volume backups. Use something more suited if you want to backup massive amount of files. There is solutions that does this with more features as

* [BackupPC](https://backuppc.github.io/backuppc/)
* [Borg backup](https://www.borgbackup.org/)
* [rdiff-backup](https://rdiff-backup.net/)
* [restic](https://restic.net/)

and many more...

## Backup structure

Backups will be stored in destination directory with the structure below. A link `latest` will be created and point to the latest backup after each run.

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
rsnap [-h] [-v] [-I] [-i FILENAME] [-d DAYS] [-n NUMBER] [-p PATH] [-s SERVER] PATH...

rsnap creates rsync snapshots of one or more paths on a remote
location. Specify number of snapshots to keep and/or max age in days.

Snapshot name format: 2021-03-06T10:25:45+00:00. A link, latest, point to
the latest snapshot.

  -d DAYS           number of days to keep snapshots
  -i FILENAME       if file exists in directory, ignore directory
  -I                ignore missing remote directory or server
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
