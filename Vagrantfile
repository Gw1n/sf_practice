Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/jammy64"

  config.vm.network "forwarded_port", guest: 5432, host: 5432

  config.vm.provision "shell", inline: <<-SHELL
    
    sudo apt-get update

    sudo apt-get install -y postgresql-16

    sudo sed -i "s/#listen_addresses = 'localhost'/listen_addresses = '*'/" /etc/postgresql/16/main/postgresql.conf

    echo "host	all	all	0.0.0.0/0	scram-sha-256" | sudo tee -a /etc/postgresql/16/main/pg_hba.conf

    sudo -u postgres psql -c "ALTER USER postgres WITH PASSWORD 'vagran';"
    
    sudo service postgresql restart
  SHELL
end
