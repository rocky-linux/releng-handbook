---
title: OpenPatch Directives
---

OpenPatch Directives
====================
Supported directives are declared in a [Protocol Buffer](https://developers.google.com/protocol-buffers) document: [cfg.proto](https://github.com/rocky-linux/srpmproc/blob/85ff2d3a60a578e43c225833fa0d3cacc5339d3c/proto/cfg.proto)

Directive files are in prototxt/textproto and all directives here can be used repeatedly in them.
Example:
```
add {
    file: "ROCKY/_supporting/debrand-single-cpu.patch"
}

add {
    file: "ROCKY/_supporting/debrand-rh_taint.patch"
}

add {
    file: "ROCKY/_supporting/debrand-rh-i686-cpu.patch"
}
```
Source: [staging/patch/kernel/ROCKY/CFG/kernel.cfg](https://git.rockylinux.org/staging/patch/kernel/-/blob/815a9dca95da31f65e34ac6d747419fd070e47f8/ROCKY/CFG/kernel.cfg#L1-11)

## Replace
The `replace` directive replaces a file in the RPM repository.
A file from the `patch` directory can be used as well as inline content.

### API
* `file`
    * type: `string`
    * required: `true`
    * description: `file to replace in the SOURCES directory in the target rpms repository`
* oneof
    * `with_file`
        * type: `string`
        * description: `full path to file in the target patch repository that should replace the given file`
    * `with_inline`
        * type: `string`
        * description: `inline string content to replace the target file with`
    * `with_lookaside`
        * type: `string`
        * description: `replace target file with another file in lookaside`

### Examples
```
replace {
    file: "index.html" # replaces rpms/nginx/SOURCES/index.html
    with_file: "ROCKY/_supporting/index.html" # with patch/nginx/ROCKY/_supporting/index.html
}
```
Source: [staging/patch/nginx/ROCKY/CFG/pages.cfg](https://git.rockylinux.org/staging/patch/nginx/-/blob/d3ff910eea5dbc3c5a251d2f69309dabafc64982/ROCKY/CFG/pages.cfg#L1)


## Delete
The `delete` directive deletes any literal file in the RPM repository.

_PS: This directive does NOT delete the source file from the spec. Use [SpecChange](#specchange) for that._

### API
* `file`
    * type: `string`
    * required: `true`
    * description: `file to delete in the target rpms repository`

### Examples
```
delete {
    file: "SOURCES/redhatsecureboot301.cer"
}
```
Source: [staging/patch/kernel/ROCKY/CFG/kernel.cfg](https://git.rockylinux.org/staging/patch/kernel/-/blob/815a9dca95da31f65e34ac6d747419fd070e47f8/ROCKY/CFG/kernel.cfg#L29)

## Add
The `add` directive adds a file from the patch repository to the rpms repository.
The file is added to the `SOURCES` directory in the target rpms repository.

_PS: This directive does NOT add the source file to the spec. Use [SpecChange](#specchange) for that._

### API
* oneof
    * `file`
        * type: `string`
        * description: `file in the patch repository to add to the rpms repository`
    * `lookaside`
        * type: `string`
        * description: `lookaside hash that should be pulled in to the rpms repository`
* `name`
    * type: `string`
    * description: `overrides file name if set`

### Examples
```
add {
    file: "ROCKY/_supporting/debrand-single-cpu.patch"
}
```
Source: [staging/patch/kernel/ROCKY/CFG/kernel.cfg](https://git.rockylinux.org/staging/patch/kernel/-/blob/815a9dca95da31f65e34ac6d747419fd070e47f8/ROCKY/CFG/kernel.cfg#L1)

```
add {
    lookaside: "c92ac268d787fd4c0154c797690fc1f8d45ca5ea"
    name: "NameConstraints.ocsp1.cert"
}
```
Source: [staging/patch/nss/ROCKY/CFG/nss.cfg](https://git.rockylinux.org/staging/patch/nss/-/blob/47af50987ca05dd9ca73f430b4454228c6251339/ROCKY/CFG/nss.cfg#L1)

## Lookaside
The `lookaside` directive puts the post-patch file into lookaside.
Files affected by the directive is automatically marked as lookaside only and excluded from the resulting rpms repository.

### API
* `file`
    * type: `array[string]`
    * description: `files in SOURCES to add to lookaside`
    * required: `true`
* `tar` (currently unimplemented in srpmproc)
    * type: `bool`
    * description: `whether the files should be put into a tar archive and gzipped`
* `archive_name` (currently unimplemented in srpmproc)
    * type: `string`
    * description: `name of the tar file, required and valid only if tar is true`
* `from_patch_tree` (currently unimplemented in srpmproc)
    * type: `bool`
    * description: `uses the patch repository as source instead of the rpms repository`

### Examples
```
lookaside {
    file: "nginx-logo.png"
}
```
Source: [staging/patch/nginx/ROCKY/CFG/pages.cfg](https://git.rockylinux.org/staging/patch/nginx/-/blob/d3ff910eea5dbc3c5a251d2f69309dabafc64982/ROCKY/CFG/pages.cfg#L21)

## Patch
The `patch` directive applies a patch on the rpms repository itself (does not influence the spec by itself)

### API
* `file`
    * type: `string`
    * description: `patch file that is located in the patch repository (from repo root)`
* `strict`
    * type: `bool`
    * description: `adds a "SOURCES" prefix should automatically be added to unprefixed diffs if set to true`

### Examples
```
patch {
    file: "ROCKY/_supporting/0001-Porting-to-8.4-debranding-and-Rocky-branding.patch"
}
```
Source: [staging/patch/kernel/ROCKY/CFG/kernel.cfg](https://git.rockylinux.org/staging/patch/kernel/-/blob/815a9dca95da31f65e34ac6d747419fd070e47f8/ROCKY/CFG/kernel.cfg#L66)

## SpecChange
The `spec_change` directive applies specified changes to the spec in target rpms repository

### API
* `file`
    * type: [`array[FileOperation]`](#fileoperation)
    * description: `allows files (both sources and patches) to be added to the spec`
* `changelog`
    * type: [`array[ChangelogOperation]`](#changelogoperation)
    * description: `adds a new changelog entry with specified information`
* `search_and_replace`
    * type: [`array[SearchAndReplaceOperation]`](#searchandreplaceoperation)
    * description: `replaces a substring with another`
* `append`
    * type: [`array[AppendOperation]`](#appendoperation)
    * description: `append a value to a pre-existing field`
* `new_field`
    * type: [`array[NewFieldOperation]`](#newfieldoperation)
    * description: `add a new field with given value. field will be grouped with other pre-existing fields (if any)`

### Examples
```
spec_change {
    changelog {
        author_name: "Mustafa Gezen"
        author_email: "mustafa@rockylinux.org"
        message: "Debrand default pages"
    }
}
```
Source: [staging/patch/nginx/ROCKY/CFG/pages.cfg](https://git.rockylinux.org/staging/patch/nginx/-/blob/d3ff910eea5dbc3c5a251d2f69309dabafc64982/ROCKY/CFG/pages.cfg#L25)

```
spec_change {
    file {
        name: "0001-Add-Rocky-Linux-specific-changes.patch"
        type: Patch
        add: true
        add_to_prep: true
        n_path: 1
    }

    search_and_replace {
        any: true
        find: "VERSION_ID%%.*"
        replace: "VERSION_ID"
        n: 1
    }

    append {
        field: "Release"
        value: ".rocky.1"
    }

    changelog {
        author_name: "Release Engineering"
        author_email: "releng@rockylinux.org"
        message: "Add Rocky Linux specific changes"
    }
}
```
Source: [staging/patch/dotnet5.0/ROCKY/CFG/dotnet5.0.cfg](https://git.rockylinux.org/staging/patch/dotnet5.0/-/blob/c0bb2ebc50d13651505088f83f857eb1580e3e24/ROCKY/CFG/dotnet5.0.cfg#L5)

```
spec_change {
    file {
        name: "0028-journal-change-support-URL-shown-in-the-catalog-entr.patch"
        type: Patch
        delete: true
    }

    file {
        name: "remove-mount-assert.patch"
        type: Patch
        add: true
    }

    changelog {
        author_name: "Release Engineering"
        author_email: "releng@rockylinux.org"
        message: "Remove support URL patch"
        message: "Disable assertion for mount for possible kernel bug"
    }
}
```
Source: [staging/patch/systemd/ROCKY/CFG/support.cfg](https://git.rockylinux.org/staging/patch/systemd/-/blob/r8/ROCKY/CFG/support.cfg#L5)

## Enums and messages

### FileOperation_Type
* type: `enum`
* definition:
    * `Unknown`
        * description: `this should never be used`
    * `Source`
        * description: `process as a source file`
    * `Patch`
        * description: `process as a patch file`

### FileOperation
* type: `message`
* definition:
    * `name`
        * type: `string`
        * description: `name of file to process`
    * `type`
        * type: [`FileOperation_Type`](#fileoperation_type)
        * description: `type of file that is being processed`
    * `add_to_prep`
        * type: `bool`
        * description: `add a %patch directive to %prep. only valid for patch files`
    * `n_path`
        * type: `int32`
        * description: `adds this value as the strip prefix argument (-p) to patch`
    * oneof
        `add`
            * type: `bool`
            * description: `adds the file to the spec`
        `delete`
            * type: `bool`
            * description: `deletes file from the spec`

### ChangelogOperation
* type: `message`
* definition:
    * `author_name`
        * type: `string`
        * description: `name to use in changelog`
    * `author_email`
        * type: `string`
        * description: `email to use in changelog`
    * `message`
        * type: `array[string]`
        * description: `message lines to use in changelog`

### SearchAndReplaceOperation
* type: `message`
* definition:
    * `find`
        * type: `string`
        * description: `substring to match on`
    * `replace`
        * type: `string`
        * description: `string to replace matches with`
    * `n`:
        * type: `int32`
        * description: `occurences to replace. -1 to replace all`
    * oneof:
        * `field`
            * type: `string`
            * description: `replace occurences for given field`
        * `any`
            * type: `bool`
            * description: `replace occurences anywhere`
        * `starts_with`
            * type: `bool`
            * description: `replace occurences that starts with the find value`
        * `ends_with`
            * type: `bool`
            * description: `replace occurences that ends with the find value`

### AppendOperation
* type: `message`
* definition:
    * `field`
        * type: `string`
        * description: `field to append value to`
    * `value`
        * type: `string`
        * description: `value to append`

### NewFieldOperation
* type: `message`
* definition:
    * `key`
        * type: `string`
        * description: `field name`
    * `value`
        * type: `string`
        * description: `field value`