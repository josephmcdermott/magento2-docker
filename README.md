# Installation

Create this file on your host machine: ~/.composer/auth.json:

```
{
    "http-basic": {
        "repo.magento.com": {
            "username": "MAGENTO_PUBLIC_KEY",
            "password": "MAGENTO_PRIVATE_KEY"
        }
    }
}
```

Next checkout this repository:

```
mkdir project-directory
cd project-directory
git clone xxx .
```

Copy docker-compose.yml.dist to docker-compose.yml:

```
cp docker-compose.yml.dist docker-compose.yml
```

At this stage you can modify docker-compose.yml as you require for your Docker engine.

When you are ready, run the setup:

```
docker-compose run --rm setup
```

Next copy the Magento files to your local for reference:

```
docker cp CONTAINER_NAME:/srv/www ./
```

... replacing CONTAINER_NAME with the appdata container name, use docker-compose ps to find it. It should end with _appdata_1.

Then, uncomment the following in docker-compose.yml:

```
/www/app/code:/srv/www/app/code
```

And finally restart the container:

```
docker-compose up -d app
```

# Magento CLI tool

```
docker exec -it CONTAINER_NAME ./bin/magento
```

... replacing CONTAINER_NAME with the phpfpm container name, use docker-compose ps to find it. It should end with _phpfpm_1.

# Reference

This guide is a simplification of MageInferno:

- https://github.com/mageinferno/magento2-docker-compose
