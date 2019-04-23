# -*- mode: ruby -*-
# vi: set ft=ruby :

# unless Vagrant.has_plugin?("vagrant-docker-compose")
#   system("vagrant plugin install vagrant-docker-compose")
#   puts "Dependencies installed, please try the command again."
#   exit
# end

exposed_ports = [3000, 9090, 9093, 9100, 8080, 5000, 9000]

$script = <<-SCRIPT
apt-get update  --quiet
apt-get install docker.io -y  --quiet
mkdir /work
git clone --quiet https://github.com/vbichov/prometheus.git /work
pushd /work
curl -Ls https://github.com/docker/compose/releases/download/1.24.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
docker-compose up -d
SCRIPT


Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-18.04"
  exposed_ports.each do | port|
    config.vm.network "forwarded_port", guest: port , host: port
  end


  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
    vb.cpus = "2"
  end

  config.vm.provision "shell", inline: $script, privileged: true
 
end
