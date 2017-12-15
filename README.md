# Paket Case-Sensitivity when finding package references

This repo contains two projects: MySDK and MyClient. 
MyClient has a project reference to MySDK.

## Expected behaviour:

When creating nuget packages using the provided `pack` command-line, two packages should be created and MyClient should have a dependency on the MySDK package. 
```
paket.exe pack nuget --build-config Debug --build-platform "AnyCPU" --version 1.0.0
```
MyClient.nuspec inside MyClient-1.0.0.nupkg should look like this:
```
<?xml version="1.0" encoding="utf-8" standalone="yes"?>
<package xmlns="http://schemas.microsoft.com/packaging/2011/10/nuspec.xsd">
  <metadata>
    <id>MyClient</id>
    <version>1.0.0</version>
    <title>MyClient</title>
    <authors>MyCompany</authors>
    <description>MyClient program.</description>
    <dependencies>
      <dependency id="MySDK" version="1.0.0" />
    </dependencies>
  </metadata>
</package>
```

## Actual behaviour

The dependency is not found:

```
<?xml version="1.0" encoding="utf-8" standalone="yes"?>
<package xmlns="http://schemas.microsoft.com/packaging/2011/10/nuspec.xsd">
  <metadata>
    <id>MyClient</id>
    <version>1.0.0</version>
    <title>MyClient</title>
    <authors>MyCompany</authors>
    <description>MyClient program.</description>
  </metadata>
</package>
```

This behaviour seems to depend on _casing of the MySdk directory_:

- If the directory is renamed to *MySDK*, the dependency is found
- If the directory name is Pascal case (*MySdk*), the dependency is *not* found


Tested on Windows 7 on an NTFS file system