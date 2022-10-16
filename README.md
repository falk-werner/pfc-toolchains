# PFC Toolchains

This repository is a mirror of [WAGO PFC Toolchains](https://github.com/orgs/WAGO/repositories?q=toolchain&type=all&language=&sort=).
In contrast to WAGO, we have all toolchains in one repository and provide released toolchains using GitHub released. Therefore we do not need Git LFS an provide significant smaller downloads.

_Note: The downside of this solution is, that you cannot use a clone
of this repository directly as a toolchain (as described
[here](https://github.com/WAGO/gcc-toolchain-2019.12-precompiled#2-installation)). But since there are no
upstream updates of a toolchain in practive, this is not considerred
a problem._

## Install a Toolchain

There is a release for each toolchain. The following steps use the
[gcc-toolchain-2019.12](https://github.com/falk-werner/pfc-toolchains/releases/tag/gcc-toolchain-2019.12) as an example how to install a
particular toolchain.

1) Download precompiled Toolchain  
   `wget https://github.com/falk-werner/pfc-toolchains/releases/download/gcc-toolchain-2019.12/gcc-toolchain-2019.12.tar.xz`

2) Create a directory to store the toolchain  
   the recommended directory is `/opt`  
   `sudo mkdir /opt/gcc-Toolchain-2019.12`

3) Extract the downloaded toolchain  
   `sudo tar -xf gcc-toolchain-2019.12.tar.xz -C /opt/gcc-Toolchain-2019.12`