---
description: Use Microsoft.PowerShell.PlatyPS to create XML-based help for PowerShell modules.
ms.date: 10/09/2025
title: Convert and publish the help files
---
# Convert and publish the help files

By this point, you should have finished creating, editing, and testing the Markdown help files. The
next step is to convert the Markdown source files to MAML help files and publish for your module.


## Convert the Markdown files to MAML

The following example imports the Markdown help files in the `.\WidgetModule` directory then exports
the command help to MAML format in the `.\maml` directory.

```powershell
Measure-PlatyPSMarkdown -Path .\WidgetModule\*.md |
    Where-Object Filetype -match 'CommandHelp' |
    Import-MarkdownCommandHelp -Path {$_.FilePath} |
    Export-MamlCommandHelp -OutputFolder .\maml
```

## Publish the help files

There are two publishing options:

- Include the help files in the module
- Package the help files for Updatable Help

### Option 1: Include the help files in the module

The `Get-Help` cmdlet looks for module Help topic files in language-specific subdirectories of the
module directory. Copy the MAML help files and any about_*.help.txt files to an language-specific
folder in the module directory. The foldername must use the culture code format, such as `en-US`.
For example, the following directory structure diagram shows the location of the Help topics for the
WidgetModule module.

```
<PSModulePath>\
  WidgetModule\
    en-US\
      about_WidgetModule.help.txt
      WidgetModule-Help.xml
      NestedWidgetModule.dll-Help.xml
```

> [!NOTE]
> In the example, the `<PSModulePath>` placeholder represents one of the paths in the
> `$env:PSModulePath` environment variable, such as `$HOME\Documents\Modules`, `$PSHOME\Modules`, or
> a custom path specified by the user.

If you have created help in other languages, create additional folders for each language.

### Option 2: Package the help files for Updatable Help

To support Updatable Help, you need to package the help file (both MAML and text-based help) in an
archive file and create a `HelpInfo.xml` file that includes the download location of the help
content, the version of help, and the languages available.

You also need to host the help content on a web server that supports HTTPS. The module must have a
module manifest. The **HelpInfoUri** property in the manifest must contain the URL to the folder
location on the web server where the `HelpInfo.xml` file is located. This URL should be the folder
location, not the full path to the `HelpInfo.xml` file and it must end with a forward slash (`/`)
character.

For more information, see [Updatable Help Authoring][02].

PlatyPS makes this process easier. If the module manifest contains the **HelpInfoUri** property when
you create the module Markdown file, PlatyPS automatically adds the required metadata to the
Markdown file. Use the following example to create the Updateable Help package.

```powershell
$params = @{
    CabinetFilesFolder = '.\maml\WidgetModule'
    MarkdownModuleFile = '.\WidgetModule\WidgetModule.md'
    OutputFolder       = '.\helppackage'
}
New-HelpCabinetFile @params
```

The **CabinetFilesFolder** parameter specifies the folder that contains the MAML and text-based help
files to include in the package. The **MarkdownModuleFile** parameter specifies the module Markdown
file that contains the metadata required to create the `HelpInfo.xml` file. The **OutputFolder**
parameter specifies the folder where the `.cab` and `.zip` files and the `HelpInfo.xml` file are
created. Copy these files to the web server in the location specified by the **HelpInfoUri**
property.

The **HelpInfoUri** property in the manifest must contain the URL to the folder location on the web
server where the `HelpInfo.xml` file is located. The `Update-Help` cmdlet uses this location to
construct the full path to the `HelpInfo.xml` file. The `Update-Help` cmdlet uses the information in
the `HelpInfo.xml` file to construct the full path to the help content files.

For more information, see [How Updatable Help Works][01].

<!-- link references -->
[01]: /powershell/scripting/developer/help/how-updatable-help-works
[02]: /powershell/scripting/developer/help/updatable-help-authoring-step-by-step
