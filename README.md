# vagrant_playground

## Simple project to play with vagrant and ansible automatization

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

**playbook.yml** 
Set proxy variables from group_vars folder.

```yml
  tasks:
    - name: Set HTTP proxy
      lineinfile:
        path: /etc/environment
        line: http_proxy={{http_proxy}}
        state: present
```