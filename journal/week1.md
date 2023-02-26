# Week 1 — App Containerization

## Dockerizing Backend 

started with running python 

```
cd backend-flask
export FRONTEND_URL="*"
export BACKEND_URL="*"
python3 -m flask run --host=0.0.0.0 --port=4567
cd ..

```
- Dont forget to unlock the port on port tab in gitpod 
- click on 4567 link on the browser 
- add the following to the link ```/api/activities/home```
- you should get back json 

## Add DockerFile 

start by creating a new docker file in the following path : ``` backend-flask/Dockerfile```

````

FROM python:3.10-slim-buster

# Inside Container 
# Make a new folder inside the container
WORKDIR /backend-flask

# Outside Container -> Inside Container
#this contains the librairies want to install to run the app
COPY requirements.txt requirements.txt

# Inside Container 
# install the python libraries used for the app
RUN pip3 install -r requirements.txt


#outside container -> Inside container 
# . means everything in the current directory
# First period . - /backend-flask (outside container)
# Second period . - /backend-flask (insid container)
COPY . .


#set environment Variables (Env Vars)
#Inside container and will remain set when the container is running
ENV FLASK_ENV=development

EXPOSE ${PORT}

#cmd (command)
CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0", "--port=4567"]


```

