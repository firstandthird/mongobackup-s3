#mongodumpandrestore-s3

A simple docker container to backup and restore mongo to and from s3.  Easy to integrate with cron


## Installation

```
docker build -t mongodumpandrestore-s3 git://github.com/rooseveltlai/mongodumpandrestore-s3.git
```

## Usage

Backup:

```
docker run --rm --link mongo:mongo --env AWS_ACCESS_KEY_ID=123 --env AWS_SECRET_ACCESS_KEY=123 --env S3BUCKET=bucket mongodumpandrestore-s3
```

Restore:

```
docker run --rm --link mongo:mongo --env AWS_ACCESS_KEY_ID=123 --env AWS_SECRET_ACCESS_KEY=123 --env S3BUCKET=bucket mongodumpandrestore-s3 20141017_221942.tar.gz
```



