# docker
Repository for WCS CI docker images

## django
    docker build -f Dockerfile --rm --no-cache .
    docker login -u honeycrisp
    docker tag <image id> honeycrisp/django
    docker push honeycrisp/django
    ...
    FROM honeycrisp/django:latest
    ...
