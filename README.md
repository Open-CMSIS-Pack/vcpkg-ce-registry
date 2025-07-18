# vcpkg-ce-registry
Registry of Open-CMSIS-Pack CMSIS-Toolbox 'ctools' for Microsoft vcpckg artifacts.

This repository is no longer maintained and the registry should no longer be used.

a) the artifact has been renamend from `tools/open-cmsis-pack/ctools` to `tools/open-cmsis-pack/cmsis-toolbox`
b) the artifact is registered in the [arm registry](https://artifacts.tools.arm.com/vcpkg-registry)
c) example - vcpkg-configuration.json
```yaml
{
 "registries": [
  {
   "name": "arm",
   "kind": "artifact",
   "location": "https://artifacts.tools.arm.com/vcpkg-registry"
  }
 ],
 "requires": {
  "arm:tools/open-cmsis-pack/cmsis-toolbox": "^2.0.0"
 }
}

```



