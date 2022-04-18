# API Gateway - Containers LifeCycle

```
API Gateway
  |
  |- Part 1: Keycloak
  |   |- Keycloak Core: jboss/keycloak
  |   |- Keycloak DB: postgre
  |   |- Keycloak Config: jboss/keycloak + configure-keycloak.sh
  |
  |- Part 2: Kong
  |   |- ...
```

## Part One - Keycloak

* Keycloak DB: passive container (cluster mode ?)
* Keycloak Core: exposes :8180, horizontal scalability, don't apply migrations
* Keycloak Config: single container to run seed/migrate commands automatically

### Update Keycloak Config

Two ways:

* Go to adminer > realm's console > Export (on side bar's bottom)
* Run cli commands in a script, run this script in Keycloak config

First method is rather for production backup (you will see many parameters, hard to make them explanatory and possible troubles after an upgrade).

## Part Two - Kong

* Kong DB: passive container (cluster mode ?)
* Kong Core: exposes :8000, horizontal scalability, don't apply migrations
* Kong Adminer: Konga, exposes :1337
* Kong Config ? : single container to run seed/migrate commands automatically

### Update Keycloak Config

Two ways:

* Go to Konga (:1337) > snapshots > Create snapshot then view snapshot details > Export
* Run cli commands in a script, run this script in Kong config

First method is more readable than Keycloak config. More it is global (all configs Vs not a single realm).

Otherwise, API is pretty simple to use (see [d4rktar/kong-konga-keycloak](https://github.com/d4rkstar/kong-konga-keycloak) `curl` requests to localhost:8001)

**Caution:** Kong snapshots contain plain secrets. This might not be a best practice. Moreover, Keycloak doesn't export those secrets (they're replaced by stars `*****`). To make import work, either replace the value in `realm-export` or update it manully/programmatically.

```javascript
// config/keycloak/realm-export.json
"clientSecret": "**********",

// config/kong/snapshot_X.json
"client_secret": "<plain_secret_value>",
```


