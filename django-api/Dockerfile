FROM python:3.8-slim-buster
LABEL maintainer="<sysadmin@datamermaid.org>"

ENV DEBIAN_FRONTEND noninteractive
ENV LANG C.UTF-8
ENV LANGUAGE C.UTF-8
ENV LC_ALL C.UTF-8

RUN apt-get update && apt-get install -y --no-install-recommends \
    gnupg \
    build-essential \
    python3-dev \
    wget \
    vim \
    nano \
    supervisor \
    nginx \
    gunicorn

RUN echo 'deb http://apt.postgresql.org/pub/repos/apt/ buster-pgdg main' >  /etc/apt/sources.list.d/pgdg.list
RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -
RUN apt-get update && apt-get install -y --no-install-recommends \
    postgresql-client-12

RUN pip install --upgrade pip
ADD ./requirements.txt ./requirements.txt
RUN pip install --upgrade -r ./requirements.txt
RUN rm ./requirements.txt

RUN groupadd webapps
RUN useradd webapp -G webapps
RUN mkdir -p /var/log/webapp/ && chown -R webapp /var/log/webapp/ && chmod -R u+rX /var/log/webapp/
RUN mkdir -p /var/run/webapp/ && chown -R webapp /var/run/webapp/ && chmod -R u+rX /var/run/webapp/
ADD ./config/gunicorn.conf /

RUN rm /etc/nginx/sites-enabled/default && rm /etc/nginx/sites-available/default
ADD ./config/webapp.nginxconf /etc/nginx/sites-enabled/

RUN mkdir -p /var/log/supervisor
ADD ./config/supervisor_conf.d/nginx.conf /etc/supervisor/conf.d/
ADD ./config/supervisor_conf.d/webapp.conf /etc/supervisor/conf.d/

EXPOSE 8000 80 443
