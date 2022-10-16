# How to add a new Toolchain

Since this repository is a mirror for [WAGO PFC Toolchains](https://github.com/orgs/WAGO/repositories?q=toolchain&type=all&language=&sort=), a new toolchain is added whenever WAGO releases a new one.

WAGO decided to provide two GIT repositories for each new toolchain:
- build scripts to re-create the toolchain  
  e.g. [WAGO/gcc-toolchain-2019.12](https://github.com/WAGO/gcc-toolchain-2019.12)
- the precompiled toolchain itself  
  e.g. [WAGO/gcc-toolchain-2019.12-precompiled](https://github.com/WAGO/gcc-toolchain-2019.12-precompiled)

To add a new toolchain, we create a tag containing the build scripts and
a release based on this tag containing a re-packaged version of the
precompiled toolchain.

In this how to `gcc-toolchain-2019.12` is used as an example.

## Create a Tag containing Toolchain Build Scripts

Clone the upstream toolchain. Since we are not interested in the
upstream history, a shallow clone is sufficient.

    git clone --depth 1 https://github.com/WAGO/gcc-toolchain-2019.12

Clone this repository and switch working directory

    git clone https://github.com/falk-werner/pfc-toolchains.git
    cd pfc-toolchains

Create a new empty orphan branch. Note that the `switch` command is
the best way to do this. Also note that the newly created branch should
be prefixed by the topic `toolchain/` to prevent later confusion with the tag name. 

    git switch --orphan toolchain/gcc-toolchain-2019.12

Copy the contents of the upstream repo into the newly created branch.

    rsync -r --exclude .git ../gcc-toolchain-2019.12/ .

Commit the branch.

    git add -A
    git commit -m "added toolchain build scripts from https://github.com/WAGO/gcc-toolchain-2019.12
    git push -u orgin toolchain/gcc-toolchain-2019.12

Create the tag

    git tag -a gcc-toolchain-2019.12 -m "gcc-toolchain-2019.12"
    git push -u origin gcc-toolchain-2019.12

## Create a Release based on the Tag

Clone the precompiled toolchain. A shallow clone is sufficient, since
we only want to re-package the contents.

    git clone --depth 1 https://github.com/WAGO/gcc-toolchain-2019.12-precompiled.git
    cd gcc-toolchain-2019.12-precompiled

Create a tarball containing the toolchains binaries and sysroot. Note that owner and group
should be set to 0 (root) to avoid references to any local user.

    tar -cf gcc-toolchain-2019.12.tar arm-linux-gnueabihf arm-linux-gnueabihf-sysroot --owner=0 --group=0

Compress the tarball. Therefore `xz` should be used to achieve a good compression. This
might take a while depending on the development machine.

    xz -z9 gcc-toolchain-2019.12.tar

Finally, the release can be created via GitHub UI. Choose the previously created tag and
upload the `.xz` archive containing the precompiled toolchain.