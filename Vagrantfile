Vagrant.configure("2") do |config|

    # main & default: normal OS series...
    config.vm.define "main", primary: true do |node|
        node.vm.box = "ubuntu/trusty64"
        #node.vm.box = "ubuntu/precise64"
        ####node.vm.box = "debian/jessie64"
        #node.vm.box = "debian/wheezy64"
        #node.vm.box = "chef/centos-7.1"
        #node.vm.box = "chef/centos-6.6"

        node.vm.provision "ansible" do |ansible|
            ansible.playbook = "test.yml"
            #ansible.sudo = true
            ansible.verbose = "vvv"
        end
    end


    # docker: for auto build & testing (e.g., Travis CI)
    config.vm.define "docker" do |node|
        node.vm.box = "williamyeh/ubuntu-trusty64-docker"

        node.vm.provision "shell", inline: <<-SHELL
            cd /vagrant
            docker build  -f test/Dockerfile-ubuntu14.04  -t fluentd_trusty   .
            docker build  -f test/Dockerfile-ubuntu12.04  -t fluentd_precise  .
            ####docker build  -f test/Dockerfile-debian8      -t fluentd_jessie   .
            docker build  -f test/Dockerfile-debian7      -t fluentd_wheezy   .
            docker build  -f test/Dockerfile-centos7      -t fluentd_centos7  .
            docker build  -f test/Dockerfile-centos6      -t fluentd_centos6  .
        SHELL
    end

end

