---
description: Overview of the SecretManagement module
ms.date: 01/21/2022
title: SecretManagement overview
---
# Microsoft.PowerShell.SecretManagement overview

PowerShell SecretManagement module provides a convenient way for a user to store and retrieve
secrets. The secrets are stored in SecretManagement extension vaults. An extension vault is a
PowerShell module that has been registered to SecretManagement, and exports five module functions
required by SecretManagement. An extension vault can store secrets locally or remotely. Extension
vaults are registered to the current logged in user context, and are available only to that user.
