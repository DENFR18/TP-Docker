# Vagrantfile
Vagrant.configure("2") do |config|
  # Utilisation d'une image Ubuntu standard
  config.vm.box = "ubuntu/focal64"

  # Configuration du réseau : Ports forwarding
  # Port pour l'application NodeJS (TP Partie 2)
  config.vm.network "forwarded_port", guest: 8080, host: 8080
  # Port pour Wordpress (TP Partie 3)
  config.vm.network "forwarded_port", guest: 8081, host: 8081
  # Port pour PhpMyAdmin (TP Partie 3)
  config.vm.network "forwarded_port", guest: 8082, host: 8082
  # Synchronisation du dossier actuel vers /home/vagrant/tp_docker dans la VM
  config.vm.synced_folder ".", "/home/vagrant/tp_docker"

  # Script de provisioning pour installer Docker et Docker Compose
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y ca-certificates curl gnupg lsb-release
    
    # Installation officielle de Docker
    curl -fsSL https://get.docker.com -o get-docker.sh
    sh get-docker.sh
    
    # Ajout de l'utilisateur vagrant au groupe docker (évite d'utiliser sudo)
    usermod -aG docker vagrant
    
    # Installation de Docker Compose (plugin)
    apt-get install -y docker-compose-plugin
    
    echo "Docker et Docker Compose sont installés !"
  SHELL
end