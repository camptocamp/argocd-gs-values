## HELM chart

Values to be used with the [helm-secrets](https://github.com/camptocamp/helm-secrets) chart version 1.2 and upper, aliased as `secrets`.

## Docker registry

The `values-docker-registry*.yaml` files initialize the Docker registry with the shared key vault.

## Security

The `values-docker-security.yaml` file provide security context for the pods and containers.

## Database

The `values-db-main.yaml` file fill the secret for the database connection using the shared key vault if the database is named `main`.

The `values-db-gmf.yaml` file fill the secret for the database connection using the shared key vault if the database is named `gmf`.

The `values-db-merginmaps.yaml` file fill the secret for the database connection using the shared key vault if the database is named `merginmaps`.

In your values you should add:

```yaml
app:
  externalSecrets:
    app:
      secretStoreRef:
        name: gmf-<project>-(int|prod)
```

In your container you can used the following environment variables:

```yaml
env:
  PGHOST:
    type: secret
    name: secrets
    key: PGHOST
  PGHOST_SLAVE:
    type: secret
    name: secrets
    key: PGHOST_SLAVE
  PGPORT:
    type: secret
    name: secrets
    key: PGPORT
  PGPORT_SLAVE:
    type: secret
    name: secrets
    key: PGPORT_SLAVE
  PGDATABASE:
    type: secret
    name: secrets
    key: PGDATABASE
  PGUSER:
    type: secret
    name: secrets
    key: PGUSER
  PGPASSWORD:
    type: secret
    name: secrets
    key: PGPASSWORD
```
