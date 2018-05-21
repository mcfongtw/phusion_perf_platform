# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"
DOCKER_HOST_NAME = "ContainerHost"
#DOCKER_HOST_VAGRANTFILE = "./DockerHostVagrantfile"
DOCKER_HOST_VAGRANTFILE = "../StudyNotesOnJavaPerformance/examples/root/perf-container-base/Vagrantfile"
NETWORK_PRIVATE_IP_PREFIX = "172.16.3."

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

	config.vm.define "PerfToolVM" do |perftool|
  		perftool.vm.provider "docker" do |docker|
			docker.build_dir = "."
			docker.force_host_vm = true
    			docker.vagrant_machine = "#{DOCKER_HOST_NAME}"
    			docker.vagrant_vagrantfile = "#{DOCKER_HOST_VAGRANTFILE}"
			docker.has_ssh = false
			docker.remains_running = false
			docker.create_args = ['--privileged=true']
		        docker.volumes=["/var/lib/docker:/var/lib/docker", "/tmp:/output"]
  		end
		perftool.ssh.username = "root"
		perftool.ssh.port = 22
		perftool.ssh.private_key_path = 'phusion.key'
		perftool.vm.synced_folder ".", "/vagrant", disabled: false
		perftool.vm.provision "shell", inline: "echo 'SSH Init Complete!'" 
	end
end
