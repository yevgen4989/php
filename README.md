# PHP Docker Container Images

[![Build Status](https://github.com/yevgen4989/php/workflows/Build%20docker%20image/badge.svg)](https://github.com/yevgen4989/php/actions)
[![Docker Pulls](https://img.shields.io/docker/pulls/yevgen4989/php.svg)](https://hub.docker.com/r/yevgen4989/php)
[![Docker Stars](https://img.shields.io/docker/stars/yevgen4989/php.svg)](https://hub.docker.com/r/yevgen4989/php)
[![Docker Layers](https://images.microbadger.com/badges/image/yevgen4989/php.svg)](https://microbadger.com/images/yevgen4989/php)

## Table of Contents

- [Docker Images](#docker-images)
    - [`-dev`](#-dev)
    - [`-dev-macos`](#-dev-macos)
    - [Supported architectures](#supported-architectures)
- [Environment Variables](#environment-variables)
    - [PHP and PHP-FPM configuration](#php-and-php-fpm-configuration)
    - [Additional configuration](#additional-configuration)
- [Build arguments](#build-arguments)    
- [PHP Extensions](#php-extensions)
- [Tools](#tools)
- [Xdebug](#xdebug)
- [Changelog](#changelog)
- [Users and permissions](#users-and-permissions)
- [Crond](#crond)
- [SSHD](#sshd)
- [Adding SSH key](#adding-ssh-key)
- [Complete PHP-based stack](#complete-php-based-stacks)
- [Images based on `yevgen4989/php`](#images-based-on-yevgen4989php)
- [Orchestration Actions](#orchestration-actions)

## Docker Images

❗For better reliability we release images with stability tags (`yevgen4989/php:8.1-X.X.X`) which correspond to [git tags](https://github.com/yevgen4989/php/releases). We strongly recommend using images only with stability tags. 

About images:

- All images based on Alpine Linux
- Base image: [yevgen4989/base-php](https://github.com/yevgen4989/base-php)
- [GitHub actions builds](https://github.com/yevgen4989/php/actions) 
- [Docker Hub](https://hub.docker.com/r/yevgen4989/php) 

Supported tags and respective `Dockerfile` links:

- `8.1`, `8`, `latest` [_(8/Dockerfile)_]
- `8.0` [_(8/Dockerfile)_]
- `7.4`, `7` [_(7/Dockerfile)_]
- `7.3` [_(7/Dockerfile)_]
- `8.1-dev`, `8-dev`, `dev` [_(8/Dockerfile)_]
- `8.0-dev` [_(8/Dockerfile)_]
- `7.4-dev`, `7-dev` [_(7/Dockerfile)_]
- `7.3-dev` [_(7/Dockerfile)_]
- `8.1-dev-macos`, `8-dev-macos`, `dev-macos` [_(8/Dockerfile)_]
- `8.0-dev-macos` [_(8/Dockerfile)_]
- `7.4-dev-macos`, `7-dev-macos` [_(7/Dockerfile)_]
- `7.3-dev-macos` [_(7/Dockerfile)_]

### `-dev`

Images with `-dev` tag have a few differences:

- `sudo` allowed for all commands for `super` user
- PHP source code available under `/usr/src/php.tar.xz`
- `PHP_FPM_CLEAR_ENV` is set to `no` by default
- Additional packages installed: yarn
- Blackfire CLI installed

### `-dev-macos` 

Same as `-dev` but the default user/group `super` has uid/gid `501`/`20`  to match the macOS default user/group ids.

### Supported architectures

All images built for `linux/amd64` and `linux/arm64` 

## Environment Variables

#### PHP and PHP-FPM configuration

The default configuration not recommended for use for production environment:

| Variable                                | 8.1           | 8.0            | 7.4            | 7.3            |
|-----------------------------------------|---------------|----------------|----------------|----------------|
| [`PHP_ALLOW_URL_FOPEN`]                 | `On`          | `On`           | `On`           | `On`           |
| [`PHP_APCU_ENABLE_CLI`]                 | `0`           | `0`            | `0`            | `0`            |
| [`PHP_APCU_ENABLED`]                    | `1`           | `1`            | `1`            | `1`            |
| [`PHP_APCU_ENTRIES_HINT`]               | `4096`        | `4096`         | `4096`         | `4096`         |
| [`PHP_APCU_COREDUMP_UNMAP`]             | `0`           | `0`            | `0`            | `0`            |
| [`PHP_APCU_GC_TTL`]                     | `3600`        | `3600`         | `3600`         | `3600`         |
| [`PHP_APCU_PRELOAD_PATH`]               | `NULL`        | `NULL`         | `NULL`         | `NULL`         |
| [`PHP_APCU_SERIALIZER`]                 |               |                |                |                |
| [`PHP_APCU_SHM_SEGMENTS`]               | `1`           | `1`            | `1`            | `1`            |
| [`PHP_APCU_SHM_SIZE`]                   | `32M`         | `32M`          | `32M`          | `32M`          |
| [`PHP_APCU_SLAM_DEFENSE`]               | `1`           | `1`            | `1`            | `1`            |
| [`PHP_APCU_TTL`]                        | `0`           | `0`            | `0`            | `0`            |
| [`PHP_APCU_USE_REQUEST_TIME`]           | `1`           | `1`            | `1`            | `1`            |
| [`PHP_ASSERT_ACTIVE`]                   | `On`          | `On`           | `On`           | `On`           |
| [`PHP_AUTO_PREPEND_FILE`]               |               |                |                |                |
| [`PHP_AUTO_APPEND_FILE`]                |               |                |                |                |
| `PHP_BLACKFIRE`                         |               |                |                |                |
| `PHP_BLACKFIRE_AGENT_HOST`              | `blackfire`   | `blackfire`    | `blackfire`    | `blackfire`    |
| `PHP_BLACKFIRE_AGENT_PORT`              | `8707`        | `8707`         | `8707`         | `8707`         |
| `PHP_BROTLI_OUTPUT_COMPRESSION`         | `0`           | `0`            | `0`            | `0`            |
| `PHP_BROTLI_OUTPUT_COMPRESSION_LEVEL`   | `-1`          | `-1`           | `-1`           | `-1`           |
| `PHP_CLI_MEMORY_LIMIT`                  | `-1`          | `-1`           | `-1`           | `-1`           |
| [`PHP_DATE_TIMEZONE`]                   | `UTC`         | `UTC`          | `UTC`          | `UTC`          |
| [`PHP_DEFAULT_SOCKET_TIMEOUT`]          | `60`          | `60`           | `60`           | `60`           |
| [`PHP_DISPLAY_ERRORS`]                  | `On`          | `On`           | `On`           | `On`           |
| [`PHP_DISPLAY_STARTUP_ERRORS`]          | `On`          | `On`           | `On`           | `On`           |
| [`PHP_ERROR_REPORTING`]                 | `E_ALL`       | `E_ALL`        | `E_ALL`        | `E_ALL`        |
| [`PHP_EXPOSE`]                          | `Off`         | `Off`          | `Off`          | `Off`          |
| `PHP_EXTENSIONS_DISABLE`                |               |                |                |                |
| [`PHP_FPM_CLEAR_ENV`]                   | `yes`         | `yes`          | `yes`          | `yes`          |
| `PHP_FPM_ENV_VARS`                      |               |                |                |                |
| [`PHP_FPM_LOG_LEVEL`]                   | `notice`      | `notice`       | `notice`       | `notice`       |
| [`PHP_FPM_PM`]                          | `dynamic`     | `dynamic`      | `dynamic`      | `dynamic`      |
| [`PHP_FPM_PM_MAX_CHILDREN`]             | `8`           | `8`            | `8`            | `8`            |
| [`PHP_FPM_PM_MAX_REQUESTS`]             | `500`         | `500`          | `500`          | `500`          |
| [`PHP_FPM_PM_MAX_SPARE_SERVERS`]        | `3`           | `3`            | `3`            | `3`            |
| [`PHP_FPM_PM_MIN_SPARE_SERVERS`]        | `1`           | `1`            | `1`            | `1`            |
| [`PHP_FPM_PM_STATUS_PATH`]              |               |                |                |                |
| [`PHP_FPM_REQUEST_SLOWLOG_TIMEOUT`]     |               |                |                |                |
| [`PHP_FPM_PM_START_SERVERS`]            | `2`           | `2`            | `2`            | `2`            |
| [`PHP_FPM_USER`]                        | `www-data`    | `www-data`     | `www-data`     | `www-data`     |
| [`PHP_FPM_GROUP`]                       | `www-data`    | `www-data`     | `www-data`     | `www-data`     |
| `PHP_IGBINARY_COMPACT_STRINGS`          | `On`          | `On`           | `On`           | `On`           |
| `PHP_IONCUBE_LOADER_ENABLED`            | -             | -              |                |                |
| [`PHP_LOG_ERRORS`]                      | `On`          | `On`           | `On`           | `On`           |
| [`PHP_LOG_ERRORS_MAX_LEN`]              | `0`           | `0`            | `0`            | `0`            |
| [`PHP_MAX_EXECUTION_TIME`]              | `120`         | `120`          | `120`          | `120`          |
| [`PHP_MAX_FILE_UPLOADS`]                | `20`          | `20`           | `20`           | `20`           |
| [`PHP_MAX_INPUT_TIME`]                  | `60`          | `60`           | `60`           | `60`           |
| [`PHP_MAX_INPUT_VARS`]                  | `2000`        | `2000`         | `2000`         | `2000`         |
| [`PHP_MEMORY_LIMIT`]                    | `512M`        | `512M`         | `512M`         | `512M`         |
| [`PHP_MYSQLI_CACHE_SIZE`]               | `2000`        | `2000`         | `2000`         | `2000`         |
| [`PHP_NEWRELIC_ENABLED`]                | -             | `false`        | `false`        | `false`        |
| [`PHP_NEWRELIC_LICENSE`]                | -             |                |                |                |
| _see all newrelic ext options_          | -             | [8.x newrelic] | [7.x newrelic] | [7.x newrelic] |
| [`PHP_OPCACHE_ENABLE`]                  | `1`           | `1`            | `1`            | `1`            |
| [`PHP_OPCACHE_ENABLE_CLI`]              | `0`           | `0`            | `0`            | `0`            |
| [`PHP_OPCACHE_VALIDATE_TIMESTAMPS`]     | `1`           | `1`            | `1`            | `1`            |
| [`PHP_OPCACHE_REVALIDATE_FREQ`]         | `2`           | `2`            | `2`            | `2`            |
| [`PHP_OPCACHE_MAX_ACCELERATED_FILES`]   | `4000`        | `4000`         | `4000`         | `4000`         |
| [`PHP_OPCACHE_MEMORY_CONSUMPTION`]      | `128`         | `128`          | `128`          | `128`          |
| [`PHP_OPCACHE_INTERNED_STRINGS_BUFFER`] | `8`           | `8`            | `8`            | `8`            |
| [`PHP_OPCACHE_FAST_SHUTDOWN`]           | -             | -              | -              | -              |
| [`PHP_OPCACHE_HUGE_CODE_PAGES`]         | `0`           | `0`            | `0`            | `0`            |
| [`PHP_OPCACHE_PRELOAD`]                 | -             | -              | -              | -              |
| [`PHP_OPCACHE_PRELOAD_USER`]            | `www-data`    | `www-data`     | `www-data`     | `www-data`     |
| [`PHP_OUTPUT_BUFFERING`]                | `4096`        | `4096`         | `4096`         | `4096`         |
| [`PHP_PCOV_ENABLED`]                    | `0`           | `0`            | `0`            | `0`            |
| _see all pcov ext options_              | [8.x pcov]    | [8.x pcov]     | [7.x pcov]     | [7.x pcov]     |
| [`PHP_PDO_MYSQL_CACHE_SIZE`]            | -             | -              | -              | -              |
| [`PHP_PHAR_READONLY`]                   | `1`           | `1`            | `1`            | `1`            |
| [`PHP_PHAR_REQUIRE_HASH`]               | `1`           | `1`            | `1`            | `1`            |
| [`PHP_PHAR_CACHE_LIST`]                 |               |                |                |                |
| [`PHP_POST_MAX_SIZE`]                   | `32M`         | `32M`          | `32M`          | `32M`          |
| [`PHP_REALPATH_CACHE_SIZE`]             | `4096k`       | `4096k`        | `4096k`        | `4096k`        |
| [`PHP_REALPATH_CACHE_TTL`]              | `120`         | `120`          | `120`          | `120`          |
| [`PHP_SENDMAIL_PATH`]                   | `/bin/true`   | `/bin/true`    | `/bin/true`    | `/bin/true`    |
| [`PHP_SESSION_SAVE_HANDLER`]            | `files`       | `files`        | `files`        | `files`        |
| [`PHP_SHORT_OPEN_TAG`]                  | `1`           | `1`            | `1`            | `1`            |
| _see all sqlsrv ext options_            | -             | -              | [7.x sqlsrv]   | [7.x sqlsrv]   |
| _see all session options_               | [8.1 session] | [8.0 session]  | [7.4 session]  | [7.3 session]  |
| `PHP_XHPROF`                            |               |                |                |                |
| _see all xhprof options_                | [8.x xhprof]  | [8.x xhprof]   | [7.x xhprof]   | [7.x xhprof]   |
| [`PHP_UPLOAD_MAX_FILESIZE`]             | `32M`         | `32M`          | `32M`          | `32M`          |
| [`PHP_XDEBUG`]                          |               |                |                |                |
| [`PHP_XDEBUG_MODE`]                     | `off`         | `off`          | `off`          | `off`          |
| _see all xdebug ext options_            | [8.x xdebug]  | [8.x xdebug]   | [7.x xdebug]   | [7.x xdebug]   |
| [`PHP_ZEND_ASSERTIONS`]                 | `1`           | `1`            | `1`            | `1`            |

> "-" - Not available for this version

#### Additional configuration

| Variable                          | Default value       |
|-----------------------------------|---------------------|
| `GIT_USER_EMAIL`                  | `yevgen4989@example.com` |
| `GIT_USER_NAME`                   | `yevgen4989`             |
| `SSH_PRIVATE_KEY`                 |                     |
| `SSH_DISABLE_STRICT_KEY_CHECKING` |                     |
| `SSHD_GATEWAY_PORTS`              | `no`                |
| `SSHD_HOST_KEYS_DIR`              | `/etc/ssh`          |
| `SSHD_LOG_LEVEL`                  | `INFO`              |
| `SSHD_PASSWORD_AUTHENTICATION`    | `no`                |
| `SSHD_PERMIT_USER_ENV`            | `yes`               |
| `SSHD_USE_DNS`                    | `yes`               |

## Build arguments

| Argument         | Default value |
|------------------|---------------|
| `PHP_VER`        |               |
| `PHP_DEV`        |               |
| `SUPER_GROUP_ID` | `1000`        |
| `SUPER_USER_ID`  | `1000`        |

Change `SUPER_USER_ID` and `SUPER_GROUP_ID` mainly for local dev version of images, if it matches with existing system user/group ids the latter will be deleted. 

## PHP Extensions

You can disable extension by listing them in `$PHP_EXTENSIONS_DISABLE` separated by `,`, e.g. `$PHP_EXTENSIONS_DISABLE=event,ds`

| Extension        | 8.1         | 8.0        | 7.4    | 7.3    |
|------------------|-------------|------------|--------|--------|
| [amqp]           | 1.11.0beta  | 1.11.0beta | 1.10.2 | 1.10.2 |
| [apcu]           | 5.1.21      | 5.1.21     | 5.1.21 | 5.1.21 |
| [ast]            | 1.0.10      | 1.0.10     | 1.0.10 | 1.0.10 |
| [blackfire]      | latest      | latest     | latest | latest |
| bcmath           |             |            |        |        |
| brotli           | 0.13.1      | 0.13.1     | 0.13.1 | 0.13.1 |
| bz2              |             |            |        |        |
| calendar         |             |            |        |        |
| Core             |             |            |        |        |
| ctype            |             |            |        |        |
| curl             |             |            |        |        |
| date             |             |            |        |        |
| dom              |             |            |        |        |
| [ds]             | 1.4.0       | 1.4.0      | 1.4.0  | 1.4.0  |
| exif             |             |            |        |        |
| [event]          | 3.0.6       | 3.0.6      | 3.0.6  | 3.0.6  |
| fileinfo         |             |            |        |        |
| filter           |             |            |        |        |
| ftp              |             |            |        |        |
| gd               |             |            |        |        |
| hash             |             |            |        |        |
| iconv            |             |            |        |        |
| [igbinary]       | 3.2.6       | 3.2.6      | 3.2.6  | 3.2.6  |
| [imagick]        | 3.5.1       | 3.5.1      | 3.5.1  | 3.5.1  |
| imap             |             |            |        |        |
| intl             |             |            |        |        |
| [ioncube loader] | -           | -          | latest | latest |
| json             |             |            |        |        |
| ldap             |             |            |        |        |
| libxml           |             |            |        |        |
| mbstring         |             |            |        |        |
| [mcrypt]         | -           | 1.0.4      | 1.0.4  | 1.0.4  |
| [memcached]      | 3.1.5       | 3.1.5      | 3.1.5  | 3.1.5  |
| [mongodb]        | 1.11.1      | 1.11.1     | 1.11.1 | 1.11.1 |
| mysql            | -           | -          | -      | -      |
| mysqli           |             |            |        |        |
| mysqlnd          |             |            |        |        |
| [newrelic]       | -           | latest     | latest | latest |
| [OAuth]          | 2.0.7       | 2.0.7      | 2.0.7  | 2.0.7  |
| openssl          |             |            |        |        |
| [pcov]           | latest      | latest     | latest | latest |
| pcntl            |             |            |        |        |
| pcre             |             |            |        |        |
| PDO              |             |            |        |        |
| pdo_mysql        |             |            |        |        |
| pdo_pgsql        |             |            |        |        |
| pdo_sqlite       |             |            |        |        |
| pdo_sqlsrv       | 5.10.0beta1 | 5.9.0      | 5.9.0  | 5.9.0  |
| pgsql            |             |            |        |        |
| Phar             |             |            |        |        |
| posix            |             |            |        |        |
| [rdkafka]        | 6.0.0       | 6.0.0      | 6.0.0  | 6.0.0  |
| readline         |             |            |        |        |
| [redis]          | 5.3.4       | 5.3.4      | 5.3.4  | 5.3.4  |
| Reflection       |             |            |        |        |
| session          |             |            |        |        |
| SimpleXML        |             |            |        |        |
| soap             |             |            |        |        |
| sockets          |             |            |        |        |
| sodium           |             |            |        |        |
| SPL              |             |            |        |        |
| sqlite3          |             |            |        |        |
| sqlsrv           | 5.10.0beta1 | 5.9.0      | 5.9.0  | 5.9.0  |
| standard         |             |            |        |        |
| tidy             |             |            |        |        |
| tokenizer        |             |            |        |        |
| [uploadprogress] | 2.0.2       | 2.0.2      | 2.0.2  | 2.0.2  |
| [uuid]           | 1.2.0       | 1.2.0      | 1.2.0  | 1.2.0  |
| [xdebug]         | 3.1.2       | 3.1.2      | 3.1.2  | 3.1.2  |
| [xhprof]         | 2.3.5       | 2.3.5      | 2.3.5  | 2.3.5  |
| xml              |             |            |        |        |
| xmlreader        |             |            |        |        |
| xmlrpc           | -           | -          |        |        |
| xmlwriter        |             |            |        |        |
| xsl              |             |            |        |        |
| [yaml]           | 2.2.2       | 2.2.2      | 2.2.2  | 2.2.2  |
| Zend OPcache     |             |            |        |        |
| zip              |             |            |        |        |
| zlib             |             |            |        |        |

Legend:

> - [EMPTY] – Core PHP extension
> - "-" - Not exists in this version
> Some extensions may not be available in [`-dev`](#-dev) images  

Extensions xdebug, blackfire and xhprof disabled by default.

## Tools

| Tool                                | 8.0    | 7.4    | 7.3    |
|-------------------------------------|--------|--------|--------|
| [Composer](https://getcomposer.org) | latest | latest | latest |

## Xdebug

By default, xdebug extension not loaded to avoid any performance impact. Set `PHP_XDEBUG` env var to any value to load it and set [`PHP_XDEBUG_MODE`] to the appropriate value (by default `off` – disabled) to enable xdebug.

## Changelog

Changes per stability tag reflected in git tags description under [releases](https://github.com/yevgen4989/python/releases). 

## Crond

You can run Crond with this image changing the command to `sudo -E LD_PRELOAD=/usr/lib/preloadable_libiconv.so crond -f -d 0` and mounting a crontab file to `./crontab:/etc/crontabs/www-data`. Example crontab file contents:

```
# min	hour	day	month	weekday	command
*/1	*	*	*	*	echo "test" > /mnt/files/cron
```

## SSHD

You can run SSHD with this image by changing the command to `sudo /usr/sbin/sshd -De` and mounting authorized public keys to `/home/super/.ssh/authorized_keys`

## Adding SSH key

You can add a private SSH key to the container by mounting it to `/home/super/.ssh/id_rsa`

## Users and permissions

Default container user is `super:super` (UID/GID `1000`). PHP-FPM runs from `www-data:www-data` user (UID/GID `82`) by default. User `super` is a part of `www-data` group.

Codebase volume `$APP_ROOT` (`/var/www/html`) owned by `super:super`. Files volume `$FILES_DIR` (`/mnt/files`) owned by `www-data:www-data` with `775` mode.

See https://github.com/yevgen4989/php/issues/22 for more details.

#### Helper scripts 

- `files_chmod` – in case you need write access for `super` user to a file/dir generated by `www-data` on this volume run `sudo files_chmod [FILEPATH]` script (FILEPATH must be under `/mnt/files`), it will recursively change the mode to `ug=rwX,o=rX`

- `files_chown` – in case you manually uploaded files under `super` user to files volume and want to change the ownership of those files to `www-data` run `sudo files_chown [FILEPATH]` script (FILEPATH must be under `/mnt/files`), it will recursively change ownership to `www-data:www-data`

## Complete PHP-based stacks

- [yevgen4989/docker4php](https://github.com/yevgen4989/docker4php)
- [yevgen4989/docker4drupal](https://github.com/yevgen4989/docker4drupal)
- [yevgen4989/docker4wordpress](https://github.com/yevgen4989/docker4wordpress)

## Images based on `yevgen4989/php`

- [yevgen4989/drupal-php](https://github.com/yevgen4989/drupal-php)
- [yevgen4989/wordpress-php](https://github.com/yevgen4989/wordpress-php)
- [yevgen4989/adminer](https://github.com/yevgen4989/adminer)
- [yevgen4989/matomo](https://github.com/yevgen4989/matomo)
- [yevgen4989/cachet](https://github.com/yevgen4989/cachet)
- [yevgen4989/webgrind](https://github.com/yevgen4989/webgrind)
- [yevgen4989/xhprof](https://github.com/yevgen4989/xhprof)

## Orchestration Actions

Usage:
```
make COMMAND [params ...]

commands:
    migrate
    check-ready [host max_try wait_seconds delay_seconds]
    git-clone url [branch]
    git-checkout target [is_hash]   
    files-import source
    files-link public_dir 
    update-keys
    walter

default params values:
    is_hash 0
    branch "" Branch, tag or hash commit
```

[_(8/Dockerfile)_]: https://github.com/yevgen4989/php/tree/master/8/Dockerfile
[_(7/Dockerfile)_]: https://github.com/yevgen4989/php/tree/master/7/Dockerfile

[7.x xdebug]: https://github.com/yevgen4989/php/tree/master/7/templates/docker-php-ext-xdebug.ini.tmpl
[8.x xdebug]: https://github.com/yevgen4989/php/tree/master/8/templates/docker-php-ext-xdebug.ini.tmpl
[7.x pcov]: https://github.com/yevgen4989/php/tree/master/7/templates/docker-php-ext-pcov.ini.tmpl
[8.x pcov]: https://github.com/yevgen4989/php/tree/master/8/templates/docker-php-ext-pcov.ini.tmpl
[7.x sqlsrv]: https://github.com/yevgen4989/php/tree/master/7/templates/docker-php-ext-sqlsrv.ini.tmpl
[7.x newrelic]: https://github.com/yevgen4989/php/tree/master/7/templates/docker-php-ext-newrelic.ini.tmpl
[8.x xhprof]: https://github.com/yevgen4989/php/tree/master/8/templates/docker-php-ext-xhprof.ini.tmpl
[7.x xhprof]: https://github.com/yevgen4989/php/tree/master/7/templates/docker-php-ext-xhprof.ini.tmpl
[8.1 session]: https://github.com/yevgen4989/php/tree/master/8/templates/docker-php-8.1.ini.tmpl
[8.0 session]: https://github.com/yevgen4989/php/tree/master/8/templates/docker-php-8.0.ini.tmpl
[7.4 session]: https://github.com/yevgen4989/php/tree/master/7/templates/docker-php-7.4.ini.tmpl
[7.3 session]: https://github.com/yevgen4989/php/tree/master/7/templates/docker-php-7.3.ini.tmpl

[`PHP_ALLOW_URL_FOPEN`]: http://php.net/manual/en/filesystem.configuration.php#ini.allow-url-fopen
[`PHP_APCU_COREDUMP_UNMAP`]: http://php.net/manual/en/apcu.configuration.php#ini.apcu.coredump-unmap
[`PHP_APCU_ENABLE_CLI`]: http://php.net/manual/en/apcu.configuration.php#ini.apcu.enable-cli
[`PHP_APCU_ENABLED`]: http://php.net/manual/en/apcu.configuration.php#ini.apcu.enabled
[`PHP_APCU_ENTRIES_HINT`]: http://php.net/manual/en/apcu.configuration.php#ini.apcu.entries-hint
[`PHP_APCU_GC_TTL`]: http://php.net/manual/en/apcu.configuration.php#ini.apcu.gc-ttl
[`PHP_APCU_PRELOAD_PATH`]: http://php.net/manual/en/apcu.configuration.php#ini.apcu.preload-path
[`PHP_APCU_SERIALIZER`]: http://php.net/manual/en/apcu.configuration.php#ini.apcu.serializer
[`PHP_APCU_SHM_SEGMENTS`]: http://php.net/manual/en/apcu.configuration.php#ini.apcu.shm-segments
[`PHP_APCU_SHM_SIZE`]: http://php.net/manual/en/apcu.configuration.php#ini.apcu.shm-size
[`PHP_APCU_SLAM_DEFENSE`]: http://php.net/manual/en/apcu.configuration.php#ini.apcu.slam-defense
[`PHP_APCU_TTL`]: http://php.net/manual/en/apcu.configuration.php#ini.apcu.ttl
[`PHP_APCU_USE_REQUEST_TIME`]: http://php.net/manual/en/apcu.configuration.php#ini.apcu.use-request-time
[`PHP_ASSERT_ACTIVE`]: http://php.net/assert.active
[`PHP_AUTO_APPEND_FILE`]: http://php.net/auto-append-file
[`PHP_AUTO_PREPEND_FILE`]: http://php.net/auto-prepend-file
[`PHP_DATE_TIMEZONE`]: http://php.net/date.timezone
[`PHP_DEFAULT_SOCKET_TIMEOUT`]: http://php.net/manual/en/filesystem.configuration.php#ini.default-socket-timeout
[`PHP_DISPLAY_ERRORS`]: http://php.net/display-errors
[`PHP_DISPLAY_STARTUP_ERRORS`]: http://php.net/display-startup-errors
[`PHP_ERROR_REPORTING`]: http://php.net/error-reporting
[`PHP_EXPOSE`]: http://php.net/expose-php
[`PHP_FPM_CLEAR_ENV`]: http://php.net/manual/en/install.fpm.configuration.php#clear-env
[`PHP_FPM_GROUP`]: http://php.net/manual/en/install.fpm.configuration.php#group
[`PHP_FPM_LOG_LEVEL`]: http://php.net/manual/en/install.fpm.configuration.php#log-level
[`PHP_FPM_PM_MAX_CHILDREN`]: http://php.net/manual/en/install.fpm.configuration.php#pm.max-chidlren
[`PHP_FPM_PM_MAX_REQUESTS`]: http://php.net/manual/en/install.fpm.configuration.php#pm.max-requests
[`PHP_FPM_PM_MAX_SPARE_SERVERS`]: http://php.net/manual/en/install.fpm.configuration.php#pm.max-spare-servers
[`PHP_FPM_PM_MIN_SPARE_SERVERS`]: http://php.net/manual/en/install.fpm.configuration.php#pm.min-spare-servers
[`PHP_FPM_PM_START_SERVERS`]: http://php.net/manual/en/install.fpm.configuration.php#pm.start-servers
[`PHP_FPM_PM_STATUS_PATH`]: http://php.net/manual/en/install.fpm.configuration.php#pm.status-path
[`PHP_FPM_PM`]: http://php.net/manual/en/install.fpm.configuration.php#pm
[`PHP_FPM_REQUEST_SLOWLOG_TIMEOUT`]: http://php.net/manual/en/install.fpm.configuration.php#request-slowlog-timeout
[`PHP_FPM_USER`]: http://php.net/manual/en/install.fpm.configuration.php#user
[`PHP_LOG_ERRORS_MAX_LEN`]: http://php.net/log-errors-max-len
[`PHP_LOG_ERRORS`]: http://php.net/log-errors
[`PHP_MAX_EXECUTION_TIME`]: http://php.net/max-execution-time  
[`PHP_MAX_FILE_UPLOADS`]: http://php.net/manual/en/ini.core.php#ini.max-file-uploads
[`PHP_MAX_INPUT_TIME`]: http://php.net/max-input-time
[`PHP_MAX_INPUT_VARS`]: http://php.net/max-input-vars
[`PHP_MBSTRING_ENCODING_TRANSLATION`]: http://php.net/mbstring.encoding-translation
[`PHP_MBSTRING_HTTP_INPUT`]: http://php.net/mbstring.http-input
[`PHP_MBSTRING_HTTP_OUTPUT`]: http://php.net/mbstring.http-output
[`PHP_MEMORY_LIMIT`]: http://php.net/memory-limit
[`PHP_MYSQLI_CACHE_SIZE`]: http://php.net/mysqli.cache_size
[`PHP_NEWRELIC_APPNAME`]: https://docs.newrelic.com/docs/agents/php-agent/configuration/php-agent-configuration#inivar-appname
[`PHP_NEWRELIC_BROWSER_MONITORING_AUTO_INSTRUMENT`]: https://docs.newrelic.com/docs/agents/php-agent/configuration/php-agent-configuration#inivar-autorum
[`PHP_NEWRELIC_CAPTURE_PARAMS`]: https://docs.newrelic.com/docs/agents/php-agent/configuration/php-agent-configuration#inivar-enabled
[`PHP_NEWRELIC_ENABLED`]: https://docs.newrelic.com/docs/agents/php-agent/configuration/php-agent-configuration#inivar-enabled
[`PHP_NEWRELIC_FRAMEWORK`]: https://docs.newrelic.com/docs/agents/php-agent/configuration/php-agent-configuration#inivar-framework
[`PHP_NEWRELIC_GUZZLE_ENABLED`]: https://docs.newrelic.com/docs/agents/php-agent/configuration/php-agent-configuration#inivar-autorum
[`PHP_NEWRELIC_HIGH_SECURITY`]: https://docs.newrelic.com/docs/agents/php-agent/configuration/php-agent-configuration#inivar-high-security
[`PHP_NEWRELIC_IGNORED_PARAMS`]: https://docs.newrelic.com/docs/agents/php-agent/configuration/php-agent-configuration#inivar-ignored_params
[`PHP_NEWRELIC_LABELS`]: https://docs.newrelic.com/docs/agents/php-agent/configuration/php-agent-configuration#inivar-labels
[`PHP_NEWRELIC_LICENSE`]: https://docs.newrelic.com/docs/agents/php-agent/configuration/php-agent-configuration#inivar-license
[`PHP_NEWRELIC_LOGLEVEL`]: https://docs.newrelic.com/docs/agents/php-agent/configuration/php-agent-configuration#inivar-loglevel
[`PHP_NEWRELIC_TRANSACTION_TRACER_DETAIL`]: https://docs.newrelic.com/docs/agents/php-agent/configuration/php-agent-configuration#inivar-tt-detail
[`PHP_NEWRELIC_DISTRIBUTED_TRACING_ENABLED`]: https://docs.newrelic.com/docs/agents/php-agent/configuration/php-agent-configuration#inivar-misctt-settings
[`PHP_OPCACHE_ENABLE_CLI`]: http://php.net/manual/en/opcache.configuration.php#ini.opcache.enable-cli
[`PHP_OPCACHE_ENABLE`]: http://php.net/manual/en/opcache.configuration.php#ini.opcache.enable
[`PHP_OPCACHE_FAST_SHUTDOWN`]: http://php.net/manual/en/opcache.configuration.php#ini.opcache.fast-shutdown
[`PHP_OPCACHE_HUGE_CODE_PAGES`]: http://php.net/manual/en/opcache.configuration.php#ini.opcache.huge_code_pages
[`PHP_OPCACHE_INTERNED_STRINGS_BUFFER`]: http://php.net/manual/en/opcache.configuration.php#ini.opcache.interned-strings-buffer
[`PHP_OPCACHE_MAX_ACCELERATED_FILES`]: http://php.net/manual/en/opcache.configuration.php#ini.opcache.max-accelerated-files
[`PHP_OPCACHE_MEMORY_CONSUMPTION`]: http://php.net/manual/en/opcache.configuration.php#ini.opcache.memory-consumption
[`PHP_OPCACHE_PRELOAD`]: http://php.net/manual/en/opcache.configuration.php#ini.opcache.preload
[`PHP_OPCACHE_PRELOAD_USER`]: http://php.net/manual/en/opcache.configuration.php#ini.opcache.preload-user
[`PHP_OPCACHE_REVALIDATE_FREQ`]: http://php.net/manual/en/opcache.configuration.php#ini.opcache.revalidate-freq
[`PHP_OPCACHE_VALIDATE_TIMESTAMPS`]: http://php.net/manual/en/opcache.configuration.php#ini.opcache.validate-timestamps
[`PHP_OUTPUT_BUFFERING`]: http://php.net/output-buffering
[`PHP_PDO_MYSQL_CACHE_SIZE`]: http://php.net/pdo_mysql.cache_size
[`PHP_PHAR_CACHE_LIST`]: http://php.net/manual/en/phar.configuration.php#ini.phar.cache-list
[`PHP_PHAR_READONLY`]: http://php.net/manual/en/phar.configuration.php#ini.phar.readonly
[`PHP_PHAR_REQUIRE_HASH`]: http://php.net/manual/en/phar.configuration.php#ini.phar.require-hash
[`PHP_POST_MAX_SIZE`]: http://php.net/post-max-size
[`PHP_REALPATH_CACHE_SIZE`]: http://php.net/realpath-cache-size
[`PHP_REALPATH_CACHE_TTL`]: http://php.net/realpath-cache-ttl
[`PHP_SENDMAIL_PATH`]: http://php.net/sendmail-path
[`PHP_SESSION_SAVE_HANDLER`]: http://php.net/session.save-handler
[`PHP_SHORT_OPEN_TAG`]: https://www.php.net/manual/en/ini.core.php#ini.short-open-tag
[`PHP_TRACK_ERRORS`]: http://php.net/track-errors
[`PHP_UPLOAD_MAX_FILESIZE`]: http://php.net/upload-max-filesize
[`PHP_XDEBUG_MODE`]: https://xdebug.org/docs/all_settings#mode
[`PHP_XDEBUG`]: #xdebug
[`PHP_ZEND_ASSERTIONS`]: http://php.net/zend.assertions
[`PHP_PCOV_ENABLED`]: https://github.com/krakjoe/pcov#configuration

[amqp]: http://pecl.php.net/package/amqp
[apcu]: http://pecl.php.net/package/apcu
[ast]: https://github.com/nikic/php-ast
[ds]: https://pecl.php.net/package/ds
[event]: https://pecl.php.net/package/event
[grpc]: https://pecl.php.net/package/grpc
[igbinary]: https://pecl.php.net/package/igbinary
[imagick]: https://pecl.php.net/package/imagick
[ioncube loader]: https://www.ioncube.com/loaders.php
[mcrypt]: http://pecl.php.net/package/mcrypt
[memcached]: http://pecl.php.net/package/memcached
[mongodb]: http://pecl.php.net/package/mongodb
[newrelic]: http://download.newrelic.com/php_agent/release
[OAuth]: http://pecl.php.net/package/oauth
[pcov]: https://pecl.php.net/package/pcov
[rdkafka]: https://pecl.php.net/package/rdkafka
[redis]: http://pecl.php.net/package/redis
[uploadprogress]: https://pecl.php.net/package/uploadprogress
[uuid]: https://pecl.php.net/package/uuid
[xdebug]: https://pecl.php.net/package/xdebug
[xhprof]: https://pecl.php.net/package/xhprof
[yaml]: https://pecl.php.net/package/yaml
[latest]: https://github.com/yevgen4989/pecl-php-uploadprogress/releases/tag/latest
[blackfire]: https://blackfire.io/dashboard/mine/profiles
