# Rasa Docker Local

This project allows you to use Docker compose to run an existing Rasa project.

From the existing rasa root directory:

```
git clone https://github.com/rgstephens/rasa-docker-local docker-local
cp docker-local/docker-compose.yml
docker run -v $(pwd):/app rasa/rasa:1.5.1-full train --augmentation 0 --config docker-compose/config.yml
docker-compose -f docker-compose.yml build --no-cache --build-arg RASA_X_VERSION=0.23.3
docker-compose -f docker-compose.yml up -d
docker-compose -f docker-compose.yml logs | grep password  # to get the Rasa X password
# browse to http://localhost:5002 for Rasa X
# browse to http://localhost:8080 for Mr. Bot
```

To get around the Mr. Bot links opening tab issue, build Mr. Bot with this command:

```
docker-compose -f docker-compose.yml build --no-cache --build-arg RASA_X_VERSION=0.23.3 --build-arg REPO=https://github.com/rgstephens/rasa-webchat --build-arg BRANCH=links-open-tab
```
