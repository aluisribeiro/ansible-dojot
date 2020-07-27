IMAGE_NAME = "ubuntu/bionic64"
N = 2

Vagrant.configure("2") do |config|
    config.disksize.size = '30GB'
    config.ssh.insert_key = false

    config.vm.provider "virtualbox" do |v|
        v.memory = 6144
        v.cpus = 2
    end
      
    config.vm.define "k8s-master" do |master|
        master.vm.box = IMAGE_NAME
        master.vm.network "private_network", ip: "192.168.50.10"
        master.vm.hostname = "k8s-master"
        master.vm.provision "ansible_local" do |ansible|
            ansible.playbook = "vagrant.yaml"
            ansible.inventory_path = "inventories/example_local"
            ansible.limit = "dojot-k8s"
            ansible.extra_vars = {
                node_ip: "192.168.50.10",
            }
        end
    end

    # (1..N).each do |i|
    #     config.vm.define "node-#{i}" do |node|
    #         node.disksize.size = '20GB'
    #         node.vm.box = IMAGE_NAME
    #         node.vm.network "private_network", ip: "192.168.50.#{i + 10}"
    #         node.vm.hostname = "node-#{i}"
    #         node.vm.provision "ansible" do |ansible|
    #             ansible.playbook = "kubernetes-setup/node-playbook.yml"
    #             ansible.extra_vars = {
    #                 node_ip: "192.168.50.#{i + 10}",
    #             }
    #         end
    #     end
    end