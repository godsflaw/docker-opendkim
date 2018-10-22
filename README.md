```
export OPENDKIM_VERSION='2.10.3'
cd ${OPENDKIM_VERSION}
docker build -t godsflaw/opendkim:${OPENDKIM_VERSION} .
docker push godsflaw/opendkim:${OPENDKIM_VERSION}
```
