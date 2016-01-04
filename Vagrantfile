# WarpSpeed Vagrant Configuration.

# Visit http://warpspeed.io for complete information.
# (c) Turner Logic, LLC. Distributed under the GNU GPL v2.0.

hostname = "warpspeed-dev"
ip       = "192.168.88.10"

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

    config.vm.box = "ubuntu/trusty64"
    config.vm.hostname = hostname

    # for live reload
    config.vm.network "forwarded_port", guest: 35729, host: 35729

    # for mysql
    config.vm.network "forwarded_port", guest: 3306, host: 3306
    
    # RabbitMQ
    config.vm.network "forwarded_port", guest: 5672, host: 5672
    config.vm.network "forwarded_port", guest: 15672, host: 15672

    # RethinkDB

    # client port
    config.vm.network "forwarded_port", guest: 28015, host: 28015

    # web interface
    config.vm.network "forwarded_port", guest: 8080, host: 8080

    config.vm.network :private_network, ip: ip

    # Use this config if you have nfs support (OSX or Linux).
    # Note: You will be required to enter your host root password during "vagrant up".
    config.vm.synced_folder "~/Sites", "/home/vagrant/sites", type: "nfs", :mount_options => ["actimeo=2"]

    config.vm.provider "virtualbox" do |vb|
        vb.name = hostname
        vb.memory = 2048
        vb.cpus = 1
        vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
        vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        vb.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/v-root", "1"]
    end
 # Edit the s.args below to determine what installers are called during provisioning.
    config.vm.provision "shell" do |s|
        s.path = "provision.sh"
        s.args = "-h=#{hostname} --nginx --php --python --nodejs --rbenv --beanstalkd --mysql --postgresql --mongodb"
    end



end
