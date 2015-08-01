# DACK Playbooks

This is a set of [Ansible](http://www.ansible.com) playbooks that launches the latest version of WordPress, PHP 5.6+, and can be used for static site (use .html extensions) local development, and only local for development now.

### Issues
File a detailed issue with your errors messages, or any suggestions in the issue panel, or a pull request.

## Download and Install Dependencies
[Ansible](http://www.ansible.com)
[best-practices for Ansible](http://docs.ansible.com/playbooks_best_practices.html)
[Homebrew](http://brew.sh)
[Vagrant](http://www.vagrantup.com)
[Virtualbox](https://www.virtualbox.org)

Install [Homebrew](http://brew.sh)

Install via Ansible >= 1.9.2 via homebrew
```sh
brew update
brew install ansible
```

Install Virtualbox and Vagrant (brew-cask is an optional here, or simple head to the links above)

<sub>Vagrant >= 1.7.4, Virtualbox >= 5.0.0</sub>

```sh
git clone https://github.com/d-g-h/DACK.git {{PROJECT_NAME}}
```

For example,
```sh
git clone https://github.com/d-g-h/DACK.git DEVTESTPHP
```

## Configuration

Adjust your /etc/hosts file as necessary to match the [Vagrantfile](https://github.com/RadishLab/STACK/blob/master/Vagrantfile)

```
192.168.50.254
```

For example,
```hosts
192.168.50.254 dev.dev
```

Change the `PROJECT_NAME`

In {{PROJECT_NAME}}/group_vars/all.yml

```
project_name: "dev"
project_url: "dev.dev"
```

**Start** the server with `vagrant up`
If `vagrant up` outputs an error, please run `vagrant destroy -f`. Then save and remove the project folder.

**Stop** the server with `vagrant halt`

**Resume** the server with `vagrant up`

### MySQL
`mysql -u root -proot`
Once the box is running you might want to use Sequel Pro.
You can use the default set port 2254 but you should increment an unique port number (host) to avoid the problems below in Vagrantfile.

```
config.vm.network :forwarded_port, guest: 22, host: 2254, auto_correct: false, id: "ssh"
```

You might run into the error below which means that you have a conflict with your `~/.ssh/known_hosts`

![Middle Man Attack Warning](/src/img/Screen%20Shot%202014-08-05%20at%208.57.46%20AM.png)

If so remove the localhost line in `~/.ssh/known_hosts`

![Remove localhost](/src/img/Screen%20Shot%202014-08-05%20at%208.59.36%20AM.png)

File after removal

![Remove localhost](/src/img/Screen%20Shot%202014-08-05%20at%208.59.52%20AM.png)

Import plist settings from `/src/sequel-pro/ansible-sql.plist`

Password: (Blank, no text please)
SSH Password: vagrant

Accept RSA Keyprint

![Accept RSA Keyprint](/src/img/Screen%20Shot%202014-08-05%20at%209.00.02%20AM.png)

Select the database

### WP Multisite
For Multisite use, enabled options, {{PROJECT_NAME}}/group_vars/all.yml, toggle `true` or `false`

Update hosts file for subdomains

Enable the network

![Enable network](/src/img/enable_network.png)

Edit wp-config.php based on the given settings, log out, log back in order for them to take effect.
If you can’t login, please try another browser or clearing your cache and cookies

![wp-config.php](/src/img/update_wp_config.png)
