# Django Todo App

**Tutorial**: [Deploying Django Apps with Docker: A Step-by-Step Guide](https://betterstack.com/community/guides/scaling-python/dockerize-django/)

![Django todo app screenshot](screenshot.png)

## 🟢 Prerequisites

You must have [Python3](https://www.python.org/downloads/) and [pip](https://pypi.org/project/pip/) installed on your machine. You also need to set up [PostgreSQL](https://www.postgresql.org/download/). This project was tested against the following versions:

- Python 3.10.6
- Pip 22.0.2
- PostgreSQL 14.8

## 📦 Getting started

- Fork this repo to your GitHub account by clicking the **Fork** button.
- Clone the repo to your machine.

```bash
git clone https://github.com/<username>/django-todo-app
```

- [Follow the tutorial](https://betterstack.com/community/guides/scaling-python/dockerize-django/) to learn how to deploy the application using Docker.

- See the [docker](https://github.com/betterstack-community/django-todo-app/tree/docker) branch for the final code.

## ⚖ License

The code used in this project and in the linked tutorial are licensed under the [Apache License, Version 2.0](LICENSE).

## Forked version instructions

Run the following first to get started. 

`mkvirtualenv venv`

A venv must be present when creating the docker container. You cannot rely on virtualenvwrapper when creating a container as the venv lives in the container. 

## Shortcut for creating an image. 

### To be automated via docker compose

Make sure you have a Dockerfile and .dockerignore file.

run `docker build -t django-todo-app .`

Create a network file for talking to containers

`docker run --name <your_postgres_name> -p 5432:5432 -e POSTGRES_USER=<your_postgres_user> -e POSTGRES_PASSWORD=<your_posgres_user_password> --network my-django-postgres-network -d postgres`

Create your DB and users. 

Run `docker pull postgres`

Rename db to whatever you want

Run `docker tag postgres:latest <your_db_image_name>:latest`

Create an .env file with the following parameters

DATABASE_NAME=django_todo
DATABASE_USER=<postgresql_username>
DATABASE_PASSWORD=<postgresql_password>
DATABASE_HOST=<postgresql_db_image_name>
DATABASE_PORT=5432

Run the app container with the network bridge attached.

run `docker --env-file .env run --name django-todo-app-c1 -p 8000:8000 --network my-django-postgres-network -d django-todo-app`

The app should be visible @ http://127.0.0.1:8000/



