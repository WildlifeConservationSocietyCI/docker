# docker
Repository for WCS CI docker images

## django
    docker build -f Dockerfile --rm --no-cache .
    docker login -u honeycrisp
    docker tag <image id> honeycrisp/docker:django-api
    docker tag <image id> honeycrisp/docker:django-geo-api
    docker push honeycrisp/docker:django-api
    docker push honeycrisp/docker:django-geo-api
    ...
    FROM honeycrisp/docker:django-geo-api
    ...
