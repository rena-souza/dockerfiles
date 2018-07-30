# java-8-selenium-firefox
FROM alpine:3.8

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
		openjdk8="$JAVA_ALPINE_VERSION" \
	&& [ "$JAVA_HOME" = "$(docker-java-home)" ]


# Install firefox Firefox

RUN echo "http://dl-4.alpinelinux.org/alpine/v3.8/main" >> /etc/apk/repositories && \
	echo "http://dl-4.alpinelinux.org/alpine/v3.8/community" >> /etc/apk/repositories


# RUN apk update && apk add firefox-esr dbus-x11 ttf-freefont xvfb
RUN apk update && \
	apk add --no-cache \
    dbus-x11 \
    dumb-init \
    firefox-esr \
    mesa-gl \
    mesa-dri-swrast \
    ttf-freefont


# Install geckodriver
RUN mkdir /var/driver
COPY ./geckodriver /var/driver
RUN chmod a+x /var/driver/geckodriver

ENV webdriver.gecko.driver=/var/driver/geckodriver


# ENTRYPOINT [ "/usr/bin/dumb-init", "/usr/bin/firefox" ]



