# MST P41 Manifest

This repository contains the `repo` manifest used to download the Yocto Project
BSP sources for MST P41. The `scarthgap-7.8.0` branch provides the
`default.xml` manifest, with the required repositories pinned to specific
commits.

## Install the repo tool

If `repo` is not already installed, run:

```bash
mkdir -p ~/bin
curl -fL https://storage.googleapis.com/git-repo-downloads/repo -o ~/bin/repo
chmod a+x ~/bin/repo
export PATH="$HOME/bin:$PATH"
```

The `PATH` setting applies to the current shell. Add the same `export` line to
your shell startup file to make it available in new terminals.

## Download the BSP sources

Create a workspace under `/work/yocto`, initialize the manifest and download the
repositories. Make sure your regular user has write access to `/work/yocto`.

```bash
mkdir -p /work/yocto/scarthgap-mst
cd /work/yocto/scarthgap-mst
repo init -u https://github.com/ahmadmoutraji/mst-p41-manifest.git \
    -b scarthgap-7.8.0 \
    -m default.xml
repo sync -j$(nproc)
```

The BSP sources are checked out into `/work/yocto/scarthgap-mst/layers/`.
The BSP build instructions use the same workspace path.

## Build an image

For build host requirements, machine selection, build environment setup and image
build commands, refer to the
[meta-mst-p41-bsp README](https://github.com/ahmadmoutraji/meta-mst-p41-bsp/blob/scarthgap/README.md).
After syncing the sources, this file is also available at
`layers/meta-mst-p41-bsp/README.md` in your workspace.
