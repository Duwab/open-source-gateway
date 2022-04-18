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
* [Kong integrations samples](https://github.com/ncarlier/kong-integration-samples): Kong with multiple integrations (keycloak, elk, InfluxDB)

## Dependencies

| Service | Dependencies |
| --- | --- |
| VueJS | <ul><li>url API (kong)</li><li>url OpenID server</li><li>Callback for standard [***Code Flow***](https://openid.net/specs/openid-connect-basic-1_0.html#CodeFlow) (keycloak adds guard then read+send code to get token)</li></ul> |
| Keycloak | <ul><li>1 realm (per site), with multiple providers</li><li>Client for VueJS</li><li>Client for Kong</li><li>Build with custom theme</li><li>Seed: demo user, admin user</li></ul> |
| Kong | <ul><li>oidc plugin</li><li>plugin "instance" with Keycloak url + token (should be same as front)</li><li>Routings to µservices</li></ul> |
| µservices | <ul><li>network aliases between each other</li><li>handle possible access by API Gateway</li></ul> |


This should give the big picture (maybe think adding nginx to "mock" VPC entry point)

Then other µservices are supposed to be added grouped by projects into submodules (they should work independently of all of this)

### Use cases

* Projects bootstraping
* Day-to-day Development
* Testing (e2e) and QA environments setup
* Production recovery/re-install


## Getting started

```
docker compose up    # details to init in start.sh
cd apps/vuejs-demo
npm run serve
```

- Keycloack admin: http://localhost:8180/admin/master/console
- Konga: http://localhost:1337/#!/plugins
- Kong API Gateway: http://localhost:8000
- Kong Admin API: http://localhost:8001
- VueJS: http://localhost:8080

## Objectives

- [ ] Project init made simple: `git clone && docker compose up && curl http://localhost:8080`
- [ ] Project update made simple:
  - [ ] `git pull && migrate`
  - [ ] `git pull && restore`
- [ ] Submodules as solutions containing multiple µservices
  - [ ] Demo gRPC with 2 go services
  - [ ] Doc to add another service
  - [ ] Update made simple (project/submodule level):
    - [ ] migrate
    - [ ] restore
- [ ] Structure by solutions (Gateway, solution1(go1, go2), solution2(submodule))
