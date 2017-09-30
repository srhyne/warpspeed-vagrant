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

    # browsersync
    config.vm.network :forwarded_port, guest: 3000, host: 3000, auto_correct: true
    config.vm.network :forwarded_port, guest: 3001, host: 3001, auto_correct: true
    # had issues with caching
    config.vm.network :forwarded_port, guest: 3002, host: 3002, auto_correct: true

    config.vm.network :private_network, ip: ip

    # Use this config if you have nfs support (OSX or Linux).
    # Note: You will be required to enter your host root password during "vagrant up".
    # If you get an error on the sync_folder, remove /etc/exports on mac
    config.vm.synced_folder "~/Sites/conveyour.dev", "/home/vagrant/sites/conveyour.dev", type: "nfs", 
    :mount_options => ['rw', 'vers=3', 'tcp', 'fsc' ,'actimeo=2'],
    linux__nfs_options: ['rw','no_subtree_check','all_squash','async']

    config.vm.provider "virtualbox" do |vb|
        vb.name = hostname
        vb.memory = 4096
        vb.cpus = 2
        vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
        vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        vb.customize ["modifyvm", :id, "--ioapic", "on"]
        vb.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/v-root", "1"]
    end
 # Edit the s.args below to determine what installers are called during provisioning.
    config.vm.provision "shell" do |s|
        s.path = "provision.sh"
        s.args = "-h=#{hostname} --nginx --php --python --nodejs --rbenv --beanstalkd --mysql --postgresql --mongodb"
    end



end
