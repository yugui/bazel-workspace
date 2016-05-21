# -*- mode: ruby -*-
Vagrant.configure('2') do |config|
  config.vm.box      = 'ubuntu/trusty64'
  config.ssh.forward_agent = true
  config.vm.synced_folder "rules_go", "/src/rules_go"
  config.vm.synced_folder "bazel", "/src/bazel"
  config.vm.network :forwarded_port, id: "ssh", guest: 22, host: 2222,
    auto_correct: true

  %w[ master ].each_with_index do |name, i|
    config.vm.define(name) do |c|
      c.vm.hostname = name
      c.vm.provision :chef_solo do |chef|
        chef.version = '12.10.40'
        chef.data_bags_path = "data_bags"
        chef.roles_path = %w[ roles ]

        chef.json = {}
        %w[ bazel ].each do |name|
          chef.add_role name
        end
      end
    end
  end
end
# vim: set ft=ruby :
