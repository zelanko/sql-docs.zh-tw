---
title: 升級為新版本
titleSuffix: SQL Server big data clusters
description: 了解如何升級至新版本的 SQL Server 2019 巨量資料叢集 （預覽）。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 45c489d7bb2dc6f0fea5815dce4b2f0ef11ae5ad
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/22/2019
ms.locfileid: "66015190"
---
# <a name="how-to-upgrade-sql-server-big-data-clusters"></a>如何升級 SQL Server 的巨量資料叢集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文章提供有關如何升級至新版本的 SQL Server 的巨量資料叢集的指引。 這篇文章中的步驟特別適用於如何預覽版本間進行升級。

## <a name="backup-and-delete-the-old-cluster"></a>備份並刪除舊的叢集

目前，巨量資料叢集升級至新版本的唯一方式是以手動方式移除並重新建立叢集。 每個版本具有的唯一版本**mssqlctl**不與舊版相容。 此外，如果較舊的叢集，就必須下載新的節點上的影像，最新的映像可能無法相容於舊叢集上的映像。 若要升級至最新版本時，使用下列步驟：

1. 然後再刪除舊的叢集，請 HDFS 和 SQL Server 的主要執行個體上備份資料。 SQL Server 的主要執行個體，您可以使用[SQL Server 備份及還原](data-ingestion-restore-database.md)。 HDFS 中，為您[的資料可以複製**curl**](data-ingestion-curl.md)。

1. 刪除舊的叢集使用`mssqlctl delete cluster`命令。

   ```bash
    mssqlctl cluster delete --name <old-cluster-name>
   ```

   > [!Important]
   > 使用新版**mssqlctl**符合您的叢集。 請勿刪除舊的叢集中，較新版的**mssqlctl**。

1. 如果您有任何舊版**mssqlctl**安裝，請務必要解除安裝**mssqlctl**第一次，然後再安裝最新版本。

   如果您要解除安裝**mssqlctl**對應至 CTP 2.2] 或 [較低的執行：

   ```powershell
   pip3 uninstall mssqlctl
   ```

   CTP 2.3 或更新版本，請執行下列命令。 取代`ctp-2.5`在命令中使用新版**mssqlctl**您要解除安裝：

   ```powershell
   pip3 uninstall -r  https://private-repo.microsoft.com/python/ctp-2.5/mssqlctl/requirements.txt
   ```

1. 安裝最新版**mssqlctl**。 下列命令會安裝**mssqlctl**針對 CTP 3.0:

   **Windows:**

   ```powershell
   pip3 install -r  https://private-repo.microsoft.com/python/ctp3.0/mssqlctl/requirements.txt
   ```

   **Linux:**

   ```bash
   pip3 install -r  https://private-repo.microsoft.com/python/ctp3.0/mssqlctl/requirements.txt --user
   ```

   > [!IMPORTANT]
   > 每個發行的路徑**mssqlctl**變更。 即使您先前已安裝**mssqlctl**，您必須建立新的叢集之前重新安裝最新的路徑。

## <a id="mssqlctlversion"></a> 確認 mssqlctl 版本

再部署新的巨量資料叢集，請確認您使用最新版**mssqlctl**與`--version`參數：

```bash
mssqlctl --version
```

## <a name="install-the-new-release"></a>安裝新的版本

移除先前的巨量資料叢集並安裝最新版本後**mssqlctl**，部署新的巨量資料叢集使用目前的部署指示。 如需詳細資訊，請參閱 <<c0> [ 如何部署 SQL Server 的巨量資料叢集的 Kubernetes 上](deployment-guidance.md)。 然後，將還原的任何必要的資料庫或檔案。

## <a name="next-steps"></a>後續步驟

如需有關巨量資料叢集的詳細資訊，請參閱[什麼是 SQL Server 的巨量資料叢集](big-data-cluster-overview.md)。
