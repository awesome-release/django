## Verified to work in Release
This project was derived from the Django project in [awesome-compose](https://github.com/docker/awesome-compose)

In order to make this project work in Release, we had to allow hosts on * in app/example/settings.py on line 37. This allows incoming connections from any host.

To make this project run in [Release](https://releaseapp.io), simply create a new application with this repository.

## Compose sample application
### Django application in dev mode

Project structure:
```
.
├── docker-compose.yml
├── app
    ├── Dockerfile
    ├── requirements.txt
    └── manage.py

```

[_docker-compose.yml_](docker-compose.yml)
```
services: 
  web: 
    build: app 
    ports: 
      - '8000:8000'
```

## Deploy with docker-compose

```
$ docker-compose up -d
Creating network "django_default" with the default driver
Building web
Step 1/6 : FROM python:3.7-alpine
...
...
Status: Downloaded newer image for python:3.7-alpine
Creating django_web_1 ... done

```

## Expected result

Listing containers must show one container running and the port mapping as below:
```
$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                    NAMES
3adaea94142d        django_web          "python3 manage.py r…"   About a minute ago   Up About a minute   0.0.0.0:8000->8000/tcp   django_web_1
```

After the application starts, navigate to `http://localhost:8000` in your web browser:

Stop and remove the containers
```
$ docker-compose down
```
