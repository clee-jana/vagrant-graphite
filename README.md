# Graphite

* Access the graphite web console at http://localhost:5080
* You can access graphite at localhost:5003

## Installation Instructions

* Download [Vagrant](http://vagrantup.com)
* Install [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
* Start your vagrant image and SSH in with `vagrant ssh`
* Run this last command: `sudo graphite-manage syncdb`. You can use the
  default values and pick a generic password.
* Test the install by visiting the Graphite Web Console at [http://localhost:5080](http://localhost:5080)
* Fire some test data to graphite (10 second intervals between).
  Example: `echo "test.count 3 `date +%s`" | nc -c 127.0.0.1 5003` on OS
  X or `nc -q` on linux.

* You do not need to repeat all these steps everytime if you shutdown
  with `vagrant halt`. You only need to run the syncdb command if you
  `vagrant destroy`.

## Starting Vagrant

```
# from this repos home
$> vagrant up
# to resume a suspended instance
$> vagrant resume
# ssh into the isntance
$> vagrant ssh
```

## Stopping the instance
```
# standby
$> vagrant suspend

# shutdown
$> vagrant halt

# delete the instance to start over. please note you will lose the contents of the vagrant box. synced folders are safe because they are on the host vm.
$> vagrant destroy
```

## Known Issues

* Not sure how to auto run the syncdb command unattended. I've tried
  various forms of `-noinput` without any luck.
* Need to change ENABLE_UDP_LISTENER to True in /etc/carbon/carbon.conf
