---
title: 使用 Windows Installer 安裝 azdata
titleSuffix: SQL Server big data clusters
description: 瞭解如何安裝 azdata 工具, 以便安裝和管理[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] (預覽) 安裝程式。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a8dd5d2c7d0210880a82d774185a3f2a915608ec
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2019
ms.locfileid: "70158143"
---
# <a name="install-azdata-to-manage-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-with-windows-installer"></a>安裝`azdata`以使用[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] Windows Installer 管理

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文說明如何在 Windows 上`azdata`安裝適用于 SQL Server 2019 Big Data 叢集發行候選版本。 Windows 安裝開始之前, `azdata`需要`pip`安裝。

>若為 Linux (Ubuntu), 請參閱[ `azdata` install with installer](./deploy-install-azdata-linux-package.md)。

目前, 在其他作業系統或散發套件上, 沒有`azdata`要安裝的封裝管理員。 針對這些平臺, 請[參閱`azdata`不安裝套件管理員](./deploy-install-azdata.md)。

## <a name="install-azdata-with-the-microsoft-windows-installer"></a>使用`azdata` Microsoft Windows Installer 安裝

若要`azdata`使用 Microsoft Windows Installer 安裝在上,

1. 如果`azdata`是使用來`pip`安裝, 請移除。 如果`azdata`是使用 Windows Installer 安裝, 請繼續進行下一個步驟。
1. 使用`azdata` Windows Installer 安裝。

### <a name="uninstall-if-previous-installation-done-with-pip"></a>在先前的安裝完成時卸載`pip`

如果您已安裝任何舊版的**mssqlctl** , 請將它移除。 下列命令會移除**mssqlctl**的 CTP 3.1 版本。

   ```bash
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

如果您已`azdata`安裝任何舊版, 請務必先將其卸載, 再安裝最新版本。

   針對 CTP 3.2, 請執行下列命令。

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-ctp3.2/requirements.txt
   ```

移除之後,[請`azdata`在 Windows 上安裝](#install-azdata-windows)。

>[!NOTE]
>如果您先前的安裝是使用 MSI 完成, 則在使用 MSI 安裝程式之前, 您將不需要卸載任何目前的版本。

### <a id="install-azdata-windows"></a>使用 Windows Installer 安裝

使用 Windows Installer 在 Windows 上安裝或`azdata`更新。

[下載WindowsInstaller`azdata` ](http://aka.ms/azdata-msi)。

當安裝程式詢問是否可以對電腦進行變更時, 請按一下`Yes`[]。

### <a name="uninstall-azdata-with-windows-installer"></a>使用`azdata` Windows Installer 卸載

若要`azdata`使用 Windows Installer 卸載, 請遵循適當作業系統的指示。

| 平台      | 指示                                           |
| ------------- |--------------------------------------------------------|
| Windows 10    | 開始 > 設定 > 應用程式                                |
| Windows 8     | 啟動 > 控制台 > 程式 > 卸載程式 |

會呼叫 **`Azdata CLI`** 要卸載的程式。 選取 [此應用程式], `Uninstall`然後按一下 [] 按鈕。

## <a name="next-steps"></a>後續步驟

如需有關 big data 叢集的詳細資訊, 請參閱[ [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]什麼是？](big-data-cluster-overview.md)。
