My Docker based local environment setup for web development
---

An ideal Docker based local environment setup not only for Drupal 8 development.

## One-time only setup
* Clone my Traefik configuration from [this](https://github.com/mxr576/my-traefik-docker) respository and start the
Traefik container with `docker-compose up -d`
* Install and setup DNSMasq to redirect all request from .l domains to your
localhost. (Or [add manually](https://wodby.com/stacks/drupal/docs/local/domains/) your project url (ex.: my-project.l) to your system's hosts file.)

How it works? DNSMasq redirects all requests for .l domains to your local machine. Treafik watches incoming
requests to .l domains and based on labels in docker-compose.yml redirects requests to the proper containers.  

## How to use it
* Download [docker-compose.yml](docker-compose.yml) to a folder.
* Download [.env.example](.env.example) to the same folder as docker-compose.yml and change its name to *.env*.
Modify its content according to your needs.
* Run `docker-compose up`.
* Place your code inside the `web` folder in the same folder as docker-compose.yml file lives.

Example folder structure:

```
root:
   - .env
   - docker-compose.yml
   - docker-composer.override.yml (optional)
   - web
       - index.php
```

If you need to change/add anything to this setup add a docker-compose.override.yml
to your project and make your changes in there.

## Usage examples

### xDebug without using Docker for Mac

The `PHP_XDEBUG_REMOTE_HOST` variable must be overridden in docker-compose.override.yml
or the `docker.for.mac.localhost` domain should be redirected to 127.0.0.1.

### Running Drupal 8 PHPUnit tests

If you are using the default image with `-dev` suffix then use the following command inside the php container:

```sh
sudo -u root -E sudo -u www-data -E vendor/bin/phpunit ...
```



**This setup is based on the [Docker4Drupal](https://github.com/wodby/docker4drupal) project
and it uses containers created by [Wodby](wodby.com).**
