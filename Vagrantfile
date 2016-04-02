# -*- mode: ruby -*-
Vagrant.configure('2') do |config|
  config.vm.box      = 'ubuntu/trusty64'
  config.ssh.forward_agent = true
  config.vm.synced_folder "rules_go", "/src/rules_go"
  config.vm.synced_folder "bazel", "/src/bazel"

  %w[ master ].each_with_index do |name, i|
    config.vm.define(name) do |c|
      c.vm.hostname = name
      c.vm.provision :chef_solo do |chef|
        chef.cookbooks_path = ['chef/cookbooks', 'chef/berks-cookbooks']
        %w[
          apt
          git
          devtools
          dotfiles
          rbenv
          java
        ].each do |recipe|
          chef.add_recipe(recipe)
        end
        chef.json = {
          "java" => {
            "install_flavor" => "oracle",
            "jdk_version" => 8,
            "set_etc_environment" => true,
            "oracle" => {
              "accept_oracle_download_terms" => true,
            }
          },
        }
      end
    end
  end
end
# vim: set ft=ruby :
