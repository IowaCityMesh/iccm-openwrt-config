# Iowa City Community Mesh OpenWRT configurations

This is a repository of OpenWRT configurations, used to streamline the process of building firmware that can be flashed onto routers in the Iowa City Community Mesh. The files here can be used on their own, but the repository is organized to work with OpenWRT's [buildroot environment system](https://openwrt.org/docs/guide-developer/toolchain/env), with a single configuration on each branch.

## Before You Begin

To use these configurations with OpenWRT buildroot, first set up your build environment by installing any [prerequisite packages](https://openwrt.org/docs/guide-developer/toolchain/install-buildsystem), and ensure you have 10-15 GB of disk space (more if building images for multiple targets) and at least 2 GB RAM. Once you're ready, clone the OpenWRT repository, move to the correct branch/tag, and use the `feeds` script to fetch the most recent packages:

    git clone https://git.openwrt.org/openwrt/openwrt.git
    cd openwrt
    git checkout v22.03.3
    ./scripts/feeds update -a
    ./scripts/feeds install -a

## Installation

Once buildroot is set up and you're in its root directory (`openwrt` by default), clone this repository into the `env` directory and create symlinks to the `.config` file and `files` directory:

    git clone iccm.git env
    ln -s env/.config .config
    ln -s env/files files

## Usage

### Applying an existing configuration

To use a configuration from the repository, find it using `env list`, then switch to it using `env switch`:

    ./scripts/env list
    ./scripts/env switch <config-name>

### Making a new configuration

To make a new configuration, start from the `master` environment (for a initial blank configuration) or another existing environment, then use `env new` to create a new environment and `make menuconfig` to begin altering it:

    ./scripts/env new <config-name>
    make menuconfig

### Generating a firmware image

Once your desired configuration is in place, use `make download` to fetch source code for dependencies, then `make world` to compile the image (see the [build system usage guide](https://openwrt.org/docs/guide-developer/toolchain/use-buildsystem) for tips on doing this efficiently, as below):

    make download
    ionice -c 3 chrt --idle 0 nice -n19 make -j$(nproc) world

When finished, the firmware will be in the subdirectory of `bin/targets` that corresponds to your configuration's build target.