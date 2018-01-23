# Docker Vagrantfiles

This project provides Vagrantfiles to use Docker and Docker Compose on a specific OS with the shared folder.

In the beginning, please install [VirtualBox](https://www.virtualbox.org/) and [Vagrant](https://www.vagrantup.com/).

## Build and Run

Copy a sample Vagrantfile for a specific OS:

```
$ cp -f Vagrantfile.ubuntu path_to_working_dir/Vagrantfile
$ cd path_to_working_dir
```

You may have to edit the Vagrantfile especially for `config.vm.box` and `config.vm.network`.

Start the virtual machine:

```
$ vagrant up
```

For the first time, the following error may occur
`/sbin/mount.vboxsf: mounting failed with the error: No such device`.
In that case, please enter the following command for that shared folder problem:

```
$ vagrant plugin install vagrant-vbguest
$ vagrant vbguest
$ vagrant reload
```

(If you got any shared folder problems, please retry the above command.)

For Mac users, please install the following plugin for file notification:

```
$ vagrant plugin install vagrant-notify-forwarder
$ vagrant reload
```

(Currently Windows would not support file notification)

## Login

Login to the virtual machine by the following command:

```
$ vagrant ssh
```

Check the shared folder worked:

```
$ ls -l
```

## Tips

### VM address

You can check the ip address of the VM which is configured in `config.vm.network` in Vagrantfile as follows:

```
$ vagrant ssh
$ ip addr | grep -E "192\.|10\.10" | awk '{print $2}' | sed 's/\/.*$//'
$ 10.10.10.110
```

It would be convenient for development to set a host name for the VM IP address by [editing hosts file](https://www.howtogeek.com/howto/27350/beginner-geek-how-to-edit-your-hosts-file/).

```
$ vi /etc/hosts # For mac / linux
# Add this line for the VM IP address
10.10.10.110    vm1.local
```

Now, you can access `vm1.local` for `10.10.10.110` to access the VM.


If no ip address is shown by the above `ip addr ...` command, something goes wrong in your network.
An alternative way to expose internal servers is to use port forwarding.
For example, put the following setting in Vagrantfie

```
config.vm.network "forwarded_port", guest: 80, host: 10080
```

then, you can access 80 port on the inside of the VM via `localhost:10080` on the outside of the VM



### Git SSH key

To download git repositories on the VM, you may have to set a SSH private key in `~/.ssh` directory.

```
$ cp your_ssh_private_key ~/.ssh/id_rsa
$ chmod 600 ~/.ssh/id_rsa # you should change the permission to `600` for ssh keys
```

If you already have a private key in your local on the outside of the VM,
`ssh-add` command can just copy it to the VM from the local.

```
$ ssh-add ~/.ssh/id_rsa # Copy the ssh key from your local on the outside of the VM
```

If you have no ssh key, just generate it by `ssh-keygen` and register the public key to the target Git system.

```
$ ssh-keygen
$ cat ~/.ssh/id_rsa.pub # Register the public key to the target Git system
```

### Vagrant basic commands

```
$ vagrant reload
```

will reload the VM with reloading Vagrantfile. If you changed `Vagrantfile`, execute this command.

```
$ vagrant halt
```

will shutdown the VM, and

```
$ vagrant up
```

will start the VM again.

