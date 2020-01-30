# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.ssh.insert_key = false
  config.ssh.private_key_path = ["~/.vagrant.d/insecure_private_key"]
  config.vm.network "forwarded_port", guest: 27017, host: 27017, host_ip: "127.0.0.1" # mongodb
  config.vm.network "forwarded_port", guest: 4200, host: 4200, host_ip: "127.0.0.1" # angular app
  config.vm.network "forwarded_port", guest: 8000, host: 8000, host_ip: "127.0.0.1" # web services
  config.vm.network "forwarded_port", guest: 8080, host: 8080, host_ip: "127.0.0.1" # nginx proxy
  config.vm.provider "virtualbox" do |vb|
    # vb.gui = true
    vb.memory = "2048"
    vb.cpus = "2"
    vb.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/vagrant", "1"]
  end
  config.vm.provision "shell", inline: <<-SHELL
    # Configure software sources
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    wget -qO - https://www.mongodb.org/static/pgp/server-4.2.asc | sudo apt-key add -
    echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.2.list
    curl -sL https://deb.nodesource.com/setup_12.x | sudo bash -
    add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    
    # Install software
    apt-get update
    apt-get install -y \
    jq \
    unzip \
    pwgen \
    zsh \
    nodejs \
    mongodb-org \
    redis \
    build-essential \
    apt-transport-https \
    ca-certificates \
    gnupg-agent \
    software-properties-common \
    docker-ce \
    docker-ce-cli \
    containerd.io \
    python3-pip \
    nginx \
    ansible
    pip3 install awscli
    pip3 install jmespath
    curl -L https://storage.googleapis.com/kubernetes-release/release/v1.15.4/bin/linux/amd64/kubectl -o /usr/local/bin/kubectl
    chmod 755 /usr/local/bin/kubectl
    wget https://releases.hashicorp.com/terraform/0.12.7/terraform_0.12.7_linux_amd64.zip -O /tmp/terraform.zip -o /dev/null
    unzip /tmp/terraform.zip -d /usr/local/bin/

    # Configure system
    systemctl enable mongod
    service mongod start
    usermod -a -G docker vagrant

    # Install supplemental tools
    npm install -g gulp mocha typescript tsc-watch @angular/cli stylus nib
  SHELL
end
