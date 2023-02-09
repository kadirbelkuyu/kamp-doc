Vagrant.configure("2") do |config|
  config.vm.box = "spox/ubuntu-arm"
  config.vm.box_version = "1.0.0"

  config.vm.define "control", primary: true do |control|
    control.vm.hostname = "control"

    control.vm.network "private_network", ip: "192.168.56.10"

    control.vm.provision "shell", inline: <<-SHELL
      apt update > /dev/null 2>&1 && apt install -y python3.8-venv sshpass > /dev/null 2>&1
    SHELL
  end
 
  (0..2).each do |i|
    config.vm.define "host#{i}" do |node|
      node.vm.hostname = "host#{i}"

      node.vm.network "private_network", ip: "192.168.56.#{i+20}"

      node.vm.provision "shell", inline: <<-SHELL
        sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
        systemctl restart sshd.service
      SHELL
    end
  end
end