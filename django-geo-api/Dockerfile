FROM honeycrisp/docker:django-api

RUN apt-get update && apt-get install -y --no-install-recommends \
    gdal-bin \
    python-gdal

RUN pip install --upgrade pip
ADD ./requirements.txt ./requirements.txt
RUN pip install --upgrade -r ./requirements.txt
RUN rm ./requirements.txt