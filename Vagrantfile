Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"

####DB
config.vm.define "db" do |db|
    db.vm.hostname = "database" 
    db.vm.network "private_network", ip: "172.17.177.21"
##Configurações de Size da VM
  db.vm.provider "virtualbox" do |v|
    v.name = "MiniDC-Database"
    v.memory = 512
    v.cpus = 2
  	end
  end

####WEB
config.vm.define "web" do |web|
    web.vm.hostname = "blog"
    web.vm.network "private_network", ip: "172.17.177.22"
##Configurações de Size da VM
  web.vm.provider "virtualbox" do |v|
    v.name = "MiniDC-Blog"
    v.memory = 512
    v.cpus = 2
  	end
  end

####Controller
config.vm.define "controller" do |controller|
    controller.vm.hostname = "database"  
    controller.vm.network "private_network", ip: "172.17.177.11"
##Configurações de Size da VM
#Restringindo o permissionamento da pasta vagrant
  controller.vm.synced_folder "./", "/vagrant", mount_options: ["dmode=750,fmode=600"]
  controller.vm.provider "virtualbox" do |v|
    v.name = "MiniDC-AnsibleController"
    v.memory = 512
    v.cpus = 2
  	end
  ##Integrando o ansible no provisionamento
   config.vm.provision :ansible_local do |ansible|
     ansible.install_mode = "default"
     ansible.playbook = "playbook.yml"
     ansible.inventory_path = "inventory"
     ansible.verbose  = true
     ansible.install  = true
     ansible.limit    = "all"
  		end
  	end
  end
