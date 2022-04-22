# First stage: downloading zip, unzipping
FROM kubeless/unzip:latest AS builder

WORKDIR /tmp/

# Downloading server-files and unpacking them.
# Since its zip it cannot be unpacked by ADD
ADD https://edge.forgecdn.net/files/3707/304/Valhelsia%203-3.5.1-SERVER.zip "Valhelsia+3-3.5.1-SERVER.zip"
RUN unzip Valhelsia+3-3.5.1-SERVER.zip -d server

# Second stage: the container
FROM openjdk:18-oraclelinux7
COPY --from=builder /tmp/server/ /srv/forge-val

WORKDIR /srv/forge-val
EXPOSE 25565

RUN chmod 744 ServerStart.sh
RUN echo "eula=true" > eula.txt
RUN yum install screen -y
CMD screen -S MC ./ServerStart.sh