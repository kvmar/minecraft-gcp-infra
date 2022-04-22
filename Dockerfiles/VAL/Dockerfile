# First stage: downloading zip, unzipping
FROM kubeless/unzip:latest AS builder

WORKDIR /tmp/

# Downloading server-files and unpacking them.
# Since its zip it cannot be unpacked by ADD
ADD https://edge.forgecdn.net/files/3723/369/Valhelsia%20Enhanced%20Vanilla-1.1.2-SERVER.zip server.zip
RUN unzip server.zip

# Second stage: the container
FROM openjdk:8u292-oraclelinux7
COPY --from=builder /tmp/server.zip/ /srv/forge-val

WORKDIR /srv/forge-rad
EXPOSE 25565

#aut-accept EULA
RUN rm eula.txt && echo "eula=true" > eula.txt

RUN chmod 744 ServerStart.sh
RUN yum install screen -y
CMD screen -S MC ./ServerStart.sh