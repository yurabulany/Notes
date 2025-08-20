# Dockerfile

```
ARG NG_VERSION=latest

FROM nginx:${NG_VERSION}

ARG NG_VERSION
ARG ARG_FILE=mytext.txt

ENV NG_VERSION="${NG_VERSION}"

RUN mkdir -p /opt/ && touch /opt/"$ARG_FILE"
```

## Build command

`docker build --build-arg NG_VERSION=stable --build-arg ARG_FILE=myfile.txt -t nginx:innow-dkr-10 .`

## Result video

[Result video](../Videos/docker9.mkv)
