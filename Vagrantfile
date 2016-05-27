# This guide is optimized for Vagrant 1.7 and above.
# Although versions 1.6.x should behave very similarly, it is recommended
# to upgrade instead of disabling the requirement below.
Vagrant.require_version ">= 1.7.0"
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "ubuntu/trusty64"
  config.vm.hostname = "internal"
  config.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"
  config.vm.provision "file", source: "./chrome.list", destination: "./chrome.list"
  config.vm.provision "shell" do |s|
    s.inline = "cp chrome.list /etc/apt/sources.list.d/"
    s.privileged = true
  end
  config.vm.provision "shell" do |s|
    s.inline = "wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -"
    s.privileged = true
  end
  config.vm.provision "shell" do |s|
    s.inline = "sudo apt-get update"
    s.privileged = true
  end
  config.vm.provision "shell" do |s|
    s.inline = "sudo apt-get install -qq git google-chrome-stable"
    s.privileged = true
  end
  config.vm.provision "file", source: "~/.gnupg/pubring.gpg", destination: "~/.gnupg/pubring.gpg"
  config.vm.provision "file", source: "~/.gnupg/secring.gpg", destination: "~/.gnupg/secring.gpg"
  config.vm.provision "file", source: "~/.gnupg/trustdb.gpg", destination: "~/.gnupg/trustdb.gpg"
  config.vm.provision "file", source: "~/.gitconfig", destination: "~/.gitconfig"

end
