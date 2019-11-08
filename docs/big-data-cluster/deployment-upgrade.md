---
title: 升級為新版本
titleSuffix: SQL Server big data clusters
description: 了解如何將 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] (預覽) 升級至新版本。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 90bfaaa1a8cb6fd42081d8afa5feff13f9aec37c
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531964"
---
# <a name="how-to-upgrade-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>如何升級 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文提供將 SQL Server 巨量資料叢集升級至新版本的指導。 本文中的步驟特別適用於如何從預覽版本升級至 SQL Server 2019 服務更新版本。

## <a name="backup-and-delete-the-old-cluster"></a>備份和刪除舊叢集

目前，沒有適用於巨量資料叢集的就地升級，升級至新版本的唯一方法是手動移除並重新建立叢集。 每個版本都有與先前版本不相容的唯一 `azdata` 版本。 此外，如果舊叢集必須在新節點上下載容器映像，則最新映像可能會與叢集上的舊版映像不相容。 請注意，只有在容器設定的部署設定檔中使用 `latest` 映像標籤，才會提取新版映像。 根據預設，每個版本都有一個對應至 SQL Server 發行版本的特定映像標籤。 若要升級至最新版本，請遵循下列步驟：

1. 在刪除舊叢集之前，請先備份 SQL Server 主要執行個體和 HDFS 上的資料。 針對 SQL Server 主要執行個體，您可以使用 [SQL Server 備份和還原](data-ingestion-restore-database.md)。 針對 HDFS，您[可以使用 `curl` 來複製資料](data-ingestion-curl.md)。

1. 使用 `azdata delete cluster` 命令刪除舊叢集。

   ```bash
    azdata bdc delete --name <old-cluster-name>
   ```

   > [!Important]
   > 使用符合您叢集的 `azdata` 版本。 請勿使用較新版本的 `azdata` 來刪除舊叢集。

   > [!Note]
   > 發出 `azdata bdc delete` 命令會導致刪除巨量資料叢集名稱所識別命名空間中建立的所有物件，但不會刪除命名空間本身。 命名空間只要是空的且其中未建立任何其他應用程式，就可以重複用於後續部署。

1. 解除安裝舊版 `azdata`

   ```powershell
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. 安裝最新版 `azdata`。 下列命令會從最新版本安裝 `azdata`：

   **Windows：**

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

   **Linux：**

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!IMPORTANT]
   > 針對每個版本，`azdata` 的 `n-1` 版本路徑會有所變更。 即使您先前已安裝 `azdata`，您還是必須從最新的路徑重新安裝，才能建立新的叢集。

## <a id="azdataversion"></a> 確認 azdata 版本

在您部署新的巨量資料叢集之前，請使用 `--version` 參數，確認您所使用的是最新版 `azdata`：

```bash
azdata --version
```

## <a name="install-the-new-release"></a>安裝新版本

在您移除先前的巨量資料叢集並安裝最新的 `azdata` 之後，請使用目前的部署指示來部署新巨量資料叢集。 如需詳細資訊，請參閱[如何在 Kubernetes 上部署 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](deployment-guidance.md)。 接著，還原任何必要的資料庫或檔案。

## <a name="next-steps"></a>後續步驟

如需巨量資料叢集的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](big-data-cluster-overview.md)。
