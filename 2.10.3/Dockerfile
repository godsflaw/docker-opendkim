FROM node:8.6.0-alpine
MAINTAINER Christopher Mooney <chris@dod.net>

ENV VERSION="2.10.3"
ENV LOCALDIR="/opendkim-${VERSION}"
ENV SOURCE_URL_BASE="https://downloads.sourceforge.net/project/opendkim"

# install deps
RUN apk upgrade --update && \
  apk add --no-cache --virtual build-base && \
  apk add --no-cache --virtual curl && \
  apk add --no-cache --virtual openssl-dev && \
  apk add --no-cache --virtual libmilter-dev

# drop codebase
RUN mkdir -p ${LOCALDIR}
RUN curl -LO "${SOURCE_URL_BASE}/opendkim-${VERSION}.tar.gz" && \
  curl -LO "http://laurikari.net/tre/tre-0.8.0.tar.gz"

# extract
RUN tar xvfz "tre-0.8.0.tar.gz"
RUN tar xvfz "opendkim-${VERSION}.tar.gz"

# install tre
WORKDIR "/tre-0.8.0"
RUN ./configure && make && make install

# install opendkim
WORKDIR "${LOCALDIR}"
RUN ./configure --with-tre --enable-diffheaders && make && make install

WORKDIR "${LOCALDIR}"
CMD ["tail", "-f", "INSTALL"]
