---
title: 升級為新版本
titleSuffix: SQL Server big data clusters
description: 瞭解如何將 SQL Server 2019 big data 叢集 (預覽) 升級至新版本。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7bdb1eb59fd36d065df9dba0f6d6879c1a294914
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419391"
---
# <a name="how-to-upgrade-sql-server-big-data-clusters"></a>如何升級 SQL Server big data 叢集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文提供如何將 SQL Server big data 叢集升級至新版本的指導方針。 本文中的步驟特別適用于如何在預覽版本之間升級。

## <a name="backup-and-delete-the-old-cluster"></a>備份和刪除舊叢集

目前, 將大型資料叢集升級至新版本的唯一方法, 就是手動移除並重新建立叢集。 每個版本都有與先前版本不相容的唯一**azdata**版本。 此外, 如果較舊的叢集必須在新的節點上下載映射, 則最新的映射可能與叢集上的舊版映射不相容。 若要升級至最新版本, 請使用下列步驟:

1. 在刪除舊叢集之前, 請先備份 SQL Server 主要實例和 HDFS 上的資料。 針對 SQL Server 的主要實例, 您可以使用[SQL Server 備份和還原](data-ingestion-restore-database.md)。 針對 HDFS, 您[可以使用**捲曲**複製資料](data-ingestion-curl.md)。

1. 使用`azdata delete cluster`命令刪除舊叢集。

   ```bash
    azdata bdc delete --name <old-cluster-name>
   ```

   > [!Important]
   > 使用符合您叢集的**azdata**版本。 請勿使用較新版本的**azdata**刪除較舊的叢集。

1. 在 CTP 3.2 之前, **azdata**稱為**mssqlctl**。 如果您已安裝任何舊版的**mssqlctl**或**azdata** , 請務必先卸載, 再安裝最新版本的**azdata**。

   針對 CTP 2.3 或更高版本, 請執行下列命令。 在`ctp3.1`命令中, 將取代為您要卸載的**mssqlctl**版本。 如果版本是在 CTP 3.1 之前, 請在版本號碼之前加上`ctp-2.5`破折號 (例如)。

   ```powershell
   pip3 uninstall -r https://mcr.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. 安裝最新版本的**azdata**。 下列命令會安裝適用于 CTP 3.2 的**azdata** :

   **時段**

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

   **廠商**

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!IMPORTANT]
   > 針對每個版本, **azdata**的路徑會變更。 即使您先前已安裝**azdata**或**mssqlctl**, 您還是必須從最新的路徑重新安裝, 才能建立新的叢集。

## <a id="azdataversion"></a>確認 azdata 版本

部署新的 big data 叢集之前, 請確認您使用的是最新版本的**azdata** `--version`搭配參數:

```bash
azdata --version
```

## <a name="install-the-new-release"></a>安裝新版本

移除先前的 big data 叢集並安裝最新的**azdata**之後, 請使用目前的部署指示來部署新的 big data 叢集。 如需詳細資訊, 請參閱[如何在 Kubernetes 上部署 SQL Server big data](deployment-guidance.md)叢集。 然後, 還原任何必要的資料庫或檔案。

## <a name="next-steps"></a>後續步驟

如需 big data 叢集的詳細資訊, 請參閱[什麼是 SQL Server big data](big-data-cluster-overview.md)叢集。
