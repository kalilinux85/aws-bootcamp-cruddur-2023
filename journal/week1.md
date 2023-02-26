# Week 1 — App Containerization

## Dockerizing Backend 

started with running puython 

```
cd backend-flask
export FRONTEND_URL="*"
export BACKEND_URL="*"
python3 -m flask run --host=0.0.0.0 --port=4567
cd ..

```
- Dont forget to unlocj the port on port tab 
- click on 4567 link on the browser 
- add the following to the link ```/api/activities/home```
- you should get back json 
