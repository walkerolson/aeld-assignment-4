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
