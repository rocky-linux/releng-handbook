Blob storage
============

OpenPatch can accept any type of side-storage that can provide a HTTP interface to retrieve the files.
The files should be present in a flat CAS-like structure.

For example, if `nginx` has the following metadata:
```text
a9dc8c5b055a3f0021d09c112d27422f45dd439c SOURCES/nginx-1.14.1.tar.gz
9571452ab835130f1b074cf98b95a717ec703347 SOURCES/poweredby.png
b8b4d1d77597b691918c850953b70c98fa178be28faf756a5aa0dddf8b96ab33 SOURCES/nginx-logo.png
```

`SOURCES/nginx-1.14.1.tar.gz` would be present at `{side-storage-http}/a9dc8c5b055a3f0021d09c112d27422f45dd439c`

The following side-storages are currently used in production:

* [http://rocky-linux-sources-staging.a1.rockylinux.org](http://rocky-linux-sources-staging.a1.rockylinux.org/) - AWS S3 backed