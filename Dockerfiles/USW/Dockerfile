# First stage: downloading zip, unzipping
FROM kubeless/unzip:latest AS builder

WORKDIR /tmp/

# Downloading server-files and unpacking them.
# Since its zip it cannot be unpacked by ADD
ADD https://api.papermc.io/v2/projects/paper/versions/1.19.2/builds/237/downloads/paper-1.19.2-237.jar paper.jar
ADD "https://www.dl.dropboxusercontent.com/s/a5oo98bdiu3bqhx/server_pack.zip?dl=0" server_pack.zip
RUN unzip server_pack.zip

# Second stage: the container
FROM openjdk:17-ea-22-jdk-oraclelinux7
COPY --from=builder /tmp/ /srv/usw

WORKDIR /srv/usw
EXPOSE 25565

#aut-accept EULA
RUN echo "eula=true" > eula.txt
RUN yum install screen -y

CMD screen -S MC java -Xms8048m -Xmx12096m -jar paper.jar nogui