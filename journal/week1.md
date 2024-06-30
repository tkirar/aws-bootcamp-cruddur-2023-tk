# Week 1 — App Containerization

## TEST RUN BACKEND locally on terminal

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

```dockerfile
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

## Build backend-flask Container

```sh
docker build -t backend-flask ./backend-flask
```

## RUN backend-flask Container
```sh
docker run --rm -p 4567:4567 backend-flask
```
- Make sure to add Environment Variables while running container
  ```sh
  docker run --rm -p 4567:4567 -e FRONTEND_URL="*" -e BACKEND_URL="*" backend-flask
  ```
  - check the ports for server url
  - Make sure it returns json

## TEST RUN FRONTEND locally on terminal

```sh

cd frontend-react-js
npm install
npm start

```

## Create DOCKERFILE
Dockerfile should be created in : `frontend-react-js/Dockerfile`

```dockerfile
FROM node:16.18

ENV PORT=3000

COPY . /frontend-react-js
WORKDIR /frontend-react-js
RUN npm install
EXPOSE ${PORT}
CMD ["npm", "start"]
```


## Build frontend-react-js Container

```sh
docker build -t frontend-react-js ./frontend-react-js
```

##  Run Multiple Containers

### Create a docker-compose file

Create `docker-compose.yml` at the root of the project

```yaml
version: "3.8"
services:
  backend-flask:
    environment:
      FRONTEND_URL: "https://3000-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}"
      BACKEND_URL: "https://4567-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}"
    build: ./backend-flask
    ports:
      - "4567:4567"
    volumes:
      - ./backend-flask:/backend-flask
  frontend-react-js:
    environment:
      REACT_APP_BACKEND_URL: "https://4567-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}"
    build: ./frontend-react-js
    ports:
      - "3000:3000"
    volumes:
      - ./frontend-react-js:/frontend-react-js

# the name flag is a hack to change the default prepend folder
# name when outputting the image names
networks: 
  internal-network:
    driver: bridge
    name: cruddur
```

##  Bring up multiple Containers

```sh
Docker compose up
```
