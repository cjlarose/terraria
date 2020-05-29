FROM ubuntu:14.04.4 AS builder

MAINTAINER Christian Oelsner <c.oelsner@web.de>

WORKDIR /opt

RUN apt-get update && apt-get install -y unzip 

ADD https://terraria.org/system/dedicated_servers/archives/000/000/038/original/terraria-server-1404.zip terraria-server.zip

RUN unzip terraria-server.zip "1404/Linux/*" \
  && chmod -R a+rw 1404/Linux/* \
  && chmod a+x 1404/Linux/TerrariaServer* \
  && mv 1404/Linux terraria/

# Stage 2
FROM ubuntu:14.04.4

WORKDIR /opt/terraria

COPY --from=builder /opt/terraria .

VOLUME ["/world"]
EXPOSE 7777

ADD serverconfig.txt .

ENTRYPOINT ./TerrariaServer -x64 -config serverconfig.txt
