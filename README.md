# PHP-FPM 7.2.29-DEV Docker
PHP-FPM 7.2.29 use **ONLY** for development environment

**Good for the latest stable version of symfony**

[![Build Status](https://api.travis-ci.com/bsramin/docker-php7.2-fpm-dev.svg?branch=master)](https://travis-ci.com/github/bsramin/docker-php7.2-fpm-dev)
[![](https://images.microbadger.com/badges/image/ramin/php7.2.svg)](https://microbadger.com/images/ramin/php7.2 "Get your own image badge on microbadger.com")
[![](https://images.microbadger.com/badges/version/ramin/php7.2.svg)](https://microbadger.com/images/ramin/php7.2 "Get your own version badge on microbadger.com")

*Based on **[php:7.2.29-fpm](https://github.com/docker-library/php/blob/master/7.2/stretch/fpm/Dockerfile)***

## Services

- **PHP-FPM 7.2.29** (on *port 9001*)
    - **APCu** - APC User Cache
    - **OPcache**
    - PHP extension for interfacing with **Redis** (with php session.save_handler pre-configurated with tcp://redis-session:6379)
    - **PHP Intl** extension with **Icu** 63.1
    - **PHP pdo/pdo_mysql** extension 
    - **PHP zip** extension 
- **Xdebug** 2.6.1 (on *port 9000*)
- **Composer**
- **GIT**
- **ZSH** (with *oh-my-zsh*) shell

***

### Xdebug

Preconfigurated with this arg

    ARG XDEBUG_KEY="PHPSTORM"
    ARG XDEBUG_REMOTE_IP="10.254.254.254"
    ARG XDEBUG_REMOTE_PORT="9000"
 
#### Xdebug with macOS host (Docker for Mac)

Add new alias loopback for localhost

    sudo ifconfig lo0 alias 10.254.254.254 netmask 255.255.255.0

or use [xdebug-starter.sh](https://github.com/bsramin/dch-project-sample/blob/master/container/php/xdebug-starter.sh)

#### Xdebug with Linux host

Add new alias loopback for localhost

Append to file `/etc/network/interfaces`


    auto lo:0
    iface lo:0 inet static
    name Docker loopback
    address 10.254.254.254
    netmask 255.255.255.0

or use [xdebug-starter.sh](https://github.com/bsramin/dch-project-sample/blob/master/container/php/xdebug-starter.sh)

***

### Redis (session handler)

If you use this docker with compose, simply add this service to your docker-compose.yml

      redis-session:
          image: redis:latest
          hostname: redis-session
          ports:
            - "6379:6379"
            
And link php container with redis

eg.

      php:
          image: ramin/php7.2:latest
          hostname: php
          links:
              - redis-session


*** 

Licensed under a GPL3+ license: http://www.gnu.org/licenses/gpl-3.0.txt