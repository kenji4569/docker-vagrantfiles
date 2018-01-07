# Docker Vagrantfiles

This project provides Vagrantfiles to use Docker and Docker Compose on a specific OS with the shared folder.

In the beginning, please install [VirtualBox](https://www.virtualbox.org/) and [Vagrant](https://www.vagrantup.com/).

## Run VM with Vagrant

Copy a sample Vagrantfile for a specific OS:

```
cp -f Vagrantfile.ubuntu path_to_working_dir/Vagrantfile
cd path_to_working_dir
```

You may have to edit the Vagrantfile especially for `config.vm.box` and `config.vm.network`.

Start the virtual machine:

```
vagrant up
```

For Mac users, please install the following plugin for file notification:

```
vagrant plugin install vagrant-notify-forwarder
```

For the first time, the following error may occur
`/sbin/mount.vboxsf: mounting failed with the error: No such device`
In that case, please enter the following command for that shared folder problem:

```
vagrant plugin install vagrant-vbguest
vagrant vbguest
```

Update the plugin settings:

```
vagrant reload
````

Log in to the virtual machine:

```
vagrant ssh
```