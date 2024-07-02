# Quick Note

## dotnet 8

### IncludeSourceRevisionInInformationalVersion: auto git versioning

The `IncludeSourceRevisionInInformationalVersion` is a new property introduced in .NET 8 that enhances versioning information in .NET projects. This property, when enabled, appends the source control revision (such as a Git commit hash) to the `InformationalVersion` attribute of the assembly.

WARN: the default value of this property is true, that means the version value is inclueded in built binaries. 

To use this property, add this in your project file (`.csproj` or equivalent):

```xml
<PropertyGroup>
  <IncludeSourceRevisionInInformationalVersion>true</IncludeSourceRevisionInInformationalVersion>
</PropertyGroup>
```

By setting this property to `true`, the build process will automatically include the source revision in the `InformationalVersion`, which can be viewed through assembly metadata.

ref: [Breaking change: Source Link included in the .NET SDK - .NET | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/core/compatibility/sdk/8.0/source-link)

Alternative way: [NuGet Gallery | Unclassified.NetRevisionTask 0.4.3](https://www.nuget.org/packages/Unclassified.NetRevisionTask)