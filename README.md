# Paket Case-Sensitivity when finding package references

This repo contains two projects: MySDK and MyClient. 
MyClient has a project reference to MySDK.

## Expected behaviour:

When creating nuget packages, two packages should be created and MyClient should have a dependency on the MySDK package. 

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

This can be reproduced by the Repo as-is using the provided `pack` command-line

## Actual behaviour

When doing the following rename:
```
mv MySDK MySdk
```

.. the dependency is not found anymore:

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

Tested on Windows 7 on an NTFS file system