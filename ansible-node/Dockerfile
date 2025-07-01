# Contenu final pour ansible-node/Dockerfile

FROM ubuntu:22.04

# AJOUTÉ : Empêche les dialogues interactifs pendant le build
ENV DEBIAN_FRONTEND=noninteractive

# Installer les dépendances et Ansible
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    software-properties-common \
    sshpass \
    openssh-client \
    gnupg && \
    add-apt-repository --yes --update ppa:ansible/ansible && \
    apt-get install -y ansible && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Installer le serveur SSH pour que le conteneur reste actif
RUN apt-get update && apt-get install -y openssh-server && \
    mkdir -p /var/run/sshd && \
    mkdir -p /root/.ssh && \
    chmod 700 /root/.ssh

# Copier la clé privée pour se connecter aux clients Ubuntu
COPY ubuntu-ssh/id_rsa /root/.ssh/id_rsa_ubuntu
RUN chmod 600 /root/.ssh/id_rsa_ubuntu

# Copier la clé privée pour se connecter aux clients Rocky
COPY rocky-ssh/id_rsa /root/.ssh/id_rsa_rocky
RUN chmod 600 /root/.ssh/id_rsa_rocky

# Exposer le port SSH (optionnel, mais bonne pratique)
EXPOSE 22

# Commande pour garder le conteneur en vie
CMD ["/usr/sbin/sshd", "-D"]
