# Open Source µservices with API Gateway

```

                        VueJS
                          |
                     -------------
                     |           |
  postgre  -----  Keycloak      Kong  -----  postgre
                 (+adminer)  (+adminer)
                                 |
                          ------------------------------------------
                          |            |            |              |
                        nodeJS        mock         go1  <-gRPC->  go2

```

## Base projects

* [Kong/Keycloak Tutorial](https://github.com/d4rkstar/kong-konga-keycloak): a tutorial with a complete backend stack Kong/Konga/Keycloak/postgre_x2/mockbin
* [vue-keycloak plugin](https://github.com/dsb-norge/vue-keycloak-js): based on [keycloack§js adapter](http://www.keycloak.org/docs/latest/securing_apps/index.html#_javascript_adapter), with examples
* [keycloak containers examples](https://github.com/keycloak/keycloak-containers): official repositoryfor Keycloak containers

## Dependencies

| Service | Dependencies |
| --- | --- |
| VueJS | <ul><li>url API (kong)</li><li>url OpenID server</li><li>Callback for xxx flow (keycloak adds guard then read+send code to get token</li></ul> |
| Keycloak | <ul><li>1 realm (per site), with multiple providers</li><li>VueJS client</li><li>Kong Client</li><li>Build with template</li><li>Seed: demo user, admin user</li></ul> |
| Kong | <ul><li>oidc plugin</li><li>plugin "instance" with Keycloak url (should be same as front)</li><li>Routings to µservices</li></ul> |
| µservices | <ul><li>url to other µservices</li><li>gRPC connection between some of them</li></ul> |


This should give the big picture (maybe think adding nginx to "mock" VPC entry point)

Then other µservices are supposed to be added grouped by projects into submodules (they should work independently of all of this)

### Use cases

* Projects bootstraping
* Day-to-day Development
* Testing (e2e) and QA environments setup
* Production recovery/re-install

