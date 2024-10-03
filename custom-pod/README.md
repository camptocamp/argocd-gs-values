## HELM chart

Values to be used with the [helm-custom-pod](https://github.com/camptocamp/helm-custom-pod) chart version 2 and upper, aliased as `app`.

## Docker registry

The `values-docker-registry*.yaml` files initialize the Docker registry with the shared key vault.

## Security

The `values-docker-security.yaml` file provide security context for the pods and containers.

## Database

The `values-db-main.yaml` file fill the secret for the database connection using the shared key vault if the database is named `main`.

In your container you can used the following environment variables:

```yaml
env:
  PGHOST:
    type: secret
    name: self-external-secret-app
    key: PGHOST
  PGHOST_SLAVE:
    type: secret
    name: self-external-secret-app
    key: PGHOST_SLAVE
  PGPORT:
    type: secret
    name: self-external-secret-app
    key: PGPORT
  PGPORT_SLAVE:
    type: secret
    name: self-external-secret-app
    key: PGPORT_SLAVE
  PGDATABASE:
    type: secret
    name: self-external-secret-app
    key: PGDATABASE
  PGUSER:
    type: secret
    name: self-external-secret-app
    key: PGUSER
  PGPASSWORD:
    type: secret
    name: self-external-secret-app
    key: PGPASSWORD
```

## GitHub authentication from c2cwsgiutils

The `values-c2c-auth*.yaml` files fill the secret for the GitHub authentication using [c2cwsgiutils](https://github.com/camptocamp/c2cwsgiutils) from the shared key vault.

To use is use the following environment variables, common:

```yaml
env:
  C2C_AUTH_GITHUB_REPOSITORY:
    value: camptocamp/<name>
  C2C_AUTH_GITHUB_ACCESS_TYPE:
    value: push
  C2C_AUTH_GITHUB_CLIENT_ID:
    type: secret
    name: self-external-secret-shared
    key: C2C_AUTH_GITHUB_CLIENT_ID
  C2C_AUTH_GITHUB_CLIENT_SECRET:
    type: secret
    name: self-external-secret-shared
    key: C2C_AUTH_GITHUB_CLIENT_SECRET
  C2C_AUTH_GITHUB_SECRET:
    type: secret
    name: self-external-secret-shared
    key: C2C_AUTH_GITHUB_SECRET
```

int:

```yaml
env:
  C2C_AUTH_GITHUB_PROXY_URL:
    value: https://geoservices-int.camptocamp.com/redirect
```

prod:

```yaml
env:
  C2C_AUTH_GITHUB_PROXY_URL:
    value: https://geoservices.camptocamp.com/redirect
```

You should also use the [helm-mutualize](https://github.com/camptocamp/helm-mutualize) chart to configure the redirect proxy, with:

```yaml
mutualize:
  environment: int
  config:
    enabled: true
    redirectConfigs:
      hosts:
        main: <my-host-name>
```
