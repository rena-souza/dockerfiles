# java-8-selenium-firefox
FROM node:6-alpine

# Configure timezone
RUN apk add --no-cache tzdata
ENV TZ=America/Sao_Paulo

# Add Java 8 based on https://github.com/docker-library/openjdk/blob/e6e9cf8b21516ba764189916d35be57486203c95/8-jdk/alpine/Dockerfile
ENV LANG C.UTF-8
RUN { \
		echo '#!/bin/sh'; \
		echo 'set -e'; \
		echo; \
		echo 'dirname "$(dirname "$(readlink -f "$(which javac || which java)")")"'; \
	} > /usr/local/bin/docker-java-home \
	&& chmod +x /usr/local/bin/docker-java-home
ENV JAVA_HOME /usr/lib/jvm/java-1.8-openjdk
ENV PATH $PATH:/usr/lib/jvm/java-1.8-openjdk/jre/bin:/usr/lib/jvm/java-1.8-openjdk/bin

ENV JAVA_VERSION 8u17
ENV JAVA_ALPINE_VERSION 8.171.11-r0

RUN set -x \
	&& apk add --no-cache \
		openjdk8 \
	&& [ "$JAVA_HOME" = "$(docker-java-home)" ]


# Install phantomjs

RUN set -ex \
  && apk add --no-cache --virtual .build-deps ca-certificates openssl \
  && wget -qO- "https://github.com/dustinblackman/phantomized/releases/download/2.1.1/dockerized-phantomjs.tar.gz" | tar xz -C / \
  && npm install -g phantomjs \
  && apk del .build-deps