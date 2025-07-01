# Contenu final et correct pour rocky-ssh/Dockerfile
FROM rockylinux:9

# Installer le serveur SSH et générer les clés d'hôte du serveur
RUN dnf update -y && dnf install -y openssh-server sudo && \
    ssh-keygen -A

# Créer le répertoire .ssh et y copier la clé publique
RUN mkdir -p /root/.ssh && chmod 700 /root/.ssh
COPY rocky-ssh/id_rsa.pub /root/.ssh/authorized_keys
RUN chmod 600 /root/.ssh/authorized_keys && chown root:root /root/.ssh/authorized_keys

# Autoriser la connexion root par SSH
RUN sed -i 's/^#\?PermitRootLogin.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -i 's/^#\?PasswordAuthentication.*/PasswordAuthentication no/' /etc/ssh/sshd_config

# Correction pour les conteneurs systemd
RUN sed -i 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' /etc/pam.d/sshd

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D", "-e"]
