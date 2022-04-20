# First stage: downloading zip, unzipping
FROM kubeless/unzip:latest AS builder

WORKDIR /tmp/

# Downloading server-files and unpacking them.
# Since its zip it cannot be unpacked by ADD
ADD https://media.forgecdn.net/files/3530/857/RAD-Serverpack-1.48.zip RAD-Serverpack-1.48.zip
RUN unzip RAD-Serverpack-1.48.zip

# Second stage: the container
FROM openjdk:8u292-oraclelinux7
COPY --from=builder /tmp/RAD-Serverpack-1.48/ /srv/forge-rad

WORKDIR /srv/forge-rad
EXPOSE 25565

#aut-accept EULA
RUN rm eula.txt && echo "eula=true" > eula.txt

RUN chmod 744 LaunchServer.sh
CMD ./LaunchServer.sh