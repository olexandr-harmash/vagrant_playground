Vagrant.configure("2") do |config|
  
  # Nodes amount
  N = 2

  # Initialize a hash to store host variables
  Host_vars = {}

  # Loop to create N nodes
  (1..N).each do |i|

    # Define each node with a unique name
    config.vm.define "node-#{i}" do |node|

      # Store host variables for each node
      Host_vars["node-#{i}"] = {
        # You can add specific variables here as needed
      }

      # Specify the box to use for the VM
      node.vm.box = "ubuntu/jammy64"

      # Set up synced folders for data sharing
      node.vm.synced_folder "./tdata/node-#{i}/", "/home/vagrant/tdata/"

      # Execute Ansible provisioner only once all machines are up
      if i == N

        node.vm.provision "ansible" do |ansible|

          # Specify which hosts to target
          ansible.limit = "all"

          # Define the Ansible playbook to run
          ansible.playbook = "provisioning/playbook.yml"

          # Pass the host variables to Ansible
          ansible.host_vars = Host_vars

        end

      end

    end

  end

end
