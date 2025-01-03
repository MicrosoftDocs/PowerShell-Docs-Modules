# Contributor Guide

Thank you for your interest in contributing to quality documentations. As an open source project, we
welcome input and updates from the community.

The process for contributing to this project is documented in our
[Contributor's Guide](https://aka.ms/PSDocsContributor).

## PowerShell-Docs-Modules structure

There are three categories of content in this repository:

- reference content
- conceptual content
- metadata and configuration files

We only maintain documentation for the current release of these modules.

### Reference content

The reference content is the PowerShell cmdlet reference for the DSC cmdlets. The cmdlet reference
for the various modules is collected in the `reference/ps-modules` folder. This content is also used
to create the help information displayed by the `Get-Help` cmdlet.

### Conceptual content

The conceptual documentation is also organized by module or product.

> [!NOTE]
> Anytime a conceptual article is added, removed, or renamed, the TOC must be updated and deleted or
> renamed files must be redirected.

### Metadata files

This project contains several types of metadata files. The metadata files control the behavior of
our build tools and the publishing system. Only PowerShell-Docs maintainers and approved
contributors are allowed to change these files. If you think that a meta file should be changed,
open an issue to discuss the needed changes.

Meta files in the root of the repository

- `.*` - configuration files in the root of the repository
- `*.md` - Project documentation in the root of the repository
- `*.yml` - build automation files
- `.devcontainer/*` - devcontainer configuration files
- `.github/**/*` - GitHub templates, actions, and other meta files
- `.vscode/**/*` - VS Code extension configurations
- `breadcrumb/*` - breadcrumb navigation configuration

Meta files in the documentation set

- `reference/**/*.json` - docset configuration files
- `reference/**/*.yml` - TOC and other structured content files
- `reference/**/*.ps1` - Example DSC resources and configurations
- `reference/breadcrumb/*` - breadcrumb navigation configuration
- `reference/includes/*` - markdown include files
- `reference/mapping/*` - version mapping configuration
- `reference/**/media/**` - image files used in documentation
