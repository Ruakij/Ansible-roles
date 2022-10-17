FROM golang:1-buster

# Add PPA
RUN echo "deb http://ppa.launchpad.net/dqlite/dev/ubuntu bionic main" > /etc/apt/sources.list.d/ppa_dqlite_dev_bionic.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 50FB3D04
# Install dependencies
RUN apt update -y && apt install -y build-essential git libraft-dev libsqlite3-dev libdqlite-dev

# Clone
RUN git clone https://github.com/canonical/k8s-dqlite --branch v1.0.4 /k8s-dqlite
WORKDIR /k8s-dqlite

# Compile
ENV CGO_LDFLAGS_ALLOW="-Wl,-z,now"
RUN go build -o k8s-dqlite -tags libsqlite3,dqlite k8s-dqlite.go
