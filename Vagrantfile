
Vagrant.configure("2") do |config|

  num_of_nodes = 2

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/playbook.yml"
  end

  (1..num_of_nodes).each do |i|

    config.vm.define "machine#{i}" do |machine|
      machine.vm.box = "ubuntu/jammy64"
    end

  end

end
