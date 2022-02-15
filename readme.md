# Snykii

Pronounced:
> \\ `snē-kē` \\

A simple `docker-compose` for testing image contents using [Snyk](https://snyk.io).

## setup

``` sh
# make snykii directory
mkdir snykii && cd snykii

# copy resources
uri=https://raw.githubusercontent.com/rjchicago/snykii/master/
curl ${uri}docker-compose.yml -o docker-compose.yml

# edit .env with your SNYK_TOKEN
echo "SNYK_TOKEN=<SNYK_TOKEN>" > .env
vi .env
```

## usage

``` sh
# set IMAGE variable
export IMAGE=${IMAGE}

# compose up
docker-compose up -d
docker exec -it snyk sh
```

### example tests

#### basic testing

``` sh
# test current folder
snyk test

# include dev dependencies
snyk test --dev

# test all manifest in current folder and subfolder
snyk test --all-projects
```

#### testing a jar with maven

``` sh
# install maven
apk add --update maven

# tests...
snyk test --scan-all-unmanaged
snyk log4shell
```

> See [docs](https://docs.snyk.io/products/snyk-open-source/language-and-package-manager-support) for additional language support.

## cleanup

``` sh
# compose down
docker-compose down
docker volume rm snykii_data
```
