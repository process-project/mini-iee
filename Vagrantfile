IMAGE_NAME = "bento/ubuntu-18.04"

Vagrant.configure("2") do |config|
    config.ssh.insert_key = false

    config.vm.provider "virtualbox" do |v|
        v.memory = 2048
        v.cpus = 2
    end

    config.vm.define "k8s-master" do |master|
        master.vm.box = IMAGE_NAME
        master.vm.network "private_network", ip: "192.168.50.10"
        master.vm.hostname = "k8s-master"

        master.vm.provision "ansible" do |ansible|
            ansible.playbook = "playbooks/master-playbook.yml"
            ansible.extra_vars = {
                node_ip: "192.168.50.10",
            }
        end
        
	master.vm.provision "ansible" do |ansible|
          ansible.playbook = "playbooks/slurm-playbook.yml"
        end

        master.vm.provision "ansible" do |ansible|
          ansible.playbook = "playbooks/iee-playbook.yml"
        end
    end
end
