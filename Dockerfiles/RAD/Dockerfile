# First stage: downloading zip, unzipping
FROM kubeless/unzip:latest AS builder

WORKDIR /tmp/

# Downloading server-files and unpacking them.
# Since its zip it cannot be unpacked by ADD
ADD https://www.curseforge.com/api/v1/mods/572778/files/4653048/download RAD2-Serverpack-1.5.zip
RUN unzip RAD2-Serverpack-1.5

# Second stage: the container
FROM openjdk:8u292-oraclelinux7
COPY --from=builder /tmp/RAD2-Serverpack-1.5/ /srv/forge-rad

WORKDIR /srv/forge-rad
EXPOSE 25565

#aut-accept EULA
RUN rm eula.txt && echo "eula=true" > eula.txt

RUN chmod 744 LaunchServer.sh
RUN yum install screen -y
CMD screen -S MC java -Xms8048m -Xmx12096m -XX:PermSize=256m -jar forge-1.16.5-36.2.39.jar nogui