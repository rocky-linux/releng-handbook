Rocky Linux Release Engineering Handbook
========================================

This handbook contains information on how the Rocky team builds and releases packages.
The process is mostly automated, but does have steps that is performed manually.

We're currently using the Fedora stack:

* [Koji](https://pagure.io/koji) - Used to build and store packages
* [MBS/fm-orchestrator](https://pagure.io/fm-orchestrator) - Used to orchestrate module builds (utilizes Koji for the package builds itself)
* [Sigul](https://pagure.io/sigul) - Used to sign built RPMs (utilizes Koji as well)

To fork and patch packages, we're using something called the Open Patch Architecture (also called OpenPatch).
OpenPatch requires a forge (git forge in reference implementation `srpmproc`) that can do multi-level repositories.

It expects a structure like this:

* `/rpms` - Source RPMs in SCM format that Koji expects (Sources are stored in blob storage)
* `/modules` - Module definitions (Hashes are retrieved from packages in `/rpms`)
* `/patch` - Directives to modify a Source RPM (has to match name of the repo in `/rpms`)

The Open Patch Architecture is currently implemented with the following tools:

* [srpmproc](https://github.com/rocky-linux/srpmproc) - Upstream package importer (with auto directive applier)
* [distrobuild](https://github.com/rocky-linux/distrobuild) - A simple meta-orchestrator that integrates OpenPatch with the Fedora stack

Currently the following prefixes are running in production:

* [`/staging`](https://git.rockylinux.org/staging)
