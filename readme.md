# Snykii

Pronounced:
> \\ `snē-kē` \\

A simple `docker-compose` for testing image contents using [Snyk](https://snyk.io).

## setup

``` sh
# clone repo
git clone https://github.com/rjchicago/snykii.git && cd snykii

# update .env with your SNYK_TOKEN
cp .env.example .env && vi .env
```

## usage

``` sh
# set IMAGE variable
export IMAGE=${IMAGE}

# compose up & ssh
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
# compose down & rm volume
docker-compose down
docker volume rm snykii_data
```
