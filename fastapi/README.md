## FastAPI App

create FastAPI app using the docs - https://fastapi.tiangolo.com/#create-it

 - create virtual python env:  ```python -m venv .venv```
 - activate env: ```source .venv/bin/activate```
 - pip install fastapi ```pip install fastapi```
 - pip install uvicorn ```pip install uvicorn```
 - create main.py (https://fastapi.tiangolo.com/#create-it)
 - run app locally: ```uvicorn main:app --reload```
 - test app locally: ```http://127.0.0.1:8000/```
 - stop local uvicorn

## Docker

containerize the app - https://fastapi.tiangolo.com/deployment/docker/

 - create Dockerfile (https://fastapi.tiangolo.com/deployment/docker/)
 - build docker image with tag: ```docker build -t k8s-fast-api .```
 - run container forwarding port: ```docker run -p 8000:80 k8s-fast-api```
 - test app locally: ```http://127.0.0.1:8000/```
 - create Dockerhub repo (called: fast-api-k8s)
 - build and tag with new Dockerhub tag ```docker build -t jimcr/fast-api-k8s:0.0.1 .```
 - docker login, and push to Dockerhub: ```docker push jimcr/fast-api-k8s:0.0.1```