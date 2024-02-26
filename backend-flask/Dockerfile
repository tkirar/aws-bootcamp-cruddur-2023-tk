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
