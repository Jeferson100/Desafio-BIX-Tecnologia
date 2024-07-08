FROM mcr.microsoft.com/devcontainers/python:1-3.12-bullseye

COPY requirements.txt /tmp/

COPY Makefile /tmp/

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
     && apt-get install -y python3-pip \  
     && pip3 install --no-cache-dir -r /tmp/requirements.txt
