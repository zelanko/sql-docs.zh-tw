---
title: 開發管線中的 SqlPackage
description: 了解如何透過檢查已安裝的組建編號，來使用 SqlPackage.exe 對資料庫開發管線進行疑難排解。
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 198198e2-7cf4-4a21-bda4-51b36cb4284b
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan; sstein
ms.date: 11/4/2020
ms.openlocfilehash: 002d145328ca101fee467428e5b7c8b0ff1fdd95
ms.sourcegitcommit: 866554663ca3191748b6e4eb4d8d82fa58c4e426
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/16/2020
ms.locfileid: "97577809"
---
# <a name="sqlpackage-in-development-pipelines"></a>開發管線中的 SqlPackage

**SqlPackage.exe** 是命令列公用程式，可將數種資料庫開發工作自動化，而且能夠併入 CI/CD 管線。

## <a name="managed-virtual-environments"></a>受控虛擬環境

用於 GitHub Actions 所裝載的執行器與 Azure Pipelines VM 映像的虛擬環境，是在 [virtual-environments](https://github.com/actions/virtual-environments) \(英文\) GitHub 存放庫中管理的。  SqlPackage 是包含在 `windows-latest` 環境中，而且會在每個 SqlPackage 版本發行後的數週內更新到映像中。

## <a name="checking-the-sqlpackage-version"></a>檢查 SqlPackage 版本

在疑難排解工作期間，請務必了解正在使用的 SqlPackage 版本。  若要擷取此資訊，可以為管線新增步驟，以搭配 `/version` 參數執行 SqlPackage。  下面所提供的範例是以 Microsoft 與 GitHub 受控環境為基礎，自我裝載的環境針對工作目錄可能會有不同的安裝路徑。

### <a name="azure-pipelines"></a>Azure Pipelines

透過在 Azure 管線中利用 [script](https://docs.microsoft.com/azure/devops/pipelines/yaml-schema#script) \(英文\) 關鍵字，便可以為 Azure 管線新增步驟以輸出 SqlPackage 版本號碼。

```yaml
- script: sqlpackage.exe /version
  workingDirectory: C:\Program Files\Microsoft SQL Server\150\DAC\bin\
  displayName: 'get sqlpackage version'
```

### <a name="github-actions"></a>GitHub 動作

透過在 GitHub 動作工作流程中利用 [run](https://docs.github.com/en/free-pro-team@latest/actions/reference/workflow-syntax-for-github-actions) \(英文\) 關鍵字，便可以為 GitHub 動作新增步驟以輸出 SqlPackage 版本號碼。

```yaml
- name: get sqlpackage version
  working-directory: C:\Program Files\Microsoft SQL Server\150\DAC\bin\
  run: ./sqlpackage.exe /version
```

:::image type="content" source="media/sqlpackage-pipelines-github-action.png" alt-text="GitHub 動作輸出顯示組建編號 15.0.4897.1":::

## <a name="next-steps"></a>後續步驟

- 深入了解 [sqlpackage](sqlpackage.md)
