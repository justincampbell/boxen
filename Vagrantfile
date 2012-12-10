count = (ENV['count'] or 1).to_i
flavor = (ENV['flavor'] or :ubuntu).to_sym

case flavor
when :centos
  box_name = "opscode-centos-6.3"
  box_url = "https://opscode-vm.s3.amazonaws.com/vagrant/boxes/opscode-centos-6.3.box"
when :ubuntu
  box_name = "opscode-ubuntu-12.04"
  box_url = "https://opscode-vm.s3.amazonaws.com/vagrant/boxes/opscode-ubuntu-12.04.box"
end

Vagrant::Config.run do |config|
  count.times do |number|
    number += 1
    name = "box#{number}"

    config.vm.define name do |box|
      box.vm.box = box_name
      box.vm.box_url = box_url
      box.vm.host_name = name
      box.vm.network :hostonly, "33.33.33.#{100 + number}"
    end
  end

  active_vms = JSON.parse(File.read('.vagrant'))["active"].keys.collect(&:to_sym) rescue []
  (active_vms - config.vm.defined_vm_keys).each do |name|
    config.vm.define name do |box|
      box.vm.box = box_name
    end
  end
end
