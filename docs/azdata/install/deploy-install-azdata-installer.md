---
title: 使用 Windows Installer 安裝 Azure Data CLI (azdata)
titleSuffix: ''
description: 了解如何使用安裝程式來安裝 Azure Data CLI (azdata) 工具。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9dd953a78a992a9a5fed7135ae0aee02f88e4de9
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257491"
---
# <a name="install-azure-data-cli-azdata-with-windows-installer"></a>使用 Windows Installer 來安裝 [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]

[!INCLUDE [azdata](../../includes/applies-to-version/azdata.md)]

此文章描述如何在 Windows 上使用安裝程式來安裝 `azdata`。 使用 `azdata` 來管理 SQL Server 巨量資料叢集或已啟用 Azure Arc 的資料服務。

## <a name="steps-to-install-azdata-with-the-microsoft-windows-installer"></a>使用 Microsoft Windows Installer 來安裝 `azdata` 的步驟

若要使用 Microsoft Windows Installer 安裝 `azdata`，

1. 如果 `pip` 是使用 `azdata` 來進行安裝，請將其移除。 如果 `azdata` 是使用 Windows Installer 來進行安裝，請繼續進行下一個步驟。
1. 使用 [Windows Installer](https://aka.ms/azdata-msi) 來安裝 `azdata`。

### <a name="uninstall-azdata-with-windows-installer"></a>使用 Windows Installer 來解除安裝 `azdata`

若要使用 Windows Installer 來解除安裝 `azdata`，請遵循適當作業系統的指示。

| 平台      | Instructions                                           |
| ------------- |--------------------------------------------------------|
| Windows 10| [開始] > [設定] > [應用程式]                                |
| Windows 8     | [啟動] > [控制台] -> [程式集] -> [解除安裝程式] |

要解除安裝的程式稱為 `Azdata CLI`。 選取此應用程式，然後按一下 `Uninstall` 按鈕。

## <a name="next-steps"></a>後續步驟

如需巨量資料叢集的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]？](../../big-data-cluster/big-data-cluster-overview.md)

搭配使用 `azdata` 與[已啟用 Azure Arc 的資料服務](/azure/azure-arc/data/)
