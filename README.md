# GeoBlacklight Demo

This is an example GeoBlacklight application. To create your own application built on GeoBlacklight, see [the Quick Start documentation](https://geoblacklight.org/documentation/geoblacklight_quick_start/).

## Developing

[Docker](https://www.docker.com/products/docker-desktop/) is required for development.

You can start both GeoBlacklight and solr via the Rake task:

```sh
bin/rake geoblacklight:server
```

The development and test environments use SQLite.

### Local Production

You can emulate the production environment locally using the compose file.

```sh
docker compose up -d
```

This starts both solr and a PostgreSQL container, which is the database used in production.

Then start the server using Rake as normal:

```sh
bin/rake geoblacklight:server
```

This will leave solr alone, as it's already running.
