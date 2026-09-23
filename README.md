# GeoBlacklight Demo

This is an example GeoBlacklight application. To create your own application built on GeoBlacklight, see [the Quick Start documentation](https://geoblacklight.org/documentation/geoblacklight_quick_start/).

## Developing

[Docker](https://www.docker.com/products/docker-desktop/) is required for development.

You can start both GeoBlacklight and Solr via the Rake task:

```bash
bin/rake geoblacklight:server
```

The task starts a Solr container using the config in the compose file, if one is not already running.

The database used in development and test is SQLite.

### Local Production

You can emulate the full production environment locally using the compose file.

```bash
docker compose up -d
```

This starts both Solr and a PostgreSQL container, which is the database used in production.

Then start the server using Rake, specifying the production environment:

```bash
RAILS_ENV=production bin/rake geoblacklight:server
```
