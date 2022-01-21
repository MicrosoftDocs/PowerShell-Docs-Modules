---
description: Overview of the SecretStore module
ms.date: 01/21/2022
title: SecretStore overview
---
# Microsoft.PowerShell.SecretStore overview

This module is an extension vault for the PowerShell SecretManagement module. It stores secrets
in local files for the current user account context, and uses .NET crypto APIs to encrypt file
contents. Secrets remain encrypted in-memory, and are only decrypted when retrieved and passed to
the user. This module works over all supported PowerShell platforms on Windows, Linux, and macOS. In
the default configuration, a password is required to store and access secrets, and provides the
strongest protection.
