Vagrant.configure("2") do |config|
    # Especificar la box a nivel global
    config.vm.box = "ubuntu/jammy64"
  
    # Configuración para la máquina web1
    config.vm.define "web1" do |web1|
      web1.vm.hostname = "web1"
      web1.vm.network "private_network", ip: "192.168.33.10"
      web1.vm.provider "virtualbox" do |vb|
        vb.memory = 512
        vb.cpus = 1
      end
      web1.vm.synced_folder "./web1", "/var/www/html"
      web1.vm.provision "shell", inline: <<-SHELL
        apt update
        apt install -y apache2
        systemctl enable apache2
        systemctl restart apache2
      SHELL
    end
  
    # Configuración para la máquina web2
    config.vm.define "web2" do |web2|
      web2.vm.hostname = "web2"
      web2.vm.network "private_network", ip: "192.168.33.11"
      web2.vm.provider "virtualbox" do |vb|
        vb.memory = 512
        vb.cpus = 1
      end
      web2.vm.synced_folder "./web2", "/var/www/html"
      web2.vm.provision "shell", inline: <<-SHELL
        apt update
        apt install -y apache2
        systemctl enable apache2
        systemctl restart apache2
      SHELL
    end
  
    # Configuración para el balanceador de carga
    config.vm.define "load-balancer" do |lb|
      lb.vm.hostname = "load-balancer"
      lb.vm.network "private_network", ip: "192.168.33.12"
      lb.vm.provider "virtualbox" do |vb|
        vb.memory = 512
        vb.cpus = 1
      end
      lb.vm.provision "shell", inline: <<-SHELL
        apt update
        apt install -y nginx
        cp /vagrant/nginx/nginx.conf /etc/nginx/nginx.conf
        systemctl enable nginx
        systemctl restart nginx
      SHELL
    end
end
  