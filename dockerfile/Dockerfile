FROM alpine:latest

ENV GLIBC_VERSION 2.29-r0
ENV HFISH_VERSION 0.3

# Download and install glibc
RUN apk update && \
  apk add --no-cache curl tzdata && \
  cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
  curl -Lo /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub && \
  curl -Lo glibc.apk "https://github.com/sgerrand/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}/glibc-${GLIBC_VERSION}.apk" && \
  curl -Lo glibc-bin.apk "https://github.com/sgerrand/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}/glibc-bin-${GLIBC_VERSION}.apk" && \
  apk add glibc-bin.apk glibc.apk && \
  rm -rf glibc.apk glibc-bin.apk /var/cache/apk/*

RUN curl -Lo /tmp/HFish.tar.gz https://github.com/hacklcx/HFish/releases/download/${HFISH_VERSION}/HFish-${HFISH_VERSION}-linux-amd64.tar.gz && \
  tar -zxvf /tmp/HFish.tar.gz -C /tmp && \
  mv /tmp/HFish-${HFISH_VERSION}-linux-amd64 /tmp/HFish && \
  rm -f /tmp/HFish.tar.gz /tmp/HFish/LICENSE /tmp/HFish/README.md

COPY Entrypoint.sh /Entrypoint.sh

RUN chmod +x /Entrypoint.sh

EXPOSE 21 22 23 3306 6379 7879 8080 8989 9000 9001 11211

ENTRYPOINT ["/Entrypoint.sh"]

