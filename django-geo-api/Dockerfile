FROM honeycrisp/docker:django-api

RUN echo 'deb http://apt.postgresql.org/pub/repos/apt/ stretch-pgdg main' >  /etc/apt/sources.list.d/pgdg.list
RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -
RUN apt-get update && apt-get install -y --no-install-recommends \
    postgis \
    gdal-bin \
    python-gdal

RUN pip install --upgrade pip
ADD ./requirements.txt ./requirements.txt
RUN pip install --upgrade -r ./requirements.txt
RUN rm ./requirements.txt