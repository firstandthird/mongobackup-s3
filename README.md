#mongobackup-s3

A simple docker container to backup mongo to s3.  Easy to integrate with cron.

## Usage

To initiate a backup.

```
docker run --rm --link mongo:mongo --env AWS_ACCESS_KEY_ID=123 --env AWS_SECRET_ACCESS_KEY=123 --env S3BUCKET=bucket firstandthird/mongobackup-s3
```

To list the backups on s3.

```
docker run --rm --link mongo:mongo --env AWS_ACCESS_KEY_ID=123 --env AWS_SECRET_ACCESS_KEY=123 --env S3BUCKET=bucket firstandthird/mongobackup-s3 list
```

To restore a given backup, where `[backup-file-name]` is the name of the backup file you would like to restore.

```
docker run --rm --link mongo:mongo --env AWS_ACCESS_KEY_ID=123 --env AWS_SECRET_ACCESS_KEY=123 --env S3BUCKET=bucket firstandthrd/mongobackup-s3 [backup-file-name]
```
