Distrobuild
===========
Distrobuild orchestrates imports and builds of a pre-defined list of packages and modules.
Currently it shells out to the OpenPatch reference implementation `srpmproc`.

## Metadata
The metadata is what decides what should be imported from where and what repository it belongs in.
Good metadata would ensure that all module components is imported correctly.

The following metadatas are used in production:

* [rockylinux/distrobuild-extra](https://github.com/rocky-linux/distrobuild-extra)

## Bootstrap
The initial state of distrobuild is pretty much useless. By placing the metadata files in `/tmp`, then running an import would set the instance up.
All package lists should contain one package per line and should match the following format `{REPO}_ALL.txt`

Currently the following repositories are supported:

* BASEOS
* APPSTREAM
* POWERTOOLS
* EXTERNAL
* MODULAR_CANDIDATE
* ORIGINAL
* INFRA
* EXTRAS