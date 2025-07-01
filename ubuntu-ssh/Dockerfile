# Contenu final pour ubuntu-ssh/Dockerfile
FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

# Installer le serveur SSH et créer le répertoire manquant
RUN apt-get update && apt-get install -y openssh-server sudo && \
    mkdir -p /run/sshd

# Créer le répertoire .ssh et y copier la clé publique
RUN mkdir -p /root/.ssh && chmod 700 /root/.ssh
COPY ubuntu-ssh/id_rsa.pub /root/.ssh/authorized_keys
RUN chmod 600 /root/.ssh/authorized_keys

# Autoriser la connexion root par SSH
RUN echo "PermitRootLogin yes" >> /etc/ssh/sshd_config

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
