# encoding: utf-8
# -*- mode: ruby -*-
# vi: set ft=ruby :# Box / OS


# Nombre de la maquina ( ejm: any-name-01 )
VM_NAME = "vagrant - Ubuntu 18.04 LTS x64"

# No editar
Vagrant.configure(2) do |config|
    
    config.vm.box = "hashicorp/bionic64"
	config.vm.hostname = "vagrant-ubuntu-1804"
    
    config.vm.provider "hyperv" do |v|
        v.vmname = VM_NAME
        v.cpus = 4
        v.memory = 2048
        v.maxmemory = 4096
	end
	
	config.vm.network "private_network", type: "dhcp"

	config.vm.synced_folder "./home", "/home/vagrant", create: true, owner: "vagrant", group: "vagrant"
	
	# Install
    config.vm.provision "shell", inline: <<-SHELL
        mkdir -p projects
        sudo apt-get update
        sudo apt-get install -y git 
        sudo apt-get install git-daemon-run | git-daemon-sysvinit git-doc git-el git-email git-gui gitk gitweb git-cvs git-mediawiki git-svn
        
        curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
        sudo apt-get install -y nodejs
        sudo apt-get install -y build-essential
        sudo npm install -y -g npm npx
        
        sudo apt-get install -y gnupg gcc g++ make binutils-doc cpp-doc gcc-7-locales debian-keyring g++-multilib g++-7-multilib gcc-7-doc libstdc++6-7-dbg gcc-multilib autoconf automake libtool flex bison gdb gcc-doc gcc-7-multilib libgcc1-dbg libgomp1-dbg libitm1-dbg libatomic1-dbg libasan4-dbg liblsan0-dbg libtsan0-dbg libubsan0-dbg libcilkrts5-dbg libmpx2-dbg libquadmath0-dbg glibc-doc bzr libstdc++-7-doc make-doc autoconf-archive gnu-standards autoconf-doc gettext bison-doc bzr-doc bzrtools python-bzrlib.tests flex-doc lib32stdc++6-7-dbg libx32stdc++6-7-dbg gdb-doc libtool-doc gfortran | fortran95-compiler gcj-jdk m4-doc python-bzrlib-dbg python-kerberos python-paramiko python-pycurl xdg-utils python-configobj-doc python-cryptography-doc python-cryptography-vectors python-dbus-dbg python-dbus-doc python-enum34-doc python-gi-cairo gnome-keyring libkf5wallet-bin gir1.2-gnomekeyring-1.0 python-fs python-gdata python-keyczar python-testresources python-setuptools python-secretstorage-doc

        wget -qO - https://www.mongodb.org/static/pgp/server-4.2.asc | sudo apt-key add -
        echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.2.list
        sudo apt-get install -y mongodb-org
        sudo service mongod start
        sudo service mongod status

        sudo npm install -g -y @vue/cli
        sudo npm install -g -y typescript
        
        apt-get update
        apt-get upgrade -y
        apt-get autoremove -y

        cd projects
        git clone https://github.com/Azure-Samples/nodejs-docs-hello-world.git
        cd nodejs-docs-hello-world
        npm i

        ip addr show eth0 | grep 'inet ' | awk '{print $2}' | cut -f1 -d'/'
    SHELL
end

# vagrant up
# # vagrant up --provision
# vagrant ssh
# vagrant halt
