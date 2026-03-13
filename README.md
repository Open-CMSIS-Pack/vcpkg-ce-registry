# Vendor vcpkg-ce-registry
How to create and maintain a vendor specific tools registry for use with Microsoft's vcpkg tool.

This repository provides an example of a github hosted vcpkg ce registry.

The examples uses the following name definitions:

registry owner: my-registry 
artifact vendor: my-vendor
artifact name: my-tool
artifact type: tools (one of `tools`, `compilers`, `models`, `debuggers`)
artifact origin: my-org  
artifact id: tools/my-org/my-tool
artifact version: 1.0.0 (major.minor.patch)

Step 1:
create directory with the artifact name:

```bash
  mkdir my-tool
```

Step 2:
create manifest file for a new artifact version

```bash
  cp template/manifest-template.json my-tool/my-tool-1.0.0.json
```

Step 3: 
open manifest version file in editor and fill out settings:

```
id
version
description
summary
contacts:
demands:
- "windows and x64" | "windows and arm64" | "linux and x64" | "linux and arm64" | "osx and x64" | "osx and x64"
  - install:
    - untar | unzip
    - sha256
    - strip
  - exports:
    - paths:
      - PATH
```

Step 4:
create/update index.json

```bash
  vcpkg-shell z-ce regenerate .
```

Step 5:
push changes to main branch

Step 6:
add registry and add artifact to the `requires:` node in a vcpkg-configuration.json

```json
{
 "registries": [
  {
   "name": "my-registry",
   "kind": "artifact",
   "location": "https://github.com/Open-CMSIS-Pack/vcpkg-ce-registry/archive/refs/heads/main.zip"
  }
 ],
 "requires": {
  "my-registry:tools/my-org/my-tool": "1.0.0"
 }
}

Step 7:
download, install and activate the artifact version

```bash
vcpkg-shell activate
```

or

```bash
vcpkg-shell use my-registry:tools/my-org/my-tool --version 1.0.0
```

