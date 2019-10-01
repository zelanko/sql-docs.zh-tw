---
title: 升級為新版本
titleSuffix: SQL Server big data clusters
description: 瞭解如何將 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] （預覽）升級至新版本。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: bb1bf33c9ccb342e6afc4d22d67463791c0d67b6
ms.sourcegitcommit: 36c3ead6f2a3628f58040acf47f049f0b0957b8a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/30/2019
ms.locfileid: "71688268"
---
# <a name="how-to-upgrade-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>如何升級 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文提供將 SQL Server 巨量資料叢集升級至新版本的指導。 本文中的步驟特別適用於在預覽版本之間升級。

## <a name="backup-and-delete-the-old-cluster"></a>備份和刪除舊叢集

目前，將巨量資料叢集升級至新版本的唯一方法是手動移除並重新建立叢集。 每個版本都有與舊版不相容的唯一 `azdata` 版本。 此外，如果舊叢集必須在新的節點上下載映像，則最新映像可能會與叢集上的舊版映像不相容。 若要升級至最新版本，請遵循下列步驟：

1. 在刪除舊叢集之前，請先備份 SQL Server 主要執行個體和 HDFS 上的資料。 針對 SQL Server 主要執行個體，您可以使用 [SQL Server 備份和還原](data-ingestion-restore-database.md)。 針對 HDFS，您[可以使用 `curl` 來複製資料](data-ingestion-curl.md)。

1. 使用 `azdata delete cluster` 命令刪除舊叢集。

   ```bash
    azdata bdc delete --name <old-cluster-name>
   ```

   > [!Important]
   > 使用符合您叢集的 `azdata` 版本。 請勿使用較新版本的 `azdata` 刪除較舊的叢集。

   > [!Note]
   > 發出 `azdata bdc delete` 命令會導致在命名空間中建立的所有物件都是以要刪除的大型資料叢集名稱來加以識別，而不是命名空間本身。 命名空間可重複用於後續部署，只要它是空的，而且沒有在內建立其他應用程式。

1. 在 CTP 3.2 之前，`azdata` 稱為 `mssqlctl`。 如果您已安裝任何舊版的 `mssqlctl` 或 `azdata`，請務必先卸載，再安裝最新版本的 `azdata`。

   針對 CTP 2.3 或更新版本，請執行下列命令。 以您要卸載的 `mssqlctl` 版本取代命令中的 `ctp3.1`。 如果版本是在 CTP 3.1 之前，請在版本號碼之前加上虛線 (例如 `ctp-2.5`)。

   ```powershell
   pip3 uninstall -r https://aka.ms/azdata
   ```

1. 安裝 `azdata` 的最新版本。 下列命令會為發行候選版本安裝 `azdata`：

   **Windows：**

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

   **Linux：**

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!IMPORTANT]
   > 針對每個版本，`azdata` 的路徑會變更。 即使您先前已安裝 `azdata` 或 `mssqlctl`，您仍必須從最新的路徑重新安裝，才能建立新的叢集。

## <a id="azdataversion"></a> 確認 azdata 版本

部署新的 big data 叢集之前，請確認您使用的是最新版本的 `azdata` 搭配 `--version` 參數：

```bash
azdata --version
```

## <a name="install-the-new-release"></a>安裝新版本

移除先前的 big data 叢集並安裝最新的 `azdata` 之後，請使用目前的部署指示來部署新的 big data 叢集。 如需詳細資訊，請參閱[如何在 Kubernetes 上部署 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](deployment-guidance.md)。 接著，還原任何必要的資料庫或檔案。

## <a name="next-steps"></a>後續步驟

如需 big data 叢集的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](big-data-cluster-overview.md)。
