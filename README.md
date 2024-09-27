# vagrant_playground

## Simple project to play with vagrant and ansible automatization

### Can ban account -><-

**Vagrantfile**
Used ubuntu/jammy64 box with ubuntu 22.04 operation system.

```ruby
  (1..num_of_nodes).each do |i|

    config.vm.define "machine#{i}" do |machine|
      machine.vm.box = "ubuntu/jammy64"
    end

  end
```

Set up ansible provision and describe configuration for machines.

**Up machines**

```bash
  #run playbooks
  vagrant up --provision
  #only run machines
  vagrant up
```

**Stop machines**
```bash
  vagrant halt
```

**Connect via ssh**
```bash
  #vagrant ssh machine{index}
  #index is a number of machine
  vagrant ssh machine1
```

**provisioning**
Folder that consist ansible playbooks and their variables.
It install all python libs for automatization and running scripts. 
```yml
  - name: Обновить список пакетов
      apt:
        update_cache: yes

    - name:
      apt:
        name: python3-pip
        state: present

    - name: Установка или обновление библиотек opentele и telethon
      pip:
        name:
          - opentele
          - telethon
        state: latest
```

**playbook.yml** 
Set proxy variables from group_vars folder.

```yml
 - name: Append proxy settings to environment file
      shell: |
        awk '!seen[$0]++' /home/vagrant/shared/proxy.conf /etc/environment > /etc/environment
```

**tdata**

Consists proxy.conf and telegram session data for every node.
It will be shared into vm node.

```ruby
  # Set up synced folders for data sharing
  node.vm.synced_folder "./tdata/node-#{i}/", "/home/vagrant/shared"

  node.vm.provision "file", source: "./run_session.py", destination: "/home/vagrant/"
```

**run_session.py**
Connect desktop session to teleton client need to be refactored.