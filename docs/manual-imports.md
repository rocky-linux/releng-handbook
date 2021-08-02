Manual imports
==============
We discovered that some packages have broken release imports so has to be pinned manually.

Some of these may not be required anymore. Proceed with caution

#### perl-bootstrap
`sudo AWS_REGION=us-east-2 srpmproc --module-mode --import-branch-prefix="r" --module-prefix="https://git.rockylinux.org/original/modules" --version 8 --source-rpm perl-bootstrap --upstream-prefix ssh://git@git.rockylinux.org:22220/staging --storage-addr s3://ord1-prod-rocky-sources-staging --ssh-key-location HIDDEN`

#### perl-Try-Tiny
`sudo AWS_REGION=us-east-2 srpmproc --import-branch-prefix="r" --rpm-prefix="https://git.rockylinux.org/original/rpms" --version 8 --source-rpm perl-Try-Tiny --upstream-prefix ssh://git@git.rockylinux.org:22220/staging --storage-addr s3://ord1-prod-rocky-sources-staging --ssh-key-location HIDDEN`

#### perl-Term-Size-Any
`sudo AWS_REGION=us-east-2 srpmproc --import-branch-prefix="r" --rpm-prefix="https://git.rockylinux.org/original/rpms" --version 8 --source-rpm perl-Term-Size-Any --upstream-prefix ssh://git@git.rockylinux.org:22220/staging --storage-addr s3://ord1-prod-rocky-sources-staging --ssh-key-location HIDDEN`

#### perl-Test-NoWarnings
`sudo AWS_REGION=us-east-2 srpmproc --import-branch-prefix="r" --rpm-prefix="https://git.rockylinux.org/original/rpms" --version 8 --source-rpm perl-Test-NoWarnings --upstream-prefix ssh://git@git.rockylinux.org:22220/staging --storage-addr s3://ord1-prod-rocky-sources-staging --ssh-key-location HIDDEN`

#### dom4j
`sudo AWS_REGION=us-east-2 srpmproc --version 8 --source-rpm dom4j --upstream-prefix ssh://git@git.rockylinux.org:22220/staging --storage-addr s3://ord1-prod-rocky-sources-staging --ssh-key-location HIDDEN --manual-commits "c8:19891fec809a901d73e8bc5dd70db13b37611d72"`

#### glibc32
`sudo AWS_REGION=us-east-2 srpmproc --version 8 --source-rpm glibc32 --upstream-prefix ssh://git@git.rockylinux.org:22220/staging --storage-addr s3://ord1-prod-rocky-sources-staging --ssh-key-location HIDDEN --manual-commits "c8:c0ff9f9fcf954328c22f2d21f3b0ccc893c8517a"`

#### python-pytest-mock
`sudo AWS_REGION=us-east-2 srpmproc --version 8 --source-rpm python-pytest-mock --upstream-prefix ssh://git@git.rockylinux.org:22220/staging --storage-addr s3://ord1-prod-rocky-sources-staging --ssh-key-location HIDDEN --manual-commits "c8:33ffc02f984d9f7d9862f2d80bf817e986e5dff9"`

#### javapackages-tools (201902)
`sudo AWS_REGION=us-east-2 srpmproc --source-rpm javapackages-tools --upstream-prefix "ssh://git@git.rockylinux.org:22220/staging" --version 8 --storage-addr s3://ord1-prod-rocky-sources-staging --ssh-key-location HIDDEN --single-tag imports/c8-stream-201902/javapackages-tools-5.3.1-7.module+el8.2.0+5555+73059ce4`

#### javapackages-tools (module)
`sudo AWS_REGION=us-east-2 srpmproc --module-mode --source-rpm javapackages-tools --upstream-prefix "ssh://git@git.rockylinux.org:22220/staging" --version 8 --storage-addr s3://ord1-prod-rocky-sources-staging --ssh-key-location HIDDEN --single-tag imports/c8-stream-201902/javapackages-tools-201902-8020020200125124130.af5e9d52 --module-fallback-stream 3.6`

#### slf4j (import before mongodb, then re-import from distrobuild)
`sudo AWS_REGION=us-east-2 srpmproc --version 8 --source-rpm slf4j --upstream-prefix ssh://git@git.rockylinux.org:22220/staging --storage-addr s3://ord1-prod-rocky-sources-staging --ssh-key-location HIDDEN --single-tag imports/c8-stream-3.6/slf4j-1.7.25-4.el8+1359+ee4104af`

#### mongodb
`sudo AWS_REGION=us-east-2 srpmproc --module-mode --version 8 --source-rpm mongodb --upstream-prefix ssh://git@git.rockylinux.org:22220/staging --storage-addr s3://ord1-prod-rocky-sources-staging --ssh-key-location HIDDEN --manual-commits "c8-stream-3.6:5454a7f6041f5446c59093ef2749f3a9c0ef6ff8"`

#### snakeyaml
`sudo AWS_REGION=us-east-2 srpmproc --version 8 --source-rpm snakeyaml --upstream-prefix ssh://git@git.rockylinux.org:22220/staging --storage-addr s3://ord1-prod-rocky-sources-staging --ssh-key-location HIDDEN --single-tag imports/c8s/snakeyaml-1.26-2.el8 --allow-stream-branches`

#### mdds
`sudo AWS_REGION=us-east-2 srpmproc --version 8 --source-rpm mdds --upstream-prefix ssh://git@git.rockylinux.org:22220/staging --storage-addr s3://ord1-prod-rocky-sources-staging --ssh-key-location HIDDEN --single-tag imports/c8s/mdds-1.4.3-1.el8 --allow-stream-branches`

#### spirv-tools
`sudo AWS_REGION=us-east-2 srpmproc --version 8 --source-rpm spirv-tools --upstream-prefix ssh://git@git.rockylinux.org:22220/staging --storage-addr s3://ord1-prod-rocky-sources-staging --ssh-key-location HIDDEN --single-tag imports/c8/spirv-tools-2020.5-1.20200803.git92a7165.el8`

#### gcc-toolset-10-elfutils (for gcc-toolset-10-strace, untag from build and compose after)
`sudo AWS_REGION=us-east-2 srpmproc --version 8 --source-rpm gcc-toolset-10-elfutils --upstream-prefix ssh://git@git.rockylinux.org:22220/staging --storage-addr s3://ord1-prod-rocky-sources-staging --ssh-key-location HIDDEN --allow-stream-branches --single-tag imports/c8s/gcc-toolset-10-elfutils-0.176-6.el8`

#### felix-scr
`sudo AWS_REGION=us-east-2 srpmproc --version 8 --source-rpm felix-scr --upstream-prefix ssh://git@git.rockylinux.org:22220/staging --storage-addr s3://ord1-prod-rocky-sources-staging --ssh-key-location HIDDEN --single-tag imports/c8-stream-rhel8/felix-scr-2.1.16-1.module+el8.1.1+4657+f90e8085`

#### felix-scr
`sudo AWS_REGION=us-east-2 srpmproc --version 8 --source-rpm felix-scr --upstream-prefix ssh://git@git.rockylinux.org:22220/staging --storage-addr s3://ord1-prod-rocky-sources-staging --ssh-key-location HIDDEN --single-tag imports/c8-stream-rhel8/felix-scr-2.1.16-1.module+el8.1.1+4657+f90e8085`

#### eclipse
`sudo AWS_REGION=us-east-2 srpmproc --version 8 --source-rpm eclipse --upstream-prefix ssh://git@git.rockylinux.org:22220/staging --storage-addr s3://ord1-prod-rocky-sources-staging --ssh-key-location HIDDEN --single-tag imports/c8-stream-rhel8/eclipse-4.12-6.module+el8.1.1+4657+f90e8085`

#### perl-Devel-StackTrace
`sudo AWS_REGION=us-east-2 srpmproc --import-branch-prefix="r" --rpm-prefix="https://git.rockylinux.org/original/rpms" --version 8 --source-rpm perl-Devel-StackTrace --upstream-prefix ssh://git@git.rockylinux.org:22220/staging --storage-addr s3://ord1-prod-rocky-sources-staging --ssh-key-location HIDDEN`

#### perl-Spiffy
`sudo AWS_REGION=us-east-2 srpmproc --import-branch-prefix="r" --rpm-prefix="https://git.rockylinux.org/original/rpms" --version 8 --source-rpm perl-Spiffy --upstream-prefix ssh://git@git.rockylinux.org:22220/staging --storage-addr s3://ord1-prod-rocky-sources-staging --ssh-key-location HIDDEN`

#### perl-Test-Deep (import this one from both upstream and original)
`sudo AWS_REGION=us-east-2 srpmproc --import-branch-prefix="r" --rpm-prefix="https://git.rockylinux.org/original/rpms" --version 8 --source-rpm perl-Test-Deep --upstream-prefix ssh://git@git.rockylinux.org:22220/staging --storage-addr s3://ord1-prod-rocky-sources-staging --ssh-key-location HIDDEN`

#### perl-Test-Base
`sudo AWS_REGION=us-east-2 srpmproc --import-branch-prefix="r" --rpm-prefix="https://git.rockylinux.org/original/rpms" --version 8 --source-rpm perl-Test-Base --upstream-prefix ssh://git@git.rockylinux.org:22220/staging --storage-addr s3://ord1-prod-rocky-sources-staging --ssh-key-location HIDDEN`

#### perl-Test-YAML
`sudo AWS_REGION=us-east-2 srpmproc --import-branch-prefix="r" --rpm-prefix="https://git.rockylinux.org/original/rpms" --version 8 --source-rpm perl-Test-YAML --upstream-prefix ssh://git@git.rockylinux.org:22220/staging --storage-addr s3://ord1-prod-rocky-sources-staging --ssh-key-location HIDDEN`

#### bind-dyndb-ldap
`sudo AWS_REGION=us-east-2 srpmproc --import-branch-prefix="r" --rpm-prefix="https://git.rockylinux.org/original/rpms" --version 8 --source-rpm bind-dyndb-ldap --upstream-prefix ssh://git@git.rockylinux.org:22220/staging --storage-addr s3://ord1-prod-rocky-sources-staging --ssh-key-location HIDDEN`

#### custodia
`sudo AWS_REGION=us-east-2 srpmproc --import-branch-prefix="r" --rpm-prefix="https://git.rockylinux.org/original/rpms" --version 8 --source-rpm custodia --upstream-prefix ssh://git@git.rockylinux.org:22220/staging --storage-addr s3://ord1-prod-rocky-sources-staging --ssh-key-location HIDDEN`

#### opendnssec
`sudo AWS_REGION=us-east-2 srpmproc --import-branch-prefix="r" --rpm-prefix="https://git.rockylinux.org/original/rpms" --version 8 --source-rpm opendnssec --upstream-prefix ssh://git@git.rockylinux.org:22220/staging --storage-addr s3://ord1-prod-rocky-sources-staging --ssh-key-location HIDDEN`

#### slapi-nis
`sudo AWS_REGION=us-east-2 srpmproc --import-branch-prefix="r" --rpm-prefix="https://git.rockylinux.org/original/rpms" --version 8 --source-rpm slapi-nis --upstream-prefix ssh://git@git.rockylinux.org:22220/staging --storage-addr s3://ord1-prod-rocky-sources-staging --ssh-key-location HIDDEN`

#### softhsm
`sudo AWS_REGION=us-east-2 srpmproc --import-branch-prefix="r" --rpm-prefix="https://git.rockylinux.org/original/rpms" --version 8 --source-rpm softhsm --upstream-prefix ssh://git@git.rockylinux.org:22220/staging --storage-addr s3://ord1-prod-rocky-sources-staging --ssh-key-location HIDDEN`