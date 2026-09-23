# GeoBlacklight Demo

This is an example GeoBlacklight application. To create your own application built on GeoBlacklight, see [the Quick Start documentation](https://geoblacklight.org/documentation/geoblacklight_quick_start/).

## Developing

Run the dependent services via docker compose:

```sh
docker compose up -d
```

Then run GeoBlacklight via the Rake task:

```sh
bin/rake geoblacklight:server
```
