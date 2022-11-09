# Quiqup Info

Why fork this repo? We are using M1 Macs in some cases for development, AMD64 emulation of postgres / postgis is ~50% slower in our use case. This repo is a fork with some instructions how to build the docker image on an M1 maching into a multi platform image.

## How? Docker BuildX

Pull from original repo and change the versions to publish updates

### Building

```sh
docker buildx create --name dbuilder --driver docker-container --bootstrap
docker buildx use dbuilder
docker buildx inspect

docker buildx build --platform linux/arm64,linux/amd64 --pull -t europe-west1-docker.pkg.dev/quiqup-infrastructure/public/postgis:15-3.3-alpine --push 15-3.3/alpine

docker buildx imagetools inspect europe-west1-docker.pkg.dev/quiqup-infrastructure/public/postgis:15-3.3-alpine

```

This can be setup to use different machines for each target, but given the frequency we need to update, it can be managed manually on any body with repo access and an M1 machine.
