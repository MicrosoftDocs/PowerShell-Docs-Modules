---
title: What's new in Crescendo 1.1
description: New features and changes released in Crescendo 1.1
ms.date: 12/13/2022
---
# What's new in Crescendo 1.1

This preview includes a new cmdlet, a new schema, support for argument value transformation, the
ability to bypass the output handler, and improved error handling.

## New schema version

The Crescendo schema has been updated to include support for two new members to the **Parameter**
class, `ArgumentTransform` and `ArgumentTransformType`. The schema works with supported tools like
Visual Studio Code to provide IntelliSense and tooltips during the authoring experience.

URL location of the always-available Crescendo schema:

```json
{
   "$schema": "https://aka.ms/PowerShell/Crescendo/Schemas/2022-06",
   "Commands": []
}
```

## New `Export-CrescendoCommand` cmdlet

This cmdlet creates JSON configuration files for Crescendo **Command** objects. It can create one
JSON file per **Command** object or create one JSON file containing all objects passed to it.

Crescendo **Command** objects can be created using `New-CrescendoCommand` or imported from an
existing configuration using `Import-CommandConfiguration`.

For more information, see [Export-CrescendoCommand][01].

## Prevent overwriting of the module manifest

Crescendo creates both the module `.psm1` and the module manifest `.psd1` when
`Export-CrescendoModule` is executed. This can create problems when you have customized the module
manifest beyond the scope of Crescendo. The `Export-CrescendoModule` cmdlet now provides a
**NoClobberManifest** switch parameter to prevent the manifest from being overwritten.

```powershell
Export-CrescendoModule -ConfigurationFile .\myconfig.json -ModuleName .\Mymodule -NoClobberManifest
```

> [!NOTE]
> The **NoClobberManifest** parameter prevents Crescendo from updating the module manifest. You are
> responsible for manually updating the manifest with any new cmdlets and settings.

## Bypass output handling entirely

Some native commands create different output depending on whether the output is sent to the screen
or the pipeline. [Pastel][02] is an example of a command that changes its output from a graphical
screen representation to a single string value when used in a pipeline. Crescendo output handling is
pipeline based and can cause these applications to return unwanted results. Crescendo now supports
the ability to bypass the output handler entirely.

To bypass all output handling by Crescendo:

```json
"OutputHandlers": [
    {
        "ParameterSetName": "Default",
        "HandlerType": "ByPass"
    }
]
```

## Handling error output

Previously, native command errors weren't captured by Crescendo and allowed to stream directly to
the user. This prevented you from creating enhanced error handling. Crescendo now captures the
generated command error output (stderr) and is now available to the output handler . Error messages
are placed in a queue. You can access the queue in your output handler using a new internal
function, `Pop-CrescendoNativeError`.

If you don't define an output handler, Crescendo uses the default handler. The default output
handler ensures that errors respect the `-ErrorVariable` and `-ErrorAction` parameters and adds
errors to `$Error`.

Adding an output handler that includes `Pop-CrescendoNativeError` allows you to inspect errors in
the output handler so you can handle them or pass them through to the caller.

```json
"OutputHandlers": [
    {
        "ParameterSetName": "Default",
        "StreamOutput": true,
        "HandlerType": "Inline",
        "Handler": "PROCESS { $_ } END { Pop-CrescendoNativeError -EmitAsError }"
    }
]
```

## Argument value transformation

You may find situations where the input values handed to a Crescendo wrapped command should be
translated to a different value for the underlying native command. Crescendo now supports argument
transformation to support these scenarios. We updated the schema to add two new members to the
**Parameter** class, `ArgumentTransform` and `ArgumentTransformType`. Use these members to transform
parameter arguments inline or invoke a script block that takes the parameter value as an argument.
The default value for `ArgumentTransformType` is inline.

Example: Multiplication of a value.

```json
"Parameters": [
    {
        "Name": "mult2",
        "OriginalName": "--p3",
        "ParameterType": "int",
        "OriginalPosition": 2,
        "ArgumentTransform": "param([int]$v) $v * 2"
    }
]
```

Example: Accepting an ordered hashtable.

```json
"Parameters": [
    {
        "Name": "hasht2",
        "OriginalName": "--p1ordered",
        "ParameterType": "System.Collections.Specialized.OrderedDictionary",
        "OriginalPosition": 0,
        "ArgumentTransform": "param([System.Collections.Specialized.OrderedDictionary]$v) $v.Keys.ForEach({''{0}={1}'' -f $_,$v[$_]}) -join '',''"
    }
]
```

Example: Argument transformation with join.

```json
"Parameters": [
    {
        "Name": "join",
        "OriginalName": "--p2",
        "ParameterType": "string[]",
        "OriginalPosition": 1,
        "ArgumentTransform": "param([string[]]$v) $v -join '',''"
    }
]
```

Example: Calling a script based transformation.

```json
"Parameters": [
    {
        "Name" : "Param1",
        "ArgumentTransform": "myfunction",
        "ArgumentTransformType" : "function"
    }
]
```

## Installing Crescendo

Requirements:

- **Microsoft.PowerShell.Crescendo** requires PowerShell 7.0 or higher

To install **Microsoft.PowerShell.Crescendo** using the new **PowerShellGet** v2.x:

```powershell
Install-Module -Name Microsoft.PowerShell.Crescendo -AllowPreRelease
```

To install **Microsoft.PowerShell.Crescendo** using the new [PowerShellGet v3][03]:

```powershell
Install-PSResource -Name Microsoft.PowerShell.Crescendo -AllowPreRelease
```

<!-- link references -->
[01]: /powershell/module/microsoft.powershell.crescendo/export-crescendocommand
[02]: https://github.com/sharkdp/pastel
[03]: https://www.powershellgallery.com/packages/PowerShellGet/3.0.17-beta
