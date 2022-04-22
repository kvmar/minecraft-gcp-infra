# First stage: downloading zip, unzipping
FROM kubeless/unzip:latest AS builder

WORKDIR /tmp/

# Downloading server-files and unpacking them.
# Since its zip it cannot be unpacked by ADD
ADD https://edge.forgecdn.net/files/3723/369/Valhelsia%20Enhanced%20Vanilla-1.1.2-SERVER.zip "Valhelsia+Enhanced+Vanilla-1.1.2-SERVER.zip"
RUN unzip Valhelsia+Enhanced+Vanilla-1.1.2-SERVER.zip -d server

# Second stage: the container
FROM openjdk:18
COPY --from=builder /tmp/server/ /srv/forge-val

WORKDIR /srv/forge-val
EXPOSE 25565

RUN chmod 744 ServerStart.sh
RUN echo "eula=true" > eula.txt
RUN yum install screen -y
CMD screen -S MC ./ServerStart.sh