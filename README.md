# dotnet-jdt
dotnet-jdt is a cross-platform .NET Core 2.1 or later global tool for applying [JSON Document Transformation](https://github.com/Microsoft/json-document-transforms)


### <a name="dotnet-jdt-cli"></a> Global tool for .NET Core 2.1 and later  [![NuGet package](https://img.shields.io/nuget/dt/dotnet-jdt.svg)](https://www.nuget.org/packages/dotnet-jdt-cli/) 

.NET Core 2.1 introduces the concept of [global tools](https://docs.microsoft.com/en-us/dotnet/core/tools/global-tools),
meaning that you can install `dotnet-jdt` using the .NET CLI and use it everywhere. One advantage of this approach 
is that you can use the same command, for both installation and usage, across all platforms.

> :warning: To use global tools, .Net SDK 5.0.1 or later is required. 

Install `dotnet-jdt` as a global tool (only once):

```cmd
dotnet tool install --global dotnet-jdt --version 1.0.1
```

And then you can apply JDT transforms, from the command-line, anywhere on your PC, e.g.:

```shell
jdt --source original.json --transform delta.json --output final.json
```

## Examples

Source:

```json
{
    "name": "John Doe",
    "age": 43,
    "address": {
        "street": "10 Downing Street",
        "city": "London"
    },
    "phones": [
        "+44 1234567",
        "+44 2345678"
    ]
}
```

Transform:

```json
{
    "Version": 2,
    "Settings": {
        "Setting01" : "NewValue01",
        "Setting03" : "NewValue03"
    },
    "SupportedVersions" : [4, 5],
    "UseThis" : true
}
```

Result:

```json
{
    // Overriden by the transformation file
    "Version": 2,
    "Settings": {
        // Overriden by the transformation file
        "Setting01" : "NewValue01",
        // Not present in the transformation file, unchanged
        "Setting02" : "Default02",
        // Added by the transformation file
        "Setting03" : "NewValue03"
    },
    // The array in the transformation file was appended
    "SupportedVersions" : [1, 2, 3, 4, 5],
    // Added by the transformation file
    "UseThis" : true
}
```
