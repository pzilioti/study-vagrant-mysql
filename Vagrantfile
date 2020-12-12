$script_mysql = <<-SCRIPT
  apt-get update && \
  apt-get install -y mysql-server-5.7 && \
  mysql < /vagrant/mysql/user.sql && \
  cat /vagrant/mysql/mysqld.cnf > /etc/mysql/mysql.conf.d/mysqld.cnf && \
  service mysql restart
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = 1024
    vb.cpus = 1
  end

  config.vm.define "mysql" do |mysql|
    mysql.vm.network "forwarded_port", guest: 3306, host: 3306

    mysql.vm.provider "virtualbox" do |vb|
      vb.name = "mysql"
    end

    mysql.vm.provision "shell", inline: $script_mysql
  end

end
