count = (ENV['count'] or 1).to_i
flavor = (ENV['flavor'] or :ubuntu).to_sym

Vagrant::Config.run do |config|
  count.times do |number|
    name = "box#{number}"

    config.vm.define name do |box|
      case flavor
      when :centos
        box.vm.box = "opscode-centos-6.3"
        box.vm.box_url = "https://opscode-vm.s3.amazonaws.com/vagrant/boxes/opscode-centos-6.3.box"
      when :ubuntu
        box.vm.box = "opscode-ubuntu-12.04"
        box.vm.box_url = "https://opscode-vm.s3.amazonaws.com/vagrant/boxes/opscode-ubuntu-12.04.box"
      end

      box.vm.host_name = name
      box.vm.network :hostonly, "33.33.33.#{100 + number}"
    end
  end
end
