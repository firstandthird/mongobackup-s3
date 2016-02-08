# mongobackup-s3

A simple docker container to backup MongoDB to S3, restore backups, and list backups.  Easy to integrate with cron.

## Usage

### Backup
To initiate a backup:

```
docker run --rm --link mongo:mongo --env AWS_ACCESS_KEY_ID=123 --env AWS_SECRET_ACCESS_KEY=123 --env S3BUCKET=bucket firstandthird/mongobackup-s3
```

#### Customizing backup names
The naming used by backups can also be customised through environment variables:
- ``DATEFORMAT`` accepts a Unix date format. Defaults to: ``%Y%m%d_%H%M%S``
- ``FILEPREFIX`` to add a prefix to the start of the backup's name. Defaults to blank.

**Example**
To add a file like ``mongodb.2016-02-08-03-10-20.tar.gz`` to your AWS bucket:
```
docker run --rm --link mongo:mongo --env DATEFORMAT=%Y-%m-%d-%H-%M-%S --env FILEPREFIX=mongodb. --env AWS_ACCESS_KEY_ID=123 --env AWS_SECRET_ACCESS_KEY=123 --env S3BUCKET=bucket firstandthird/mongobackup-s3
```

## List
To list the backups on S3:

```
docker run --rm --link mongo:mongo --env AWS_ACCESS_KEY_ID=123 --env AWS_SECRET_ACCESS_KEY=123 --env S3BUCKET=bucket firstandthird/mongobackup-s3 list
```

## Restore
To restore a given backup, where `[backup-file-name]` is the name of the backup file you would like to restore:

```
docker run --rm --link mongo:mongo --env AWS_ACCESS_KEY_ID=123 --env AWS_SECRET_ACCESS_KEY=123 --env S3BUCKET=bucket firstandthrd/mongobackup-s3 [backup-file-name]
```
