FROM oraclelinux:9-slim

LABEL version="oraclelinux:9-slim" \
      description="Totvs DbAccess" \
      maintainer="Eduardo Brust <eduardobrust@gmail.com>"

# Ativa repositórios necessários e instala os pacotes
RUN microdnf install -y oraclelinux-release-el9 && \
    microdnf install -y gzip tar procps util-linux && \
    microdnf clean all && \
    rm -rf /var/cache/yum

COPY dbaccess.tgz /tmp/

RUN mkdir -p /totvs && \
    tar -xzf /tmp/dbaccess.tgz -C /totvs && \
    rm /tmp/dbaccess.tgz && \
	chmod -R 755 /totvs && \
	chmod 755 /totvs/dbaccess/multi && \
    chmod 775 /totvs/dbaccess && \
    chmod +x /totvs/dbaccess/multi/dbaccess64 && \
    chmod 664 /totvs/dbaccess/multi/dbaccess.ini

WORKDIR /totvs/dbaccess/multi/

COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
