FROM openjdk:8-jre-slim 

RUN apt-get update \
    && apt-get install -y --no-install-recommends openssl ca-certificates dumb-init \
    && rm -rf /var/lib/apt/lists/* 

#COPY secret.txt /root/secret.txt
#ENTRYPOINT ["/usr/bin/dumb-init", "--"]

