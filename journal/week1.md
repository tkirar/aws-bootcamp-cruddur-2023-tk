# Week 1 — App Containerization

## Run locally on terminal

```sh

cd backend-flask
export FRONTEND_URL="*"
export BACKEND_URL="*"
python3 -m flask run --host=0.0.0.0 --port=4567

```

- From ports check the server url
- append `/api/activities/home`
- you should get back json

## Add Dockerfile

```sh
From python:3.10-slim-buster

# Inside container
WORKDIR /backend-flask

# Outside container -> Inside container
COPY requirements.txt requirements.txt

# Inside Container
RUN pip3 install -r requirements.txt

# Outside container -> Inside container
# . everything in the current directory(outside container) -> in the current directory(inside container)
COPY . .

# Set environment variables in side container and will remain set when container is running
ENV FLASK_ENV=development

EXPOSE ${PPORT}

#CMD (command)
# python3 -m flask run --host=0.0.0.0 --port=4567
CMD [ "python3", "-m" ,"flask", "run", "--host=0.0.0.0", "--port=4567"]
```

## Build Container

```sh
docker build -t backend-flask ./backend-flask
```

## RUN Container
```sh
docker run --rm -p 4567:4567 backend-flask
```
- Make sure to add Environment Variables while running container
  ```sh
  docker run --rm -p 4567:4567 -e FRONTEND_URL="*" -e BACKEND_URL="*" backend-flask
  ```
  - check the ports for server url
  - Make sure it returns json
