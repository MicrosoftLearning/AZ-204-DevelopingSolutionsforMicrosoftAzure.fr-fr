---
ms.openlocfilehash: 57e7101c824903545932fce809cd5661f95cd3dd
ms.sourcegitcommit: d2d374fffa4fcbf92b9c4bdc9c9ecc470152e033
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/16/2021
ms.locfileid: "145196226"
---
# <a name="lab-virtual-machine-setup"></a>Configuration de la machine virtuelle Lab

## <a name="installed-software"></a>Logiciel installé

| Logiciel | Lien |
| --- | --- |
| Windows 10 (Build 2004) | <https://www.microsoft.com/software-download/windows10> |
| Visual Studio Code | <https://code.visualstudio.com> |
| Extension Azure Account pour Visual Studio Code | <https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account> |
| Extension Azure Functions pour Visual Studio Code | <https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions> |
| Visual Studio Code avec l’extension Outils Azure Resource Manager | <https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools> |
| Extension Azure CLI Tools pour Visual Studio Code | <https://marketplace.visualstudio.com/items?itemName=ms-vscode.azurecli> |
| Extension PowerShell Visual Studio Code | <https://marketplace.visualstudio.com/items?itemName=ms-vscode.PowerShell> |
| Extension C# pour Visual Studio Code | <https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp> |
| PowerShell 7 | <https://github.com/PowerShell/PowerShell/releases/tag/v7.0.3> |
| Kit SDK .NET Core 3.1 | <https://dotnet.microsoft.com/download/dotnet-core/3.1> |
| Azure PowerShell | <https://docs.microsoft.com/powershell/azure/install-az-ps> |
| Azure CLI | <https://docs.microsoft.com/cli/azure/install-azure-cli> |
| Explorateur Stockage Azure | <https://azure.microsoft.com/features/storage-explorer> |
| Outil .NET - HttpRepl | <https://github.com/dotnet/HttpRepl> |
| Azure Functions Core Tools | <https://docs.microsoft.com/azure/azure-functions/functions-run-local#v3> |
| Terminal Windows | <https://aka.ms/terminal> |
| Edge (Chromium) | <https://www.microsoft.com/edge> |

## <a name="additional-configuration"></a>Configuration supplémentaire

- Activer ClearType
  
- Configurer Microsoft Edge comme navigateur par défaut

- Mettre à jour la configuration de VSCode

  ```json
  {
    "editor.fontFamily": "'Cascadia Code', Consolas, 'Courier New', monospace",
    "update.enableWindowsBackgroundUpdates": false,
    "update.mode": "manual",
    "terminal.integrated.shell.windows": "C:\\Program Files\\PowerShell\\7\\pwsh.exe",
    "workbench.startupEditor": "none",
    "terminal.integrated.rendererType": "dom",
    "csharp.suppressDotnetInstallWarning": true,
    "csharp.suppressDotnetRestoreNotification": true,
    "csharp.supressBuildAssetsNotification": true,
    "azureFunctions.showProjectWarning": false
  }
  ```

- Mettre à jour la configuration du terminal Windows

  ```json
  {
    "$schema": "https://aka.ms/terminal-profiles-schema",
    "defaultProfile": "{574e775e-4f2a-5b96-ac1e-a2962a402336}",
    "profiles": [
      {
        "guid": "{574e775e-4f2a-5b96-ac1e-a2962a402336}",
        "useAcrylic": true,
        "acrylicOpacity": 0.85,
        "colorScheme": "Campbell",
        "fontFace": "Cascadia Code",
        "hidden": false,
        "name": "PowerShell",
        "source": "Windows.Terminal.PowershellCore"
      },
      {
        "guid": "{b453ae62-4e3d-5e58-b989-0a998ec441b8}",
        "hidden": false,
        "name": "Azure Cloud Shell",
        "source": "Windows.Terminal.Azure"
      }
    ],
    "schemes": [],
    "keybindings": []
  }
  ```

- Configurez le menu Démarrer et la barre des tâches pour inclure uniquement les icônes suivantes:
  - Explorateur de fichiers
  - Edge
  - Terminal Windows
  - Visual Studio Code
  - Explorateur Stockage Azure

- Désactiver les notifications de mise à jour PowerShell 7

  1. [Créez une variable d’environnement](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_update_notifications?view=powershell-7) nommée ``POWERSHELL_UPDATECHECK``.
  
  1. Définissez la valeur de la variable d’environnement sur ``Off`` (respecte la casse).

- Exécutez Azure Functions Core Tools au moins une fois pour configurer le pare-feu Windows

  ```bash
  func init test --worker-runtime dotnet
  cd test
  func new --template 'HTTP trigger' --name web
  func start --build
  ```
