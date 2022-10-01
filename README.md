# Gitea backup for Docker

A docker container to backup your Kubernetes-based Gitea instance to a S3 bucket or SFTP server.

## Configuration

Create a configuration file as described in the [ten7.gitea_backup](https://github.com/ten7/gitea-backup) Ansible role.

Once created, you have three ways to provide it to the container:
* As a base64-encoded value of the `GITEA_BACKUP_CONFIG` environment variable
* As a mounted file at the location specified by the `GITEA_BACKUP_CONFIG_FILE` environment variable
* As a mounted file at `/config/gitea-backup/gitea-backup.yml` inside the container.

## Use with base Docker

To run the Docker image as part of a script or in cron, use the following command:

```shell
docker run --rm -v /path/to/gitea-backup.yml:/config/gitea-backup/gitea-backup.yml ten7/gitea-backup
```

Note, that if your `gitea-backup.yml` file depends on other files (such as TLS keys) you will need to add multiple `-v` switches to mount each one.

## Docker compose

Create the following Docker Compose file.

```yaml
version: '3'
services:
  backup:
    image: ten7/gitea-backup
    volumes:
      - /path/to/gitea-backup.yml:/config/gitea-backup/gitea-backup.yml
```

Again, if your `gitea-backup.yml` depends on other files (such as TLS keys) you will need to add additional items under `volumes` to mount them.

Once the `docker-compose.yml` file is created, you can run backups using:

```shell
docker-compose run backup
```

## License

GPL v3

## Author Information

This Docker image was created by [TEN7](https://ten7.com/).

