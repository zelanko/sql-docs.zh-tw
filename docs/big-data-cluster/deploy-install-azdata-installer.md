---
title: 使用 Windows Installer 安裝 azdata
titleSuffix: SQL Server big data clusters
description: 了解如何安裝 azdata 工具以使用安裝程式來安裝及管理 SQL Server 巨量資料叢集。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5b2e87cf96d6237521caeaae55802d2d72769603
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "73594332"
---
# <a name="install-azdata-to-manage-big-data-clusters-2019-with-windows-installer"></a>使用 Windows Installer 來安裝 `azdata` 以管理 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文描述如何在 Windows 上安裝適用於 SQL Server 2019 巨量資料叢集的 `azdata`。 在安裝 Windows 之前，`azdata` 的安裝需要 `pip`。

>針對 Linux (Ubuntu)，請參閱[使用安裝程式來安裝 `azdata`](./deploy-install-azdata-linux-package.md)。

目前沒有任何套件管理員能夠在其他作業系統或發行版上安裝 `azdata`。 針對這些平台，請參閱[在沒有套件管理員的情況下安裝 `azdata`](./deploy-install-azdata.md)。

## <a name="install-azdata-with-the-microsoft-windows-installer"></a>使用 Microsoft Windows Installer 安裝 `azdata`

若要使用 Microsoft Windows Installer 安裝 `azdata`，

1. 如果 `azdata` 是使用 `pip` 來進行安裝，請將其移除。 如果 `azdata` 是使用 Windows Installer 來進行安裝，請繼續進行下一個步驟。
1. 使用 Windows Installer 來安裝 `azdata`。

### <a name="uninstall-if-previous-installation-done-with-pip"></a>如果先前使用 `pip` 來進行安裝，請解除安裝

如果您已安裝任何舊版的 `azdata`，請務必先解除安裝，然後安裝最新版本。

   若要移除 `azdata` 的發行候選版本，請執行下列命令。

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

移除之後，[在 Windows 上安裝 `azdata`](#install-azdata-windows)。

>[!NOTE]
>如果您先前的安裝是使用 MSI 完成，則在使用 MSI 安裝程式之前，您將不需要解除安裝任何目前版本。

### <a name="install-with-windows-installer"></a><a id="install-azdata-windows"></a>使用 Windows Installer 來進行安裝

使用 Windows Installer 在 Windows 上安裝或更新 `azdata`。

[下載 `azdata` Windows Installer](https://aka.ms/azdata-msi)。

當安裝程式詢問是否可以對電腦進行變更時，請按一下 `Yes`。

### <a name="uninstall-azdata-with-windows-installer"></a>使用 Windows Installer 來解除安裝 `azdata`

若要使用 Windows Installer 來解除安裝 `azdata`，請遵循適當作業系統的指示。

| 平台      | Instructions                                           |
| ------------- |--------------------------------------------------------|
| Windows 10| [開始] > [設定] > [應用程式]                                |
| Windows 8     | [啟動] > [控制台] -> [程式集] -> [解除安裝程式] |

要解除安裝的程式稱為 `Azdata CLI`。 選取此應用程式，然後按一下 `Uninstall` 按鈕。

## <a name="next-steps"></a>後續步驟

如需巨量資料叢集的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)