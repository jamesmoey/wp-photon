Local WordPress Photon server (for development)
===============================================

## Photon documentation

Please refer to https://jetpack.com/support/photon/

## Requirements

This project requires Docker, download and install it from https://www.docker.com

## Installation

Clone repository to your local machine.

Switch to the project directory and run the following command: `docker-compose build`. Docker Compose will pull PHP Apache image from https://hub.docker.com/_/php/ and then it will build Photon image. It will take some time.

## Configuring hosts

See your `/etc/hosts` file: you will need an IP address used by Vagrant and configured host names.

Copy `docker-compose.override.yml.sample` into `docker-compose.override.yml.sample` and updates hosts listed there.

**Note**: `extra_hosts` must be an array of "host:IP" mappings.

## Configuring WordPress

To change default Photon domain in the WordPress you need to register a new filter like this:

```
add_filter( 'jetpack_photon_domain', function() {
	return 'http://192.168.99.100/';
} );
```

**Note**: to get an IP of the Docker, run `docker-machine ip`.

Also, to enable Thumbnail Editor plugin you need to force load it:

```
\wpcom_vip_load_plugin( 'wpcom-thumbnail-editor' );
```

## Running Photon

Use the following commands to run Photon:

* `docker-compose up` - runs Photon server in foreground
* `docker-compose up -d` - runs Photon server in background
* `docker-compose down` - stops server and removes Docker container (it will be recreated back when you start Photon again).
* to see logs from the service running on background, use `docker-compose logs`. Run `docker-compose logs --help` for more help on other parameters.
