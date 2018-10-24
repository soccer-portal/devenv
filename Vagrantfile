# params
params = {
  "hostname" => "sp-middleware-local",
  "ip" => "10.99.3.100",
  "ports" => { 3306 => 13306, 6379 => 16379, 8081 => 18081, 8082 => 18082 },
  "compose_version" => "1.22.0" # current version @ 2018/10
}

# check plugin
unless Vagrant.has_plugin?("vagrant-docker-compose")
  system("vagrant plugin install vagrant-docker-compose")
  puts "Dependencies installed, please try the command again."
  exit
end
unless Vagrant.has_plugin?("vagrant-hostsupdater")
  system("vagrant plugin install vagrant-hostupdater")
  puts "Dependencies installed, please try the command again."
  exit
end

# provision
Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-18.04"

  config.vm.network "private_network", ip: params["ip"]
  params["ports"].each {|port_from, port_to|
    config.vm.network(:forwarded_port, guest: port_from, host: port_to)
  }
  config.vm.synced_folder "./docker", "/vagrant/docker"

  config.vm.hostname = params["hostname"]
  config.hostsupdater.aliases = [ params["hostname"] ]

  config.vm.provision :shell, inline: "apt-get update"

  config.vm.provision :docker, run: "always"

  config.vm.provision :docker_compose,
    yml: "/vagrant/docker/docker-compose.yml",
    compose_version: params["compose_version"],
    run: "always"
end
