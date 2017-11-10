# Alpine MailHog Image

![https://www.augustash.com](http://augustash.s3.amazonaws.com/logos/ash-inline-color-500.png)

**This base container is not currently aimed at public consumption. It exists as a starting point for August Ash containers.**

## Versions

- `1.0.0`, `latest` [(Dockerfile)](https://github.com/augustash/docker-alpine-mailhog/blob/1.0.0/Dockerfile)

[See VERSIONS.md for image contents.](https://github.com/augustash/docker-alpine-mailhog/blob/master/VERSIONS.md)

## Usage

Launch a MailHog container that can act as a development SMTP server with an HTTP interface:

```bash
docker run --rm \
    -p 8025:8025 \
    -p 1025:1025 \
    --net <NETWORK NAME> \
    augustash/alpine-mailhog
```

### PHP Sendmail

You must direct email to the running container and that can be done by SMTP or `sendmail` for PHP applications.

For example, in your `php.ini` configuration you can use the following line:

```bash
sendmail_path = /usr/sbin/sendmail -S mail:1025
```

Alternatively you can look into MailHog's `sendmail` replacement called [mhsendmail](https://github.com/mailhog/mhsendmail). If installed, it can be used like this:

```bash
sendmail_path = /usr/local/bin/mhsendmail
```

### Web UI

Once running and capturing email, you can view the messages using the Web UI. If using the default hostname/ports, open a browser and visit [MailHog Web UI](http://mailhog.dev:8025).

### User/Group Identifiers

To help avoid nasty permissions errors, the container allows you to specify your own `PUID` and `PGID`. This can be a user you've created or even root (not recommended).

### Environment Variables

The following variables can be set and will change how the container behaves. You can use the `-e` flag, an environment file, or your Docker Compose file to set your preferred values. The default values are shown:

- `PUID`=501
- `PGID`=1000
- `MAIL_STORAGE`=memory
- `MAIL_SMTP_PORT`=1025
- `MAIL_API_PORT`=8025
- `MAIL_HOSTNAME`=mailhog.dev
- `MAIL_PARAMS`=
