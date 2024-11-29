---
sidebar_position: 1
---

# Install

## Fedora

```shell
sudo dnf install libvirt vagrant vagrant-libvirt vagrant-sshfs
```

Note that we are installing `vagrant-sshfs` which will allow us to share directories between the host and the Vagrant VM

Here is an example of how to declare shared directories. Note that the type `sshfs` is set.

```ruby
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
 config.vm.synced_folder ".", "/home/vagrant/devel", type: "sshfs"
end
```
