# First stage: downloading zip, unzipping
FROM kubeless/unzip:latest AS builder

WORKDIR /tmp/

# Downloading server-files and unpacking them.
# Since its zip it cannot be unpacked by ADD
ADD https://edge.forgecdn.net/files/3579/961/RAD-Serverpack-1.49.zip RAD-Serverpack-1.49.zip
RUN unzip RAD-Serverpack-1.49.zip

# Second stage: the container
FROM openjdk:8u292-oraclelinux7
COPY --from=builder /tmp/RAD-Serverpack-1.4.9/ /srv/forge-rad

WORKDIR /srv/forge-rad
EXPOSE 25565

#aut-accept EULA
RUN rm eula.txt && echo "eula=true" > eula.txt

RUN chmod 744 LaunchServer.sh
CMD java -Xms8048m -Xmx12096m -XX:PermSize=256m -jar forge-1.12.2-14.23.5.2859.jar nogui