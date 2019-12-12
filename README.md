# Rasa Docker Local

This project allows you to use Docker compose to run an existing Rasa project with **Rasa X** and **[Mr. Bot](https://github.com/botfront/rasa-webchat)**.

From the existing rasa root directory:

```
git clone https://github.com/rgstephens/rasa-docker-local docker-local
```

You should check the following:

* Update the [rasa-sdk](https://hub.docker.com/r/rasa/rasa-sdk/tags) version in `docker-compose.yml` and `Dockefile.app` if needed.
* If your action agent is not in the `actions` directory, update the location in the `docker-compose.yml`
* When running `build` command lookup latest [rasa-x](https://hub.docker.com/u/rasa) version first and replace in command.

```
cp docker-local/docker-compose.yml .
docker run -v $(pwd):/app rasa/rasa:1.5.2-full train
docker-compose build --no-cache --build-arg RASA_X_VERSION=0.23.3
docker-compose up -d
docker-compose logs | grep password  # to get the Rasa X password
```

* Browse to http://localhost:5002 for Rasa X
* Browse to http://localhost:8080 for Mr. Bot (if enabled in `docker-compose.yml`)

To get around the Mr. Bot links opening tab issue, build Mr. Bot with this command:

```
docker-compose -f docker-compose.yml build --no-cache --build-arg RASA_X_VERSION=0.23.3 --build-arg REPO=https://github.com/rgstephens/rasa-webchat --build-arg BRANCH=links-open-tab
```

## Version Updates

Version information is kept for `rasa`, `rasa-x` and `rasa-sdk`. To upgrade, change the version in the following files:

| File                      | Images                            |
| ------------------------- | --------------------------------- |
| docker-compose.yml        | rasa-sdk                          |
| Dockerfile.rasax          | Version passed as build parameter |
| Dockerfile.app (optional) | rasa-sdk                          |


## ToDo

* Assign images for Rasa and Mr. Bot names so they can be shared across projects
