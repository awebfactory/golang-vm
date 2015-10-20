## Ansible playbook - golang vm

This Vagrant and Virtualbox based Ansible playbook sets up a Go development environment.

For persistence, two alternatives are included:

* MongoDB as part of a complete MEAN stack (Mongodb, Node + Express suitable for back-end for Angular SPAs) together with a sample AngularJS application run on a NodeJS server.
* MySql server  

### Instructions

* Install VirtualBox and Vagrant (make sure Vagrant is version 1.6.5 or later)
* Install Ansible

* Clone this project to a folder where you keep your VMs
* First execute `vagrant box list` to check if `ubuntu/trusty64` is already on your laptop or desktop host system. If it isn't download the box with `vagrant box add ubuntu/trusty64`.
* If you receive messages to the effect that the box has a newer version, follow the instructions:

````
==> default: A newer version of the box 'ubuntu/trusty64' is available! You currently
==> default: have version '20150609.0.10'. The latest is version '20151015.0.0'. Run
==> default: `vagrant box update` to update.
````

* On the cammand-line in that folder, type `vagrant up`
* The process will take a while, on my 4GB RAM MacBook Pro it took about 20+ minutes initially. But remember that's just the first time, once you have it provisioned it starts up again very quickly. A large part of the initial slowness is the one-time provisioning via Ansible of the MEAN components, especially MongoDB.
* Check out your new vm on the command line with `vagrant ssh`
* Associate `http://golang-dev/` (or any other name you'd like) with local machine IP specified in the Vagrantfile (192.168.46.100 initially) by including the following line in `/etc/hosts`:

    192.168.46.100  golang-dev

* Within the guest VM box, if you do your work in, say, `/vagrant/dev/project01` then in the VM dir `./dev/project01` you can access the files with your favorite editor or IDE or else edit via ssh remoting.  
* The MEAN stack example app is at `/vagrant/dev/recipe-js`

* If you create and run a node.js app on port 3000, you can access it in your browser by pointing it at `http://golang-dev:3000`.

### Vagrantfile

* Box used: [Ubuntu 14.04 64-bit (Trusty)](https://vagrantcloud.com/ubuntu/boxes/trusty64)
* [Virtualbox settings:](https://www.virtualbox.org/manual/ch08.html#vboxmanage-modifyvm)
 * memory 1024
 * IP 192.168.76.103

### Playbook tasks

* Installs build-essential and git packages from Apt.
* MongoDB installation:
 * Imports MongoDB's public GPG key.
 * Adds MongoDB's Apt source.
 * Installs MongoDB
* Node.js installation:
 * Sets up [NodeSource](https://github.com/nodesource/distributions) for Ubuntu.
 * Installs NodeJS.
 * Installs the following globally with `npm install -g`:
   * Installs [Gulp](http://gulpjs.com/) .
   * Installs [Bower](http://gulpjs.com/).
   * Installs [Karma](http://gulpjs.com/).

### References

* [Geerling, Jeff, *Ansible for DevOps*](https://leanpub.com/ansible-for-devops)
  * [Ansible for DevOps Examples on GitHub](https://github.com/geerlingguy/ansible-for-devops)
* [Vagrant & Ansible Quickstart Tutorial](http://adamcod.es/2014/09/23/vagrant-ansible-quickstart-tutorial.html)
* [Ansible playbook - MEAN stack](https://github.com/dennmart/vagrant-ansible-playbooks/tree/master/mean)
