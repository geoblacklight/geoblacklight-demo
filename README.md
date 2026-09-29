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

Then set up the database:

```bash
RAILS_ENV=production bin/rails db:setup
```

Then precompile assets:

```bash
RAILS_ENV=production bin/rails assets:precompile
```

> [!WARNING]
> If there are files in public/assets, Rails will serve them first in development.
> Before going back to regular development, delete them:
> `bin/rails assets:clobber`

Finally, start the server using Rake, specifying the production environment:

```bash
RAILS_ENV=production bin/rake geoblacklight:server
```

## Deploying

The demo is deployed to `geoblacklight-demo.stanford.edu` with [Kamal](https://kamal-deploy.org).

Container images are published to GitHub's container registry, so you need to set two environment variables. You can put them in a `.env` file in the project root, which is gitignored and loaded by `bin/kamal` (anything you export in your shell takes precedence):

```sh
KAMAL_REGISTRY_USERNAME=your_github_username
KAMAL_REGISTRY_PASSWORD=your_token
```

The token should be a GitHub personal access token (classic) with only the `write:packages` scope, which you can [create here](https://github.com/settings/tokens/new?scopes=write:packages). For more info on creating it, see [this article](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry#authenticating-with-a-personal-access-token-classic).

The database password is stored in Vault at `puppet/application/geoblacklight-demo/demo/postgres_password`, so make sure you log in to Vault first. If Postgres fails to start, it might be because Kamal silently failed to get the password from Vault.

```bash
vault login -method oidc
```

Kamal also can't log in with Kerberos, so run it through `bin/kamal-otk`, which uses your Kerberos ticket to install a one-time SSH key on the server and removes the key when Kamal finishes. Get a ticket first:

```bash
kinit
```

Then use `bin/kamal-otk` wherever you'd use `bin/kamal`. To deploy:

```bash
bin/kamal-otk deploy
```
