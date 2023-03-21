FROM maven:3.8.6-openjdk-8-slim

RUN apt update && apt upgrade -y && apt autoremove -y
RUN apt install -y --no-install-recommends \
  libfontconfig1-dev \
  libssl-dev \
  wget \
  && apt clean \
  && rm -rf /var/lib/apt/lists/*

RUN mkdir /leos
RUN wget -O - "https://code.europa.eu/leos/core/-/archive/LEOS_3.3.0/core-LEOS_3.3.0.tar.gz" | tar zxvf - -C /leos --strip-components 1

WORKDIR "/leos/tools/user-repo"
RUN mvn clean install --quiet

WORKDIR "/leos/tools/cmis/chemistry-opencmis-server-inmemory"
RUN mvn clean --quiet

WORKDIR "/leos"
ENV OPENSSL_CONF=/dev/null
RUN mvn clean install --quiet

WORKDIR "/leos/tools/akn4euutil"
RUN mvn clean install --quiet

WORKDIR "/leos"
