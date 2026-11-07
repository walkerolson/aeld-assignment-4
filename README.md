# Overview

This repository contains assignment starter code for buildroot based assignments for the course Advanced Embedded Software Design, ECEN 5713

It also contains instructions related to modifying your buildroot project to use with supported hardware platforms.  See [this wiki page](https://github.com/cu-ecen-5013/buildroot-assignments-base/wiki/Supported-Hardware) for details.

## Buildroot configuration

Buildroot is included as a submodule pinned to release `2024.02.13`. Initialize the
submodules, then run `./build.sh` to configure the QEMU image using
`base_external/configs/aesd_qemu_defconfig`.

The defconfig enables Dropbear, the `aesd-assignments` package, and the root
password required by the automated QEMU tests. To verify those selections after
configuration, run:

```sh
grep -E '^(BR2_PACKAGE_(DROPBEAR|AESD_ASSIGNMENTS)=y|BR2_TARGET_GENERIC_ROOT_PASSWD="root")$' buildroot/.config
```

The package fetches the Assignment 3 source from its SSH Git URL at the
configured commit, cross-compiles `writer`, and installs `writer`, `writer.sh`,
`finder.sh`, `finder-test.sh`, and the `tester.sh` entry point under `/usr/bin`.
The tester reads configuration from `/etc/finder-app/conf` and invokes `writer`
and `finder.sh` through `PATH`, so it can be run from any working directory.
It depends on BusyBox for the shell utilities used by the scripts; Dropbear is
enabled in the defconfig for SSH access to the QEMU target.
