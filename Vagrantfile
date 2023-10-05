Vagrant.configure("2") do |config|

  #Configurações globais
  config.vm.box_check_update = true 

  #Configurações Server 01
  config.vm.define "webserver" do |webserver| 
    webserver.vm.box = "ubuntu/trusty64" #Box do Vagrant
    webserver.vm.hostname = "anderson-cliente" #Hostname do servidor
    webserver.vm.box_download_insecure=true  #Permitir conexão insegura
    webserver.vm.network "private_network", ip: "192.168.5.2" # Configuração de interface de rede
    webserver.vm.network "forwarded_port", guest: 80, host: 8080, id: "nginx" # Porta 80 da máquina virtual para a porta 8080 da máquina local
    webserver.vm.synced_folder "./shared_windows", "/shared_linux", SharedFoldersEnableSymlinksCreate: false # Configurações do Diretorio Compartilhado
    webserver.vm.provider "virtualbox" do |vb|  # Configurações do Provider
        vb.memory = 1024 
        vb.cpus = 1
    end
    webserver.vm.provision "shell", inline: <<-SHELL
      sudo apt-get update
      sudo apt-get install -y curl vim htop
    SHELL
  end

  #Configurações Server 02
  config.vm.define "docker" do |docker| 
    docker.vm.box = "centos/7" #Box do Vagrant
    docker.vm.hostname = "anderson-docker" #Hostname do servidor
    docker.vm.box_download_insecure=true  #Permitir conexão insegura
    docker.vm.network "private_network", ip: "192.168.5.3" # Configuração de interface de rede 
    docker.vm.provider "virtualbox" do |vb| # Configurações do Provider
        vb.memory = 1024
        vb.cpus = 2
    end
    docker.vm.provision "shell", path: "install_docker.sh"    
  end
end