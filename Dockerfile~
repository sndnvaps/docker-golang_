FROM buildpack-deps:jessie-scm

# gcc for cgo
RUN apt-get update && apt-get install -y --no-install-recommends \
		g++ \
		gcc \
		libc6-dev \
		make \
		wget \
	&& rm -rf /var/lib/apt/lists/*

ENV GOLANG_VERSION 1.5.1
ENV GOLANG_TAR_BALL go$GOLANG_VERSION.linux-amd64.tar.gz
ENV GOLANG_DOWNLOAD_URL https://golang.org/dl/$GOLANG_TAR_BALL
ENV GOLANG_DOWNLOAD_SHA1 46eecd290d8803887dec718c691cc243f2175fe0

RUN wget $GOLANG_DOWNLOAD_URL  \
	&& echo "$GOLANG_DOWNLOAD_SHA1  $GOLANG_TAR_BALL" | sha1sum -c - \
	&& tar -C /usr/local -xzf $GOLANG_TAR_BALL \
	&& rm $GOLANG_TAR_BALL

ENV GOPATH /go
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH

RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R 777 "$GOPATH"
WORKDIR $GOPATH

COPY go-wrapper /usr/local/bin/
