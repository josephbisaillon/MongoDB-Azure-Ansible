# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure('2') do |config|
  config.vm.boot_timeout = 1000

  common_azure = Proc.new do |azure, override|
        config.vm.box = 'azure'
	      config.ssh.pty= true
        azure.mgmt_certificate = 'cert/cert.pem'
        azure.mgmt_endpoint = 'https://management.core.windows.net'
        azure.subscription_id = 'XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX' # add here your subscription id
        azure.storage_acct_name = 'vagrantazure'
        azure.vm_image = '5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-65-20150325'
        azure.vm_user = 'muly' # change to username on your local host
	      azure.ssh_private_key_file = '/home/muly/.ssh/id_rsa'	# change the path of id_rsa to yours
	      azure.ssh_certificate_file = '/home/muly/.ssh/ssh-cert.pem' # change the path of ssh-cer.pem to yours
        azure.vm_name = 'mongo-azure'
        azure.cloud_service_name = 'mongo-staging' # same as vm_name. leave blank to auto-generate
        azure.deployment_name = 'mongo-staging' # defaults to cloud_service_name
        azure.vm_location = 'East US' # e.g., West US
	      azure.ssh_port = '22'
	      azure.tcp_endpoints = '27017:27017'
  end

  config.vm.define 'primary' do |cfg|
    cfg.vm.provider :azure do |azure, override|
      common_azure.call azure, override
      azure.vm_name = 'master-node'
      azure.ssh_port = 2200
      azure.tcp_endpoints = '40000:40000,40001:10100,40002:10400'
    end
  end

  config.vm.define 'slave1' do |cfg|
    cfg.vm.provider :azure do |azure, override|
      common_azure.call azure, override
      azure.vm_name = 'secondary-node1'
      azure.ssh_port = 2201
      azure.tcp_endpoints = '40001:40001,40000:20100,40002:20400'
    end
  end

  config.vm.define 'slave2' do |cfg|
    cfg.vm.provider :azure do |azure, override|
      common_azure.call azure, override
      azure.vm_name = 'secondary-node2'
      azure.ssh_port = 2202
      azure.tcp_endpoints = '40002:40002,40001:30100, 40000:30400'
    end
  end

  # TO ADD EXTRA SECONDARY MONGODB SERVERS UNCOMMENT THE FOLLOWING LINES
  #config.vm.define 'slave3' do |cfg|
  #  cfg.vm.provider :azure do |azure, override|
  #    common_azure.call azure, override
  #    azure.vm_name = 'secondary-node3'
  #    azure.ssh_port = 2203
  #    azure.tcp_endpoints = '40002:40003,40001:40100, 40000:40400'
  #  end
  #end
  # TO ADD EXTRA SECONDARY MONGODB SERVERS UNCOMMENT THE FOLLOWING LINES
  #config.vm.define 'slave4' do |cfg|
  #  cfg.vm.provider :azure do |azure, override|
  #    common_azure.call azure, override
  #    azure.vm_name = 'secondary-node4'
  #    azure.ssh_port = 2204
  #    azure.tcp_endpoints = '40002:40004,40001:50100, 40000:50400'
  #  end
  #end


  config.ssh.username = 'muly' # modify this username
  config.ssh.private_key_path = "/home/muly/.ssh/id_rsa" # modify this path 

end
