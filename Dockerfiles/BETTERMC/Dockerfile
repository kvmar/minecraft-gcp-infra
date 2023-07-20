# First stage: downloading zip, unzipping
FROM kubeless/unzip:latest AS builder

WORKDIR /tmp/

# Downloading server-files and unpacking them.
# Since its zip it cannot be unpacked by ADD
ADD https://edge.forgecdn.net/files/4646/921/BMC1_Fabric_1.19.2_Server_Pack%20v19.5.zip BMC1_Fabric_1.19.2_Server_Pack.zip
RUN unzip BMC1_Fabric_1.19.2_Server_Pack.zip

# Second stage: the container
FROM openjdk:8u292-oraclelinux7
COPY --from=builder /tmp/BMC1_Fabric_1.19.2_Server_Pack/ /srv/forge-bmc

WORKDIR /srv/forge-bmc
EXPOSE 25565

#aut-accept EULA
RUN rm eula.txt && echo "eula=true" > eula.txt

RUN yum install screen -y
RUN chmod 744 start.sh
CMD screen -S MC start.sh