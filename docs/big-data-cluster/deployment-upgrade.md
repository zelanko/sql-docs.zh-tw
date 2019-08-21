---
title: 升級為新版本
titleSuffix: SQL Server big data clusters
description: 瞭解如何將 ( [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]預覽) 升級至新版本。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 867729b7d638960a2dbf2cb5f7544fecf698c94d
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652338"
---
# <a name="how-to-upgrade-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>如何升級[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文提供將 SQL Server 巨量資料叢集升級至新版本的指導。 本文中的步驟特別適用於在預覽版本之間升級。

## <a name="backup-and-delete-the-old-cluster"></a>備份和刪除舊叢集

目前，將巨量資料叢集升級至新版本的唯一方法是手動移除並重新建立叢集。 每個版本都有與先前版本不相容的唯一 **azdata** 版本。 此外，如果舊叢集必須在新的節點上下載映像，則最新映像可能會與叢集上的舊版映像不相容。 若要升級至最新版本，請遵循下列步驟：

1. 在刪除舊叢集之前，請先備份 SQL Server 主要執行個體和 HDFS 上的資料。 針對 SQL Server 主要執行個體，您可以使用 [SQL Server 備份和還原](data-ingestion-restore-database.md)。 針對 HDFS，您[可以使用 **curl** 來複製資料](data-ingestion-curl.md)。

1. 使用 `azdata delete cluster` 命令刪除舊叢集。

   ```bash
    azdata bdc delete --name <old-cluster-name>
   ```

   > [!Important]
   > 使用符合您叢集的 **azdata** 版本。 請勿使用較新版本的 **azdata** 來刪除舊叢集。

1. 在 CTP 3.2 之前，**azdata** 稱為 **mssqlctl**。 如果您已安裝任何舊版的 **mssqlctl** 或 **azdata**，請務必先解除安裝，再安裝最新版本的 **azdata**。

   針對 CTP 2.3 或更新版本，請執行下列命令。 在命令中將 `ctp3.1` 取代為您要解除安裝的 **mssqlctl** 版本。 如果版本是在 CTP 3.1 之前，請在版本號碼之前加上虛線 (例如 `ctp-2.5`)。

   ```powershell
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. 安裝最新版本的 **azdata**。 下列命令會安裝適用於 CTP 3.2 的 **azdata**：

   **Windows：**

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

   **Linux：**

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!IMPORTANT]
   > 每個版本的 **azdata** 路徑都不同。 即使您先前已安裝 **azdata** 或 **mssqlctl**，您還是必須從最新的路徑重新安裝，才能建立新的叢集。

## <a id="azdataversion"></a> 確認 azdata 版本

在您部署新的巨量資料叢集之前，請確認您使用的是最新版本的 **azdata**，包含 `--version` 參數：

```bash
azdata --version
```

## <a name="install-the-new-release"></a>安裝新版本

在您移除先前的巨量資料叢集，並安裝最新的 **azdata** 之後，請使用目前的部署指示來部署新巨量資料叢集。 如需詳細資訊, 請參閱 how [to deploy [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] on Kubernetes](deployment-guidance.md)。 接著，還原任何必要的資料庫或檔案。

## <a name="next-steps"></a>後續步驟

如需有關 big data 叢集的詳細資訊, 請參閱[什麼是[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] ](big-data-cluster-overview.md)。
