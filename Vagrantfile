Vagrant.configure("2") do |config|
  config.vm.box = "debian/jessie64"
  config.vm.box_version = "8.11.0"
  #config.disksize.size = '10GB'
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "forwarded_port", guest: 8888, host: 8888
  #config.vm.synced_folder "C:\\HashiCorp\\Vagrant\\bin\\debian\\Folder", "/var/www"

  config.vm.provider "virtualbox" do |vb|
     vb.gui = false
     vb.memory = "2048"
	 vb.name = "debian-test-server"
	 vb.cpus = 2
  end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
   config.vm.provision "shell", inline: <<-SHELL
	sudo apt-get install -y apt-transport-https ca-certificates mc
	sudo wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
	sudo apt-get update
    sudo apt-get install -y vim wget htop tmux nginx apache2
	sudo apt-get install -y php5.6-cli php5.6-curl php5.6-fpm php5.6-gd php5.6-intl php5.6-json php5.6-mbstring php5.6-mcrypt php5.6-pdo-mysql php5.6-xml php5.6-zip libapache2-mod-php5
#	sudo unlink /etc/nginx/sites-enabled/default
#	sudo echo 'include /www*/*/conf/nginx.conf;' > /etc/nginx/sites-enabled/www
#	sudo mkdir -p /www/default/docs /www/default/logs /www/default/conf
	echo '<?php phpinfo();' > /www/default/docs/index.php
	sudo sed -i 's/.*Listen 80.*/Listen 8888/' /etc/apache2/ports.conf
	sudo systemctl restart apache2
	sudo systemctl start nginx
	echo "<?php echo 'HELLO WORLD'; phpinfo(); ?>" > ~/index.php
	sudo mv ~/index.php /var/www/html/index.php
   SHELL
end
