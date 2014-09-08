#mongodump-s3

A simple docker container to backup mongo to s3.  Easy to integrate with cron


## Installation

```
docker build -t mongodump-s3 git://github.com:firstandthird/mongodump-s3.git
```

## Usage

```
docker run --rm --link mongo:mongo --env AWS_ACCESS_KEY_ID=123 --env AWS_SECRET_ACCESS_KEY=123 --env S3BUCKET=bucket mongodump-s3
```


