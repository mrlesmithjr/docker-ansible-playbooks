#Ubuntu Docker image with Ansible

FROM ubuntu:12.04
#FROM ubuntu:14.04

MAINTAINER mrlesmithjr@gmail.com

RUN apt-get update && apt-get install -y \
  python-pip \
  python-dev \
  sudo \
  && apt-get clean

RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN pip install ansible 

