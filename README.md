# Docker Vagrantfiles

This project provides Vagrantfiles to use Docker and Docker Compose on a specific OS with the shared folder.

In the beginning, please install [VirtualBox](https://www.virtualbox.org/) and [Vagrant](https://www.vagrantup.com/).

## Build and Run

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

For the first time, the following error may occur
`/sbin/mount.vboxsf: mounting failed with the error: No such device`.
In that case, please enter the following command for that shared folder problem:

```
vagrant plugin install vagrant-vbguest
vagrant vbguest
vagrant reload
```

(If you got any shared folder probelms, please retry the above command.)

For Mac users, please install the following plugin for file notification:

```
vagrant plugin install vagrant-notify-forwarder
vagrant reload
```

(Currently Windows would not support file notification)

## Login

Login to the virtual machine by the following command:

```
vagrant ssh
```

Check the shared folder worked:

```
ls -l
```