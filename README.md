# debian "squeeze" bootstrapping script for EC2 #

This is a fork of camptocamps bootstrapping script for EC2 AMIs. It creates a
vanilla debian squeeze machine image, no latent logfiles no .bash\_history or
even apt package cache.  The machine configuration this script creates has been
thoroughly tested.

*This script is only tested on debian squeeze.*
*You will need an EC2 server to run this bootstrapper.*

## Usage ##

The script is started with ``./ec2debian-build-ami`` it has sensible defaults
but can be configured with options and plugins. To see a list of options run
``./ec2debian-build-ami --help``.
At the very least, the script needs to know your AWS credentials.

There are no interactive prompts, the bootstrapping can run entirely unattended
from start till finish.

Some plugins are included in the [plugins directory](https://github.com/andsens/ec2debian-build-ami/tree/master/plugins).
A list of external plugins is also provided there. If none of those scratch
your itch, you can of course [write your own plugin](https://github.com/andsens/ec2debian-build-ami/blob/master/plugins/HOWTO.md).

## Features ##

### AMI features ###

* EBS booted
* Base installation uses only 289MB
* xfs filesystem
* Ephemeral storage is properly mapped
* Standard ec2 startup scripts
* Uses standard debian Xen kernel from apt
* update-grub creates an actual menu.lst which pvGrub can read

### Bootstrapper features ###

* EBS volume is automatically created, mounted, formatted, unmounted, "snapshotted" and deleted
* AMI is automatically registered with the right kernels for the current region of the host machine
* Can create both 32-bit and 64-bit AMIs
* Plugin system to keep the bootstrapping process automated
* Custom packages
* The process is divided into simple task based scripts
* Bootstrapping server mirror depends on AWS region
* APT source mirror depends on AWS region
