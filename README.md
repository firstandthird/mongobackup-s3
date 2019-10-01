# mongobackup-s3

A simple docker container to backup MongoDB to S3, restore backups, and list backups.  Easy to integrate with cron.

## Usage

### Backup
To initiate a backup: (you can now pass in `--env DB=[db]` to only backup a specific db)

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

## Credentials
You can set the following env variables if you want to authenticate:
```
-e MONGO_USER=exampleuser -e MONGO_PASSWORD=examplepassword -e MONGOD_AUTH_DB=exampleAuthDb
```

## List
To list the backups on S3:

```
docker run --rm --link mongo:mongo --env AWS_ACCESS_KEY_ID=123 --env AWS_SECRET_ACCESS_KEY=123 --env S3BUCKET=bucket firstandthird/mongobackup-s3 list
```

## Restore Latest
To restore the latest backup on S3:
```
docker run --rm --link mongo:mongo --env AWS_ACCESS_KEY_ID=123 --env AWS_SECRET_ACCESS_KEY=123 --env S3BUCKET=bucket firstandthird/mongobackup-s3 latest
```

The sort order is used to determine the latest backup. If a ``FILEPREFIX`` is defined, this will filter the bucket list results. If using a custom ``DATEFORMAT``, ensure the sort order will still represent the correct date order.

## Restore
To restore a given backup, where `[backup-file-name]` is the name of the backup file you would like to restore:

```
docker run --rm --link mongo:mongo --env AWS_ACCESS_KEY_ID=123 --env AWS_SECRET_ACCESS_KEY=123 --env S3BUCKET=bucket firstandthrd/mongobackup-s3 [backup-file-name]
```
